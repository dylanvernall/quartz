---
title: "Vault Dead Weight Cleanup"
created: 2026-04-20T00:00:00Z
modified: 2026-04-20T00:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/vault-maintenance", "#domain/vault"]
summary: "Quarterly cleanup pattern for machine-generated caches, embeddings, and logs — 1.95 GB freed in 2026-04-16 run."
sources: ["memory/project_vault_cleanup_2026_04_16.md"]
provenance:
  extracted: 0.9
  inferred: 0.1
  ambiguous: 0.0
---

# Vault Dead Weight Cleanup

## What to Remove

### Safe Tier (remove freely — all regenerable)
- Smart Connections embeddings: `*.ajson` files (~1.6 GB) — Obsidian rebuilds on launch (~5 min)
- Python bytecode: `__pycache__/` directories — regenerates on import
- Pytest caches: `.pytest_cache/` — regenerates on test run
- Runtime locks: `.claude/scheduled_tasks.lock`

### Moderate Tier (confirm before removing)
- Build outputs: `dist/` and `build/` directories (check active builds first)
- Run logs: accumulated `.log` files >24h old (check `.gitignore` coverage)
- Vector indexes: `faiss.index`, `embeddings.npy` (regenerable via `99-System/03-Retrieval-Engine/`)
- `.bak` temp files and `Thumbs.db`

### Worktree Duplicates
- `.claude/worktrees/` copies of vector indexes and `.bak` files — these are always safe to remove

## When to Run

Run quarterly or after:
- Large Python refactors (new `__pycache__` bloat)
- Extended testing sessions (pytest cache accumulation)
- Long build cycles (`dist/build` artifacts)
- Obsidian becomes noticeably slower (Smart Connections re-indexing noise)

## Typical Impact

2026-04-16 run results:
- Items removed: 10,526 safe tier + 96 moderate tier
- Space freed: ~1.95 GB (~22% vault footprint)
- Vault footprint: 8.3 GB → ~6.35 GB
- Side effect: Obsidian Smart Connections re-indexes on next launch (~5 min overhead)

## Skill Reference

`/vault-dead-weight` — invoke via `.claude/skills/vault-dead-weight/SKILL.md`

## Related

- [[07-Wiki/03-skills/vault-maintenance.md|Vault Maintenance]] — broader maintenance workflow
- [[07-Wiki/03-skills/vault-log-cleanup-automation.md|Vault Log Cleanup Automation]] — automated log management
