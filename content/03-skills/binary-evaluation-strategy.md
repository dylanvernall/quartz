---
title: "Binary Evaluation Strategy for Code Quality Loops"
created: 2026-04-14T15:46:00+12:00
modified: 2026-04-14T15:46:00+12:00
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/code-quality", "#topic/optimization"]
sources: ["~/.claude/projects/c--Vault-Lite/memory/feedback_binary_eval_strategy.md"]
summary: "Calculate ROI upfront for binary code quality evaluations; pivot early if initial eval proves more expensive than remaining budget."
provenance: "extracted: 1.0"
---

## Rule: Strategic Evaluation Selection Before Starting

**Why:** Binary evaluations require 100% compliance to flip (all-or-nothing). Partial progress yields zero points. Choosing the wrong eval can waste 15+ iterations vs 5 actual iterations needed.

**How to apply:**

### 1. Upfront Assessment

List all failing evals with violation counts:
```
Q1: 69 length violations (estimated 15+ iterations)
Q2: 4 CC violations (estimated 5 iterations)
Q5: 8+ DRY categories (estimated 8+ iterations)
Q6: 46 bare except (estimated 2-3 iterations, mechanical fix)
```

### 2. Calculate ROI

ROI = (eval_importance × flip_probability) / estimated_cost

```
Q2: (1.0 × 0.95) / 5 = 0.19 per iteration ← BEST
Q6: (1.0 × 0.95) / 2 = 0.47 per iteration ← SECOND
Q1: (1.0 × 0.80) / 15 = 0.05 per iteration ← POOR
```

### 3. Prioritize by ROI

Not by eval name or apparent importance — follow the numbers.

### 4. Execute Methodically

Commit to eval, use batch approaches for similar violations.

### 5. Pivot Early

If actual cost exceeds estimate (Q2 takes 7 instead of 5), stop and reassess. Move to next-highest ROI eval. Never force low-ROI evals.

## Pattern Validation

Choosing Q2 over Q1 after cost assessment saved ~10 iterations in practice. Strategic selection typically wins for loops targeting 60%+ goals.
