---
title: "Confirm Ambiguous Requests Before Proceeding"
created: 2026-04-14T10:05:00Z
modified: 2026-04-14T10:05:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/communication", "#topic/clarification", "#domain/workflow"]
summary: "When user requests are incomplete or ambiguous, pause and ask for clarity rather than inferring scope."
sources: ["memory/feedback_confirm_before_completing.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Confirm Ambiguous Requests Before Proceeding

## Rule

When a user asks to "continue" or "add to" incomplete instructions, ask what comes next rather than inferring from context.

## Why

Auto-completing abstract structure (adding results when only methodology was requested) wastes effort and requires rework. This pattern can frustrate users who haven't specified the full scope yet.

## How to Apply

- **Ambiguous requests** (e.g., "continue from X" without specifying what section): pause and ask
- **Iterative writing tasks** where structure matters: ask clarifying questions BEFORE generating content
- **Example conversation**:
  - User: "Continue after the methodology section"
  - Response (good): "What should come after methodology — results, conclusions, or something else?"
  - Response (bad): Assume results and write them without asking

## Related Skills

- [[07-Wiki/03-skills/scope-clarity|Scope Clarity and Verification]]
- [[07-Wiki/03-skills/communication-patterns|Communication Patterns]]
