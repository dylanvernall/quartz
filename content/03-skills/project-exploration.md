---
title: "Project Exploration and Directory Mapping"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/process", "#domain/development"]
summary: "Map directory structure upfront with find and grep to avoid repeated path lookups in unfamiliar projects."
sources: ["memory/feedback_path_navigation_efficiency.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Project Exploration and Directory Mapping

## Rule

When working in an unfamiliar project, spend 30 seconds mapping the directory structure with `find` before attempting edits. This prevents repeated failed path lookups and clarifies project organization upfront.

## Why

Without structure mapping upfront, time is spent on multiple failed attempts:
- Running tests with incorrect paths (failed 3+ times)
- Searching for the same file multiple times across sessions
- Using full paths inconsistently
- Unclear understanding of module organization

Root cause: Diving into implementation before exploring. The mapping phase takes 30 seconds but saves 5–10 minutes in failed lookups and rework.

## How to Apply

### Quick Structure Discovery

Run these commands to reveal directory organization:

```bash
# Find test files and test locations
find . -type f -name "*.py" | grep -E "(test_|_test\.py|tests\.py)" | head -20

# Identify common source code directories
find . -type d -name "tests" -o -name "test" -o -name "src" | head -10

# Check for common project files
find . -maxdepth 2 -name "setup.py" -o -name "pyproject.toml" -o -name "Makefile"
```

### What This Reveals

These commands immediately show:
- Test location patterns (pytest, unittest, custom structure)
- Source code organization (src/ vs module-at-root)
- Module naming conventions
- Project type (package, monorepo, single-script)

### Example: Time-Tracker Project

Running `find . -type f -name "*.py" | grep -E "(test_|_test\.py)" | head -20` would have immediately shown:

**What I expected**: `tests/unit/adapters/test_*.py` structure
**What actually existed**: Different test organization
**Time saved**: ~5 minutes by discovering before implementing

## Applied

- Time-tracker project: 3 failed path lookups → mapped structure upfront
- Met-pipeline refactor: Quick find revealed pytest structure immediately
- Result: Zero follow-up path corrections needed

## Related Skills

- [[07-Wiki/03-skills/directory-structure-mapping|Directory Structure Mapping]]
- [[07-Wiki/03-skills/code-quality|Code Quality Standards]]
