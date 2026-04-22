---
title: "Communication Patterns"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/communication", "#topic/process"]
summary: "Asking clarifying questions before auto-completing scope, teaching patterns inline during work."
sources: ["memory/feedback_confirm_before_completing.md", "memory/feedback_teach_patterns_as_we_go.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Communication Patterns

## Rule

**When a user request is ambiguous or incomplete, ask clarifying questions BEFORE generating content. Teach development patterns inline during work — name the pattern, explain why, note when to apply it.**

## Why

- **Efficiency**: Auto-completing abstract structure (inferring what comes next) wastes effort and requires rework. Clarifying first saves iterations.
- **Learning**: Understanding patterns organically through real work beats abstract instruction. Brief inline callouts anchor learning in context.
- **Collaboration**: Explicit clarification signals respect for the user's intent and reduces misalignment.

## How to Apply

### Scope Clarification

When a request is ambiguous or incomplete, pause and ask rather than inferring.

**Pattern**:
- User: "Continue from X"
- You: "What should come after X — [option A], [option B], or [option C]?"

**Examples**:
- ✗ Auto-complete: Assume "add results" means "add results + conclusions"
- ✓ Clarify first: "Should I add results, conclusions, or discussion? Or something else?"

- ✗ Auto-complete: Infer the structure from context
- ✓ Clarify first: Ask explicitly if ambiguous

**Especially apply**: Iterative writing tasks where structure matters (methodologies, reports, multi-part implementations).

### Pattern Teaching

Weave brief explanations into responses whenever a notable pattern is being used.

**Pattern**: Name the pattern, explain why it's used, note when to apply. Keep it brief: 1–3 sentences.

**Examples**:

```
"I'll use TDD here — write tests first (Red), minimal implementation
(Green), then refactor (Refactor). This ensures edge cases are caught
before code cleanup."
```

```
"This is batch change pattern identification — scanning for duplicates
upfront and fixing similar issues in one pass saves 20–30% effort vs
fixing sequentially."
```

```
"Using atomic commits here (one change per commit) so the history is
readable and reversions can be precise."
```

**Benefits**:
- User learns patterns through practice, not lecture
- Patterns are contextual (user understands WHEN to apply them)
- Work flows naturally without interruption
- Builds shared vocabulary over time

## Applied

- Vault work: "I'll use memory consolidation pattern here — delete superseded files first, then merge overlapping content"
- Code reviews: "Extracting a helper function here to reduce cyclomatic complexity from 8 to 5 (target < 7)"
- Skill development: "Skill self-containment pattern — bundling input dependencies in the skill folder so it's portable"

## Related Skills

- [[07-Wiki/03-skills/confirm-ambiguous-requests|Confirming Ambiguous Requests]]
- [[07-Wiki/03-skills/scope-clarity|Scope Clarity and Confirmation]]
