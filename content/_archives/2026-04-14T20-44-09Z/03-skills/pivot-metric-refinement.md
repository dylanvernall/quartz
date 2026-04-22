---
title: "PIVOT Metric Refinement Heuristic"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/code-quality", "#topic/optimization", "#domain/development"]
summary: "Trigger PIVOT Phase 1 after 2+ consecutive DISCARD decisions if architectural constraints prevent improvement; don't wait for 3rd discard."
sources: ["memory/feedback_pivot_metric_refinement_heuristic.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# PIVOT Metric Refinement Heuristic

## Rule: Trigger PIVOT Phase 1 After 2 Consecutive DISCARDs

Autonomous optimisation loops typically wait for 3 consecutive DISCARD decisions before escalating to metric refinement. However, research shows **2 consecutive DISCARDs signal architectural constraints** — escalate immediately.

When an autonomous optimisation loop produces 2+ consecutive DISCARD decisions, immediately evaluate whether remaining violations/improvements are:

1. **Suppressive-only** (fixable via configuration, comments, feature flags, suppressions): continue iterating
2. **Architectural** (require design change, breaking changes, cross-module refactoring): escalate to PIVOT Phase 1 immediately

## Why

Diagnostic data from OpenAir NZ lintr loop (2026-04-07, Iterations 15–25) shows:

- **Iteration 15**: Attempted line-length fix → 0 improvement → DISCARD (architectural: requires roxygen documentation refactoring)
- **Iteration 20**: Attempted utils_analysis_ui structure change → 0 improvement → DISCARD (architectural: variable scoping design)
- **Iteration 21**: PIVOT Phase 1 applied (metric refined from "total violations" to "pragmatically suppressible violations")
- **Iterations 22–25**: 4 consecutive KEEP decisions, achieved goal (115 → 24 violations, 79.1%)

Early PIVOT escalation (at 2 DISCARDs instead of waiting for 3) would have recovered the loop 1 iteration earlier, saving ~3 minutes.

## How to Apply

1. **After each DISCARD decision**, inspect the change that failed
2. **If DISCARD reason is "metric unchanged (±0.1%)" or "no behavioural change"**:
   - Ask: "Would this improvement require changing system design, breaking changes, or refactoring outside current scope?"
   - If **YES**: trigger PIVOT Phase 1 immediately (don't wait for 3rd DISCARD)
   - If **NO**: continue to next iteration
3. **PIVOT Phase 1**: Refine metric definition, lower pass criterion, or adjust scope constraints
4. **Resume loop** with refined metric

## Confidence & Applicability

**Confidence**: 0.89 (high)
- Validated in OpenAir NZ session (lintr violations, 4-iteration recovery)
- Generalizable to code quality loops (cyclomatic complexity, coverage, violations)
- **Risk**: May over-escalate on noisy metrics with random failures (don't apply to flaky tests, network-dependent evals)

**Applicability**: Code optimisation loops (CC, linting, coverage), deterministic metrics only. Skip for non-deterministic evaluation commands.

## Related Skills

- [[07-Wiki/03-skills/binary-evaluation-strategy|Binary Evaluation Strategy]]
- [[07-Wiki/03-skills/batch-pattern-identification|Batch Change Pattern Identification]]
