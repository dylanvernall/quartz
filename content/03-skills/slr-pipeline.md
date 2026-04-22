---
title: "Systematic Literature Review Pipeline Patterns"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/slr-methodology", "#domain/research"]
summary: "Error handling, validation, and API performance patterns for SLR data pipeline — silent error prevention, checkpoint drift detection, real data integration testing."
sources: ["memory/feedback_slr_pipeline_code_review.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Systematic Literature Review Pipeline Patterns

## Rule

Build SLR data pipelines with these guardrails: (1) validate success flags before appending results, (2) detect checkpoint configuration drift, (3) use real external data in integration tests, (4) extract complex logic to helpers (CC < 7).

## Why

Real-world SLR pipelines fail silently: extraction errors append to result collections, pass through 3 downstream stages with no error flag, and surface only in final reports as placeholder text. Mocked tests passed; real data revealed silent data loss across 5 modules. Checkpoint configuration changes mid-run invalidated 360+ screened citations. Code complexity (CC=7+) made branch testing incomplete.

## How to Apply

### Silent Data Loss Prevention

**Pattern**: Always validate success flags BEFORE appending to result collections. Use fail-fast validation with explicit logging.

**Implementation**:
```python
# ✅ Good: Validate before append
if extraction_success is True:
    results.append(extracted_data)
    log_info(f"Extracted {identifier}")
else:
    log_warning(f"Extraction failed for {identifier}: {error}")
    rejected_count += 1

# ❌ Bad: Silent append of error state
results.append(extraction_result)  # Result may contain error flag, not data
```

**Key rules**:
- Use `is not True` pattern (not `!= True`) for boolean validation
- Always log rejected records with reason and identifier
- Never silently drop or convert error states to default values

### Checkpoint Configuration Drift Detection

**Pattern**: Validate configuration hasn't changed since checkpoint was created. Use config hash (SHA256) to detect drift.

**Implementation**:
```python
# Save checkpoint with config hash
config_fields = [criteria_version, screening_rules, api_keys]
config_hash = sha256(json.dumps(config_fields)).hexdigest()
save_checkpoint(data={'results': results, 'config_hash': config_hash})

# Load checkpoint with validation
loaded = load_checkpoint()
current_hash = sha256(json.dumps(config_fields)).hexdigest()
if loaded['config_hash'] != current_hash:
    log_warning(f"Config mismatch: {loaded['config_hash']} vs {current_hash}")
    discard_checkpoint()  # Start fresh
```

**Why**: Real incident where screening criteria were modified mid-run but checkpoint reused with old criteria, producing invalid results.

### Real Data Integration Testing

**Pattern**: Never mock external systems in integration tests. Always use real data flowing through actual API integration points.

**Why Mocks Fail**:
- Null field handling bugs (real APIs return null, mocks return defaults)
- Rate limiting and backoff failures (mocks don't test these)
- API response structure changes (mocks are frozen)
- Silent data type conversions

**Implementation**:
- Keep mocked unit tests for fast feedback
- Add integration test suite using real external data
- Test end-to-end checkpoint roundtrips (save → reload → compare)
- Test error handling by injecting real error responses
- Verify no placeholder text in outputs (indicates missing data)

### Cyclomatic Complexity Reduction

**Pattern**: Extract conditional branches to helper functions. Target CC < 5 per function.

**Implementation**:
```python
# ❌ High complexity: Nested for + nested if = CC > 5
def process_records(records):
    for record in records:
        if record.valid:
            if record.type == 'abstract':
                # Extract logic (nested)
            elif record.type == 'title':
                # Extract logic (nested)

# ✅ Low complexity: Extract to helpers
def process_records(records):
    for record in records:
        if record.valid:
            _extract_field(record)

def _extract_field(record):
    # Separate concern: CC < 3
```

### API Abstraction & Rate Limiting

**Pattern**: Extract API fetching logic to generic method with pluggable extraction functions.

**Consolidates**: Caching, error handling, rate limiting, retry logic.

**Pattern**:
```python
def _fetch_abstract(key, cache, fetch_func, extract_func):
    # Shared: caching, validation, error logging, rate limiting
    result = self.rate_limiter.call_with_backoff(fetch_func, key)
    return extract_func(result) if result else None
```

**Rate Limiting Rule**: Wrap all HTTP calls in `rate_limiter.call_with_backoff()` with exponential backoff (1s → 2s → 4s).

## Applied

- 2026-03-30: Code review identified 9 issues across orchestrator, data_extractor, quality_assessor
- Silent error handling: 3+ modules lacked validation; 1-2 hours per module to fix
- Checkpoint drift: 1 hour to implement config hash validation
- Integration testing: Added real-data suite; caught 5 bugs mocked tests missed
- Complexity reduction: Extracted CC=7 function → CC < 3 main + CC < 5 helpers
- Result: 99%+ extraction success rate; zero placeholder text in final reports

## Related Skills

- [[07-Wiki/03-skills/slr-pipeline-patterns|SLR Workflow Patterns]]
- [[07-Wiki/03-skills/testing-with-real-data|Testing with Real Data]]
- [[07-Wiki/03-skills/slr-web-search-synthesis|SLR Web Search Synthesis]]
