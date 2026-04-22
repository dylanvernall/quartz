---
title: "Pre-Commit Hook Strategy and Optimization"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/git-workflow", "#domain/development"]
summary: "Unified strategy for pre-commit hook management: cascade issues, custom hook configuration, local optimization, documentation linting decision tree."
sources: ["memory/feedback_pre_commit_comprehensive_guide_2026_03_30.md"]
provenance:
  extracted: 0.95
  inferred: 0.05
  ambiguous: 0.0
---

# Pre-Commit Hook Strategy and Optimization

## Rule

Use four complementary patterns to manage git pre-commit hooks: (1) understand hook cascade issues, (2) verify custom hook invocation compatibility, (3) run formatters locally before staging, (4) use decision tree for documentation linting vs. production code.

## Why

Pre-commit hooks enforce code quality but can create friction: auto-fixes in unrelated files cause cascading retries, custom hooks may have argument mismatches, formatters need 2–3 iterations, and documentation linting rules conflict with planning documents. Without unified strategy, commits take 10+ minutes and require `--no-verify` workarounds.

## How to Apply

### Pattern 1: Hook Cascade Issues & Workarounds

**Problem**: Auto-fix hooks modify unrelated files, causing re-validation loops until all repo issues are fixed.

**Workarounds**:

1. **Single-file atomic commits** (most reliable):
   ```bash
   git add -- path/to/file.py
   git commit -m "message"  # Avoids cascading fixes
   ```

2. **Selective staging for task-specific work**:
   ```bash
   git add -- 99-System/02-Scripts/maintenance/session_end_cleanup.py
   git add -- .claude/settings.json
   git commit -m "feat(vault): Session end cleanup hook"
   ```
   Why: Large test files or generated artifacts trigger cascade failures on unrelated linting issues.

3. **Abort problematic staging**:
   ```bash
   git reset --hard HEAD  # Start over if cascades spiral
   ```

4. **Reduce hook scope**: Audit `.pre-commit-config.yaml` to exclude unnecessary files.

5. **Never use `--no-verify` blindly**: Always understand WHY the hook failed before bypassing it.

### Pattern 2: Custom Hook Configuration Verification

**Problem**: Custom hooks (like `link_decay_detector.py`) may expect different argument patterns than pre-commit provides.

**Verification**:
```bash
# Check what pre-commit will invoke
cat .pre-commit-config.yaml | grep -A 5 "link_decay_detector"

# Expected: hook accepts multiple positional args
# hook.py file1.md file2.md file3.md ✅

# Problem: hook expects --file flag
# hook.py --file file1.md ❌ (will fail with file2.md)
```

**Fix options**:
- Modify hooks to accept positional args: `argparse.add_argument('files', nargs='*')`
- Reconfigure `.pre-commit-config.yaml`
- Use `git commit --no-verify` for large commits with explicit awareness

### Pattern 3: Pre-Stage Local Formatting

**Problem**: Multi-iteration hook retries (line endings → black → isort = 2–3 minutes).

**Solution**: Run formatters locally BEFORE `git add`:

```bash
# Format all changed files
black .
isort .

# Verify output
git diff

# Stage and commit (should pass pre-commit cleanly)
git add .
git commit -m "message"
```

Or for specific files:

```bash
black 99-System/02-Scripts/my_script.py
isort 99-System/02-Scripts/my_script.py
git add 99-System/02-Scripts/my_script.py
git commit -m "message"
```

**Confidence**: 0.95 — Standard practice across Python projects. Pre-commit hooks are safety gates, not formatters.

### Pattern 4: Linting Strategy Decision Tree

**Problem**: Documentation files often have 100+ cosmetic violations (line length, table spacing, code-fence language) that don't affect content.

**Decision Tree**:

```
Committing files?
  ├─ Few files (< 5)
  │  └─ Run: black . && isort . && git add . && git commit
  │     (Local formatting prevents retries)
  │
  ├─ Many files (5+) with custom hooks
  │  └─ Check: hook invocation pattern in .pre-commit-config.yaml
  │     └─ Mismatch found?
  │        ├─ Yes → Use --no-verify OR single-file commits
  │        └─ No → Proceed with staged commit
  │
  └─ Documentation with 100+ cosmetic violations
     └─ Are violations cosmetic only? (line length, spacing, formatting)
        ├─ Yes → Use --no-verify (document in commit message)
        └─ No → Manual fix required (logic/security issues)
```

**Using `--no-verify` for Documentation**:

When violations are cosmetic and confined to documentation:

```bash
git commit --no-verify -m "Phase 3 results: narrative synthesis complete

[Implementation details...]

Note: Commit includes 7 planning documents with 200+ markdownlint violations
(MD013 line-length, MD060 table-spacing, MD040 code-fence language).
Violations are cosmetic only; manual fixing would require 40+ edit cycles.
Content reviewed and approved."
```

**Condition Checklist Before Using `--no-verify`**:
1. ✅ Documentation only (not production code)
2. ✅ Violations are cosmetic (not logic/security)
3. ✅ Manual fix cost > 15 minutes
4. ✅ Document decision in commit message

**Alternative**: Update `.markdownlint.yaml` to exclude planning docs:
```yaml
MD013:
  exclude: |
    01-Projects/*/PHASE-*.md
    01-Projects/*/planning-*.md
```

## Applied

- 2026-03-30: Consolidated from 4 separate feedback patterns
- Cascade issues: Single-file commits reduced retry loops by 90%
- Custom hooks: Verified invocation patterns before large commits
- Local formatting: Pre-stage optimization eliminated 2–3 iteration cycles
- Documentation: Decision tree clarified when --no-verify is appropriate vs. required fixes
- Result: Average commit time reduced from 10+ min to 2–3 min

## Related Skills

- [[07-Wiki/03-skills/memory-file-exclusion|Memory File Linting Exclusion]]
- [[07-Wiki/03-skills/code-quality|Code Quality Standards]]
- [[07-Wiki/03-skills/tracked-changes-markup-pattern|Tracked Changes Markup Pattern]]
