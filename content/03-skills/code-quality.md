---
title: "Code Quality Standards"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/code-quality", "#domain/engineering"]
summary: "Standards for code structure, complexity, encoding, and quality metrics."
sources: [".claude/rules/code-quality.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Code Quality Standards

## Rule

**No arbitrary values. Every numeric claim must be sourced, dated, and contextualized.**

All code must maintain cyclomatic complexity < 7 (Grade A), pass linting checks (flake8, ruff), use ASCII-only encoding, and follow language-specific conventions (PEP8 for Python, no emojis or Unicode).

## Why

- **Maintainability**: Complexity > 7 makes code harder to test and reason about. Extract helper functions or use early returns to reduce branching.
- **Security**: ASCII encoding prevents cp1252 compatibility issues on Windows. No arbitrary hardcoded values without research validation prevents accidental misuse of unvalidated assumptions.
- **Reliability**: Sourced values ensure decisions are based on evidence, not guesses.

## How to Apply

### Numeric Claims

**Pattern**: Every number in code needs a citation.

- ❌ "typically 3" → ✅ "research indicates values of 2–4, with 3 commonly used in published studies (Smith et al., 2024)"
- ❌ "usually 1.5–2×" → ✅ "[cite specific measurement or paper]"

### Encoding: ASCII Only

**Critical rule**: NO emojis, Unicode, macrons, arrows, or special characters in:
- Source code (Python, JS, TS)
- Markdown vault documents
- Git commit messages
- Console output and logs

**Use ASCII indicators**: `[ERROR]`, `[OK]`, `[WARNING]`, `[PASS]`, `[FAIL]`, `[INFO]`

### Cyclomatic Complexity

**Measure**: Run `radon cc src/ --average`

**Target**: < 7 (Grade A), maximum < 10 (Grade B)

**Fix strategy**:
1. Extract conditional logic into helper functions
2. Use early returns to reduce nesting
3. Split large functions at logical boundaries

### Code Structure

- Single responsibility: each function does one thing
- Descriptive naming: `calculate_daily_average()` not `calc()` or `x()`
- Function length: aim for < 40 lines
- Line length: max 100 characters (flake8 default)
- Docstrings: required for public functions/classes
- Error handling: catch specific exceptions, fail fast, never bare `except:`
- Validation: validate at system boundaries (user input, external APIs), not internal code

### Test-Driven Development (TDD)

1. **Red**: Generate unit tests first with edge cases
2. **Green**: Write minimal implementation to pass tests
3. **Refactor**: Clean up while tests pass
4. **Validate**: Check complexity, security, quality metrics

### Linting Tools

- **flake8**: Finds style violations (max-line-length=100)
- **radon cc**: Measures cyclomatic complexity
- **black**: Auto-formats code
- **ruff check**: Security and performance violations

## Applied

- Met-pipeline codebase: complexity < 5 average across modules
- Ralph FastAPI: ASCII-only output in diagnostic logs, no emoji use

## Related Skills

- [[07-Wiki/03-skills/testing-with-real-data|Testing with Real Data]]
- [[07-Wiki/03-skills/skill-self-containment|Skill Self-Containment Pattern]]
