---
title: "Vault Automation and Cleanup Patterns"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/vault-maintenance", "#domain/vault"]
summary: "Vault automation patterns: tech debt audit discovery, three-tier cleanup, log file management, pre-commit hook integration."
sources: ["memory/feedback_vault_tech_debt_audit_pattern.md", "memory/feedback_vault_log_cleanup.md"]
provenance:
  extracted: 0.95
  inferred: 0.05
  ambiguous: 0.0
---

# Vault Automation and Cleanup Patterns

## Rule

Use vault automation in two phases: (1) scope discovery with explore agents, (2) three-priority cleanup (root cleanup, config audit, frontmatter sweep). Manage generated logs with `.gitignore` to prevent pre-commit blocking.

## Why

Large vaults (~2000 notes) accumulate fragmented debt: stray files, orphaned scripts, missing metadata, broken links. Trying to fix all categories simultaneously causes scope creep. Explore agents + three-tier prioritization allows progressive improvement. Vault automation tools generate large reports that block commits unless properly managed.

## How to Apply

### Phase 1: Discovery with Explore Agents (~15 min)

Before committing to fixes, use explore agents to survey scope.

**Actions**:
1. Explore agent: "Find all stray files at vault root (*.py, *.json, *.log, *.txt, media) and categorize by project"
2. Explore agent: "Find all orphaned notes with 0 inbound links and categorize by folder"
3. Explore agent: "Find all broken wikilinks and count by folder"
4. Compile findings into scope decision: What is audit scope? What is out-of-scope?

**Success metric**: Clear list of P1/P2/P3 candidates with counts. Example: "73 stray files at root, 312 orphaned notes, 528 broken links."

### Priority 1: Root Cleanup & Duplicates (30–45 min)

Target stray files at vault root and script duplicates.

**Actions**:
1. Identify misplaced files (files at `c:\Vault-Lite\*.py` that should be in `01-Projects/` or `99-System/`)
2. Identify script versions (`script.py` vs `script_enhanced.py`)
3. For each pair: read both, determine which is current, delete superseded version
4. Move root scripts to appropriate project folder (check git history)
5. Commit: `fix: vault root cleanup and script consolidation`

**Success metric**: < 5 stray files at root; no duplicate pairs.

**Typical findings**: Stray scripts belong to PICO/lit-review projects, dependency files, checkpoint JSONs from old pipelines.

### Priority 2: Config & Automation Audit (30 min)

Target stale `.claude/` configs, outdated databases, orphaned pipeline scripts.

**Actions**:
1. Audit `.claude/mcp-config-*.json` backups (delete old, keep current)
2. Check SQLite databases in `.claude/` (identify actively used via grep)
3. Scan `99-System/02-Scripts/` for abandoned "phase" pipelines
4. Move phase scripts to archive or relocate if part of ongoing project
5. Commit: `fix: vault config cleanup and db pruning`

**Success metric**: No old backups; only active databases; no orphaned phase scripts.

### Priority 3: Frontmatter Sweep (20 min)

Target files missing YAML frontmatter.

**Actions**:
1. Use `/vault-automation health` to identify files missing frontmatter
2. For each file: add minimal frontmatter (title, created, modified, type, retention, status, tags)
3. Use file creation date from git log for `created`; use today for `modified`
4. Commit: `fix: add frontmatter to [category] files`

**Success metric**: All files have frontmatter; `/vault-automation health` shows 0 issues.

### Bonus: MOC Creation (High ROI, Optional)

If orphaned notes remain after P1–P3, create missing MOCs (80%+ orphan reduction).

**Actions**:
1. Identify largest orphan clusters by folder (e.g., `01-Projects/02-03-Research/Papers/`)
2. Create folder-level MOC summarizing contents and relationships
3. Add wikilinks in MOC to all notes in folder
4. Commit: `docs: Add MOC to [folder] cluster`

### Phase 2: Log File Management

Vault automation tools generate large JSON/markdown reports that exceed pre-commit size limits.

**Strategy**: Add automation logs to `.gitignore` to prevent blocking:

```
99-System/10-Logs/reports/
```

Or: Create cleanup task in Phase 1 that removes reports older than 24 hours:

```bash
find 99-System/10-Logs/reports -name "*.json" -mtime +1 -delete
```

**Rule**: Keep recent reports (< 24h) for debugging, but don't commit them to git.

## Expected Recovery Metrics

Example from comprehensive vault recovery (2026-04-02):

- **Before**: 2,741 broken links (81% reduction target), 936 orphans (82% reduction target), 54% YAML compliance
- **After**: 528 broken links, 164 orphans, 95%+ YAML compliance
- **Timeline**: 8 phases over 2–3 sessions
- **Highest-impact**: MOC creation (reduced orphans from 280 → 64 in one phase)

## Applied

- 2026-04-14: Vault audit P1–P3 complete; 80% orphan reduction via MOC creation
- Ongoing: Root cleanup maintains < 5 stray files; health checks via `/vault-automation health`
- Result: 2214 files, 96.9% valid frontmatter, 0 broken wikilinks

## Related Skills

- [[07-Wiki/03-skills/vault-maintenance|Vault Maintenance Workflows]]
- [[07-Wiki/03-skills/vault-structure|Vault Structure and Organization]]
- [[07-Wiki/03-skills/vault-log-cleanup-automation|Vault Log Cleanup Automation]]
