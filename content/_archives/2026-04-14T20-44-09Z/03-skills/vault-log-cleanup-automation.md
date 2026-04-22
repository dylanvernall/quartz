---
title: "Vault Log Cleanup Automation"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: seasonal
status: active
tags: ["#type/skill", "#topic/vault-maintenance", "#topic/automation"]
summary: "Add vault automation report directories to .gitignore to prevent pre-commit hook blocking. Logs from link_decay_detector and vault_map can exceed 1 MB; clean logs >24h old automatically."
sources: ["memory/feedback_vault_log_cleanup.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Vault Log Cleanup Automation

## Rule: Exclude Large Automation Logs from Git

Vault automation tools generate large report files that exceed pre-commit size limits. Add them to `.gitignore` and implement automated cleanup for older reports.

**Why**: Vault automation tools (link_decay_detector, vault_map) generate large JSON/markdown report files exceeding 1 MB, which triggers pre-commit hook blocking. Without cleanup strategy, commits fail and require manual file removal each session.

## How to Apply

### Option 1: Exclude from Git (Simple)

Add to `.gitignore`:
```
99-System/10-Logs/reports/
99-System/10-Logs/lit-review/
```

This prevents automation-generated reports from being tracked entirely.

### Option 2: Keep Recent Reports, Clean Old Ones (Recommended)

Create automated cleanup task in Phase 1 pre-flight check:
```bash
# Keep reports < 24h, remove older reports
find 99-System/10-Logs/reports -name "*.json" -mtime +1 -delete
find 99-System/10-Logs/lit-review -name "*.json" -mtime +1 -delete
```

**Benefits**:
- Recent reports available for debugging
- Old reports don't clutter vault or block commits
- Automated, requires no manual intervention

### Configuration

Add to session initialization or pre-commit hook:
```bash
# Remove automation reports older than 24 hours
find 99-System/10-Logs/reports -type f -mtime +1 -delete 2>/dev/null || true
find 99-System/10-Logs/lit-review -type f -mtime +1 -delete 2>/dev/null || true
```

## Real-World Incident

Session 2026-03-19:
- link_decay_detector produced `link_decay_20260319_174951.json` (1.9 MB)
- Pre-commit hook blocked commit with file size violation
- Manual deletion required before proceeding
- Fixed by adding folder to `.gitignore`

## Related Skills

- [[07-Wiki/03-skills/vault-structure|Vault Structure & Organisation]]
- [[07-Wiki/03-skills/memory-consolidation|Memory Consolidation]]
