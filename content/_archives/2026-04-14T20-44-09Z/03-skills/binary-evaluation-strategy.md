---
title: "Binary Evaluation Strategy for Code Quality Loops"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/code-quality", "#topic/optimization", "#domain/development"]
summary: "Calculate estimated iterations for each binary evaluation upfront; pivot early if initial eval proves more expensive than remaining budget."
sources: ["memory/feedback_binary_eval_strategy.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Binary Evaluation Strategy for Code Quality Loops

## Rule

When running autonomous code quality optimisation loops with multiple binary (all-or-nothing) evaluations, **calculate estimated iterations required for each eval BEFORE starting**. Pivot early if initial eval proves more expensive than remaining budget.

## Why

Binary evaluations require 100% compliance to flip. Partial progress yields zero points:
- Function length (Q1): 69 violations × 1 iteration/violation = ~69 iterations to complete
- Cyclomatic complexity (Q2): 4 violations with clear extraction patterns = ~5 iterations to complete

Choosing Q1 over Q2 would cost 15+ iterations vs. actual 5 spent. Strategic selection beats raw effort.

## How to Apply

### 1. Upfront Assessment

List all failing evaluations with violation counts:

```
Q1: 69 length violations (estimated 15+ iterations)
Q2: 4 CC violations (estimated 5 iterations)
Q5: 8+ DRY categories (estimated 8+ iterations)
Q6: 46 bare except (estimated 2–3 iterations, mechanical fix)
```

### 2. Calculate ROI

ROI = (eval_importance × flip_probability) / estimated_cost

```
Q2: (1.0 × 0.95) / 5 = 0.19 per iteration ← BEST
Q6: (1.0 × 0.95) / 2 = 0.47 per iteration ← SECOND
Q1: (1.0 × 0.80) / 15 = 0.05 per iteration ← POOR
```

### 3. Prioritise by ROI

Not by eval name or apparent importance — rank by ROI score.

### 4. Commit to Eval

Execute methodically with batch approaches (see Batch Pattern Identification skill).

### 5. Pivot Early

If actual cost exceeds estimate:
- If Q2 required 7 iterations instead of 5, stop and reassess
- Move to next-highest ROI eval
- Never force low-ROI evaluations

## Edge Case

If only one eval remains and budget is tight, sometimes accepting partial credit is better than zero. But for loops targeting 60%+ goals, strategic selection typically wins.

## Validation

This session validated the pattern:
- Committed to Q2 after assessing Q1 cost → saved ~10 iterations
- Batch fixes (Q3 docstring, Q4 type hints, Q6 exceptions) flipped quickly
- Foundation work (timing_utils) didn't flip eval alone but created optionality

## Related Skills

- [[07-Wiki/03-skills/batch-pattern-identification|Batch Change Pattern Identification]]
- [[07-Wiki/03-skills/pivot-metric-refinement|PIVOT Metric Refinement]]
