---
title: "SLR Pipeline Code Patterns"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/code-quality", "#topic/data-pipelines"]
summary: "Prevent silent data loss in SLR pipelines: validate success flags before appending, use real-data integration tests, config-hash checkpoints, and rate limiting for API calls."
sources: ["memory/feedback_slr_pipeline_code_review.md"]
provenance:
  extracted: 0.85
  inferred: 0.10
  ambiguous: 0.05
---

# SLR Pipeline Code Patterns

## Pattern 1: Silent Data Loss Prevention

**Rule:** Always validate success flags (e.g., `extraction_success == True`) BEFORE appending to result collections. Use fail-fast validation with explicit logging.

**Why:** Real incident where extraction errors were silently appended to lists, passed through 3 downstream stages with no error indication, and resulted in placeholder text in final reports. Problem only discovered during real-data testing.

**How to apply:**
- Check for success/error indicators before using results
- Use `is not True` pattern (not `!= True`) for boolean validation
- Always log rejected records with reason and identifier
- Never silently drop or convert error states to default values

## Pattern 2: Checkpoint Config Validation

**Rule:** When resuming from checkpoints, validate that configuration hasn't changed since checkpoint creation. Use config hash (SHA-256) to detect drift.

**Why:** Real incident where screening criteria were modified mid-run, but checkpoint was reused with old criteria, producing invalid results (360 citations screened with old criteria under new rules).

**How to apply:**
- Calculate config hash when saving checkpoint (SHA-256 of relevant config fields)
- Compare config hash when loading checkpoint
- If mismatch: log warning with hashes, discard checkpoint, start fresh
- Store `config_hash` alongside checkpoint data (not in separate files)

## Pattern 3: Real Data Integration Testing

**Rule:** Never mock external systems in integration tests. Always use real data flowing through actual API integration points.

**Why:** Mocked screening/extraction tests passed but real pipeline failed immediately. Mocks cannot catch:
- Null field handling bugs (real APIs return null, mocks return defaults)
- Rate limiting and backoff failures
- API response structure changes
- Silent data type conversions

**How to apply:**
- Keep mocked unit tests for fast feedback
- Add integration test suite using real external data
- Test end-to-end checkpoint roundtrips (save → reload → compare)
- Test error handling by injecting real error responses
- Verify no placeholder text in outputs (indicates missing data)

## Pattern 4: Cyclomatic Complexity Refactoring

**Rule:** Extract conditional branches to helper functions. Target CC < 5 per function.

**Why:** Complex functions (CC > 7) with nested loops + conditionals are hard to test, high defect density. Example: `_reconstruct_openalex_abstract` had CC=7.

**How to apply:**
- Count if/for/while statements (each +1 to complexity)
- If CC > 5, extract nested branches to separate functions
- Use helper functions for data transforms
- Result: simpler main function (CC < 3), testable helpers (CC < 5 each)

## Pattern 5: API Abstraction

**Rule:** Extract API fetching logic to generic method with pluggable extraction functions. Consolidates caching, error handling, rate limiting.

**Why:** Multiple identical abstract-fetching methods (PubMed XML, CrossRef JSON, OpenAlex JSON) with 50+ duplicate lines. Each had slightly different error handling.

**How to apply:**
```python
_fetch_abstract(key, cache, fetch_func, extract_func):
  # fetch_func: performs API call (returns bytes or dict)
  # extract_func: parses response into abstract string
  # Shared: caching, validation, error logging, rate limiting
```

Result: DRY code, consistent behavior, easier to add new sources.

## Pattern 6: Rate Limiting Integration

**Rule:** All outbound API calls must use rate limiter with exponential backoff.

**Why:** Sequential API calls at max speed cascade failures. Backoff reduces load and improves success rate.

**How to apply:**
- Initialize `SimpleRateLimiter(min_delay=0.5, max_retries=3)`
- Wrap HTTP calls: `self.rate_limiter.call_with_backoff(fetch_func)`
- Exponential backoff: 1s → 2s → 4s retries
- Log failures at DEBUG level (avoid alarm fatigue)

## Quality Checklist

- [ ] All extraction results validated before appending
- [ ] Checkpoints include config hash
- [ ] Integration tests use real API data
- [ ] All functions CC < 5 or extracted to helpers
- [ ] No duplicate API fetching code
- [ ] All API calls use rate limiter with backoff

## Related Skills

- [[07-Wiki/03-skills/testing-with-real-data|Testing with Real Data]]
- [[07-Wiki/03-skills/code-quality|Code Quality Standards]]
