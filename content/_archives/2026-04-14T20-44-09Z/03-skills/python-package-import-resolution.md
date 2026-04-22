---
title: "Python Package Import Resolution"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/python", "#topic/code-quality"]
summary: "Fix ModuleNotFoundError by ensuring proper package structure: __init__.py in all package directories, correct pytest working directory, or package installation (setup.py/pyproject.toml)."
sources: ["memory/feedback_python_package_imports.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Python Package Import Resolution

## Rule: Package Structure Must Be Explicit

Python's import system requires proper package structure. Tests fail with `ModuleNotFoundError: No module named 'module'` when package structure is incomplete.

## Why

Import failures typically indicate one of three issues:

1. **Missing `__init__.py`** — Directories must be explicitly marked as packages
2. **Wrong pytest working directory** — Tests run from wrong directory relative to imports
3. **Package not installed** — No setup.py or pyproject.toml to make package discoverable

## How to Apply

### Fix 1: Add `__init__.py` to All Package Directories

Create empty `__init__.py` in all directories that are imported:

```
ralph/
├── src/
│   ├── __init__.py          ← Add this
│   ├── retrieval.py
│   └── transformers.py
├── tests/
│   ├── __init__.py          ← Add this
│   ├── test_retrieval.py
```

### Fix 2: Update Import Paths

Choose one consistent pattern:

**Option A: Relative to source directory** (recommended for pytest)
```python
# If pytest run from ralph/ directory
from src.retrieval import SomeClass
```

**Option B: Full package path** (requires package installation)
```python
# Only works if ralph is installed as package
from ralph.src.retrieval import SomeClass
```

### Fix 3: Package Installation

For Option B, ensure `setup.py` or `pyproject.toml` includes the package:

**setup.py**:
```python
packages=find_packages()
install_requires=[...]
```

**pyproject.toml**:
```toml
[project]
name = "ralph"
packages = [{include = "ralph"}]
```

### Testing the Fix

Before committing, verify pytest can collect tests without import errors:
```bash
pytest --collect-only
# Should show collected tests without ModuleNotFoundError
```

## Applied Example

Ralph Phase 1 fix:
- Added `src/__init__.py`
- Updated all test imports to use `from src.module import Thing`
- Avoided `ralph.src.*` pattern (requires package install)
- Tests collected cleanly after fix

## Related Skills

- [[07-Wiki/03-skills/testing-with-real-data|Testing with Real Data]]
- [[07-Wiki/03-skills/code-quality|Code Quality Standards]]
