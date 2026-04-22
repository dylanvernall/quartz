---
title: "Configuration Consolidation Pattern"
created: 2026-04-14T15:46:00+12:00
modified: 2026-04-14T15:46:00+12:00
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/configuration", "#topic/maintenance"]
sources: ["~/.claude/projects/c--Vault-Lite/memory/feedback_configuration_consolidation.md"]
summary: "Reduce settings files 70%+ by consolidating similar permission patterns instead of individual entries."
provenance: "extracted: 1.0"
---

## Rule: Use Pattern-Based Rules Instead of Individual Entries

**Why:** Reduces file bloat and maintenance burden. Applied to settings.local.json: reduced from 172 → 49 lines (71% reduction) while maintaining full functionality.

**How to apply:**

### 1. Group Similar Permission Patterns

Group by tool + prefix (e.g., all `python` variants together).

### 2. Look for Wildcard Opportunities

```
❌ Bad (individual entries):
- Bash(python:*) ✓
- Bash(python3:*) ✓
- Bash(python -m pytest:*) ✓
- Bash(python -m flake8:*) ✓

✓ Good (consolidated pattern):
- Bash(python*) ✓  (matches all variants with single pattern)
```

### 3. Apply to Common Groups

- **Git subcommands**: `Bash(git:*)` instead of listing each separately
- **Python tools**: `python*` catches `python`, `python3`, `python -m <tool>`
- **Web domains**: Use wildcards for subdomains (e.g., `*.api.example.com`)

### 4. Document Consolidation

Record date, what was merged, and lines saved for future reference.

## Result

Cleaner, more maintainable configuration files with fewer individual entries to review and update.
