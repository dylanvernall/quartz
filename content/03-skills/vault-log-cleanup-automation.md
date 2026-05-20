---
title: "Vault Log Cleanup Automation"
created: 2026-04-14T15:30:00+12:00
modified: 2026-04-14T15:30:00+12:00
type: skill
retention: seasonal
status: active
tags: ["#type/skill", "#topic/vault-maintenance", "#topic/automation"]
sources: ["~/.claude/projects/C--Vault-Lite/memory/feedback_vault_log_cleanup.md"]
summary: "Add vault automation logs to .gitignore to prevent pre-commit blocking; or implement cleanup task for reports older than 24 hours."
provenance: "extracted: 1.0"
---

## The Problem

Vault automation tools (link_decay_detector, vault_map) generate large JSON/markdown report files (>1 MB) that exceed pre-commit size limits. This blocks commits and requires manual file removal each session.

## Solution 1: Add to .gitignore (Recommended)

Add folders to `.gitignore` to prevent pre-commit validation:

```
99-System/10-Logs/reports/
```

**Rationale**: Automation reports are ephemeral — useful for debugging in-session but shouldn't be committed.

## Solution 2: Automated Cleanup Task

Create Phase 1 task that removes reports older than 24 hours:

```bash
find 99-System/10-Logs/reports -name "*.json" -mtime +1 -delete
```

Keep recent reports (< 24h) for debugging, delete older ones before commit.

## Real Example

2026-03-19 session:
- link_decay_detector produced link_decay_20260319_174951.json (1.9 MB)
- Pre-commit hook blocked commit
- Required manual deletion
- **Fixed by** adding folder to .gitignore

## Principle

**Generate freely, clean up automatically** — debugging reports are valuable during work, but don't need to persist in git history.

---

## Related

- [[07-Wiki/03-skills/memory-consolidation-workflow.md|Memory Consolidation Workflow]] — general cleanup pattern
