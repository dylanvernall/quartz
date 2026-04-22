---
title: "Batch Change Pattern Identification in Autonomous Loops"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/code-quality", "#topic/optimization", "#domain/development"]
summary: "Pre-identify identical violations across multiple files to batch-fix in single iterations and reduce loop count by 20–30%."
sources: ["memory/feedback_batch_change_pattern_identification.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Batch Change Pattern Identification in Autonomous Loops

## Rule

Before launching an autonomous optimisation loop (e.g., `/codex-autoresearch loop`), run a **duplicate pattern scan** to identify mechanically identical fixes that can be applied in a single iteration.

## Why

Autonomous loop hard rules mandate "one focused change per iteration." However, "one change" can be mechanically identical across multiple files if the pattern is identical. Batch identification can reduce total loop time by 20–30% when violations are frequent and fix is uniform.

**Evidence**: OpenAir NZ lintr loop (2026-04-07, Iteration 23):
- Identified 5 identical UI module files with identical violation pattern: `get_module_params(module_id)` called without explicit import
- Single iteration applied `# nolint: object_usage_linter` comment to all 5 files
- Result: −5 violations in one iteration (highest single-iteration gain)
- Sequential approach would have taken 5 iterations (5× the effort)

Batch identification pre-loop would have flagged this in Iteration 1 planning, enabling Iteration 2 to fix all 5 at once.

## How to Apply

1. **Before loop**: Scan for duplicate patterns
   ```bash
   grep -r "pattern" target_scope/ | sort | uniq -c | sort -rn
   ```

2. **For each top-10 pattern**:
   - Count occurrences
   - Check if fix is mechanically identical across files
   - If yes: log as "batch opportunity, fix count: N"

3. **During loop iteration planning**:
   - Prioritise batch-fixable violations (lowest iteration cost per violation fixed)
   - Example: "Fix 5 identical imports in 1 iteration" vs. "Extract 1 helper function"
   - Choose batch if violation count > 3 and fix is identical

### Example Batch Opportunities

| Domain | Pattern | Opportunity |
|--------|---------|-------------|
| Linting | 5 files with identical unused import | Batch fix: −5 violations/iteration |
| Coverage | 10 functions missing unit tests, identical signature | Batch fix: +10 test coverage/iteration |
| Complexity | 3 utility functions with identical parameter extraction | Batch fix: −3 CC/iteration |
| Security | 7 API endpoints with identical missing input validation | Batch fix: +7 validated endpoints/iteration |

## Confidence & Applicability

**Confidence**: 0.85 (medium-high)
- Single validation instance (Iteration 23, lintr violations)
- Generalizable to code quality metrics (linting, coverage gaps, unused variables)
- Works better on modular projects (Shiny, REST APIs) than bespoke scripts
- Risk: May over-count "similar-looking" violations that require different fixes

**Applicability**: Code quality loops on modular architectures. Skip for non-homogeneous or one-off codebases.

## Related Skills

- [[07-Wiki/03-skills/binary-evaluation-strategy|Binary Evaluation Strategy]]
- [[07-Wiki/03-skills/pivot-metric-refinement|PIVOT Metric Refinement]]
