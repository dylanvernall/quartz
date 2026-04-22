---
title: "Vault Maintenance Workflows"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: seasonal
status: active
tags: ["#type/skill", "#topic/vault-maintenance", "#domain/vault"]
summary: "Three-priority audit pattern (root cleanup, config audit, frontmatter sweep) with MOC creation bonus."
sources: ["memory/feedback_vault_tech_debt_audit_pattern.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Vault Maintenance Workflows

## Rule

**Use three sequential priorities to audit vault tech debt: P1 root cleanup, P2 config audit, P3 frontmatter sweep. Begin with scope discovery (explore agents), execute tiers, measure recovery.**

## Why

- **Scope discipline**: Large vaults (~2000 notes) accumulate fragmented debt (stray files, orphans, broken links). Fixing all categories simultaneously causes creep.
- **Progressive improvement**: Three-tier prioritization allows systematic reduction with clear decision gates.
- **High ROI**: MOC creation (when done) reduces downstream orphans by 80%+.

## How to Apply

### Discovery Phase (15 min)

Use explore agents to survey landscape BEFORE committing to fixes.

**Actions**:
1. Explore agent: "Find all stray files at vault root (*.py, *.json, *.log, *.txt, media) and categorize by project"
2. Explore agent: "Find all orphaned notes with 0 inbound links and categorize by folder"
3. Explore agent: "Find all broken wikilinks and count by folder"
4. Compile findings: Clear list of P1/P2/P3 candidates with counts

**Success metric**: Example output — "73 stray files at root, 312 orphaned notes, 528 broken links."

### Priority 1: Root Cleanup & Duplicates (30–45 min)

Target stray files at vault root and script duplicates.

**Actions**:
1. Identify misplaced files (files at `c:\Vault-Lite\*.py` that should be in 01-Projects/ or 99-System/)
2. Identify script versions (`script.py` vs `script_enhanced.py` pairs)
3. For each pair: read both, determine which is current, delete superseded version
4. Move root scripts to appropriate project folder (check git history or context)
5. Commit: `fix: vault root cleanup and script consolidation`

**Success metric**: < 5 stray files remaining at root; no duplicate script pairs.

**Typical findings**: Stray root scripts belong to PICO/lit-review projects (moved to 01-Projects/02-02-AI-Research/), dependency files, checkpoint JSONs from old pipelines.

### Priority 2: Config & Automation Audit (30 min)

Target stale `.claude/` configurations, outdated database files, orphaned pipeline scripts.

**Actions**:
1. Audit `.claude/mcp-config-*.json` backups — delete old, keep current
2. Check SQLite databases in `.claude/` — identify actively used via grep across scripts
3. Scan `99-System/02-Scripts/` for abandoned "phase" pipelines (`execute_phase2_step1.py`, etc.)
4. Move phase scripts to archive or relocate if part of ongoing project
5. Commit: `fix: vault config cleanup and db pruning`

**Success metric**: No old backups; only active databases; no orphaned phase scripts.

### Priority 3: Frontmatter Sweep (20 min)

Target files missing YAML frontmatter.

**Actions**:
1. Use `/vault-automation health` to identify missing frontmatter files
2. For each file: add minimal frontmatter (title, created, modified, type, retention, status, tags)
3. Use file creation date from git log for `created`; use today for `modified`
4. Commit: `fix: add frontmatter to [category] files`

**Success metric**: All files have frontmatter; `/vault-automation health` shows 0 issues.

### Bonus: MOC Creation (High ROI, Optional)

If orphaned notes remain after P1–P3, create missing MOCs for large folders (80%+ orphan reduction).

**Actions**:
1. Identify largest orphan clusters by folder (e.g., `01-Projects/02-03-Research/Papers/`)
2. Create folder-level MOC summarizing contents, key relationships, discovery paths
3. Add wikilinks in MOC to all notes in folder
4. Commit: `docs: Add MOC to [folder] cluster` (separates MOC creation from cleanup)

## Applied

- 2026-04-14: Vault audit P1–P3 complete; 80% orphan reduction via MOC creation
- Ongoing: Root cleanup maintains < 5 stray files; frontmatter checks via `/vault-automation health`
- Result: 2214 files, 96.9% valid frontmatter, 0 broken wikilinks

## Related Skills

- [[07-Wiki/03-skills/vault-structure|Vault Structure and Organization]]
- [[07-Wiki/03-skills/vault-automation|Vault Automation Patterns]]
- [[07-Wiki/03-skills/vault-log-cleanup-automation|Vault Log Cleanup Automation]]
