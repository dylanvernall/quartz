---
title: "Directory Structure Mapping"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/code-quality", "#topic/project-exploration"]
summary: "Map unfamiliar project structure with find+grep upfront (30 sec) to avoid repeated path lookups and failed attempts."
sources: ["memory/feedback_path_navigation_efficiency.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Directory Structure Mapping

## Rule: Explore Directory Structure Before Editing

When working in an unfamiliar project, spend 30 seconds mapping the directory structure with `find` and `grep` before attempting edits.

**Why:**

Repeated path lookup failures waste time:
- Running tests with incorrect paths (fails 3+ times)
- Searching for specific files multiple times
- Inconsistent path usage across edits

Root cause is lack of upfront structure exploration.

## How to Apply

Before writing code, run these discovery commands:

**Find test files:**
```bash
find . -type f -name "*.py" | grep -E "(test_|_test\.py|tests\.py)" | head -20
```

**Find test and source directories:**
```bash
find . -type d -name "tests" -o -name "test" -o -name "src" | head -10
```

**For other languages**, adjust patterns:
- JavaScript: `-name "*.test.js" -o -name "*.spec.js"`
- Ruby: `-name "test_*.rb" -o -name "*_spec.rb"`
- Go: `-name "*_test.go"`

## What This Reveals

- Test location patterns (unit, integration, e2e separation)
- Source code organization (flat vs nested modules)
- Module naming conventions (snake_case vs camelCase)
- Entry points and main files
- Configuration directory structure

## Example

In time-tracker project, this would have immediately shown:
- No `tests/unit/adapters/test_*.py` files
- Actual structure differs from expected code organization
- Correct test patterns to follow

**Time saved:** ~5 minutes per unfamiliar project by avoiding failed path lookups.

## Related Skills

- [[07-Wiki/03-skills/code-quality|Code Quality Standards]]
- [[07-Wiki/03-skills/project-exploration|Project Exploration Patterns]]
