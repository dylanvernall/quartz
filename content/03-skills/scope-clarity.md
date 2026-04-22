---
title: "Scope Clarity and Confirmation"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/process", "#topic/decision-making"]
summary: "Asking before auto-completing scope; treating ambiguous requests as signals to clarify, not infer."
sources: ["memory/feedback_confirm_before_completing.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Scope Clarity and Confirmation

## Rule

**When user request is incomplete or ambiguous, ask what comes next rather than inferring from context. Do not auto-complete scope.**

## Why

- **Misalignment**: Inferring the next step often leads to wasted work that needs rework. Explicit clarification avoids cycles.
- **Signal**: Ambiguity in the request is a signal to ask, not a prompt to guess.
- **Iteration efficiency**: Asking upfront costs seconds; rework costs minutes.

## How to Apply

### Recognize Ambiguous Requests

These signals suggest you should ask rather than infer:
- "Continue from X" (without specifying what X continues to)
- "Add to Y" (without specifying what else should be added)
- "Do Z and..." (trailing off without finishing the thought)
- "Improve X" (without clarifying which aspect or what "good" looks like)

### Pause and Ask

**Pattern**:
1. User provides partial instruction
2. You recognize ambiguity
3. STOP — don't generate content yet
4. Ask: "Should I [option A], [option B], or [option C]?" OR "What should come next?"
5. Wait for answer
6. THEN generate

### Examples

**Example 1 — Incomplete structure**
```
User: "Continue the methodology section"
[Ambiguous: next section unclear]

You: "Got it. After methodology should I add results,
      conclusions, or another section?"
```

**Example 2 — Unclear improvement target**
```
User: "Improve this code"
[Ambiguous: which aspect? performance, readability, tests?]

You: "What's the priority — readability, performance, test coverage,
      or something else?"
```

**Example 3 — Partial task**
```
User: "Add the new feature and..."
[Ambiguous: trailing off, unclear what else is needed]

You: "Add the feature. After that should I also update tests,
      documentation, or something else?"
```

### When Scope is Clear

If the request is explicit ("Add unit tests for the API endpoints"), generate without asking. Scope clarity is only asked when ambiguous.

## Applied

- Vault rebuild: Clarified "rebuild wiki" → 4-unit plan with explicit scope per unit
- Skill development: Clarified "add field documentation" → asked which YAML fields before writing
- Code review: Clarified "improve this" → asked target complexity, performance, or readability focus

## Related Skills

- [[07-Wiki/03-skills/confirm-ambiguous-requests|Confirming Ambiguous Requests]]
- [[07-Wiki/03-skills/communication-patterns|Communication Patterns]]
