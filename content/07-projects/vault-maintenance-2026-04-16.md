---
title: "Vault Maintenance — 2026-04-16"
created: 2026-04-16T00:00:00Z
modified: 2026-04-20T00:00:00Z
type: completion-report
retention: seasonal
status: completed
tags: ["#type/project", "#domain/vault", "#topic/maintenance"]
summary: "Comprehensive 6-phase vault cleanup: 10,526 safe-tier deletions (1.95 GB freed), 46% file reduction (4,278→2,308 files), 0 broken links post-cleanup."
---

# Vault Maintenance — 2026-04-16

## Overview

**Date**: 2026-04-16  
**Status**: Completed  
**Total freed**: ~1.95 GB (~22% vault footprint reduction)  
**File count**: 4,278 → 2,308 files (46% reduction)  
**Broken links post-cleanup**: 0

## Summary

Executed comprehensive vault cleanup across safe and moderate tiers, removing machine-generated caches, embeddings, and accumulated logs. Total of 10,622 items removed.

### Safe Tier (10,526 items, all regenerable)

- **Smart Connections embeddings**: 10,408 `.ajson` files (1.6 GB) — Obsidian rebuilds on next launch (~5 min)
- **Python bytecode**: 107 `__pycache__` directories (3 MB) — regenerates on import
- **Pytest caches**: 10 `.pytest_cache/` directories (291 KB) — regenerates on test run
- **Runtime lock**: 1 `.claude/scheduled_tasks.lock` file

### Moderate Tier (96 items, checked before removal)

- **Build outputs**: 5 `dist/` and `build/` directories (179 MB; dominated by time-tracker-rebuilt)
- **Run logs**: 82 accumulated log files (169 MB; Feb 2026 onwards)
- **Vector indexes**: 6 files (2.2 MB; faiss.index + embeddings.npy) — regenerable via `99-System/03-Retrieval-Engine/`
- **Temp files**: 3 `.bak` files + Thumbs.db (negligible)

## Key Decisions

- **Worktree cleanup**: Removed 2–3× copies of vector indexes and .bak files from `.claude/worktrees/` — all safely duplicated
- **Content preservation**: All `.md` content under `01-Projects/`, `02-Areas/`, `03-Resources/` untouched
- **Obsidian side effect**: Smart Connections re-index on next launch (~5 min startup overhead, then clears)

## Vault Health Post-Cleanup

- **Footprint**: 8.3 GB → ~6.35 GB (estimated)
- **Search performance**: Faster Glob/Grep (less noise in directory tree)
- **Backup size**: ~2 GB smaller
- **Obsidian startup**: Cleaner (Smart Connections no longer indexing node_modules content)

## When to Run Again

Run quarterly or after:
- Large Python refactors (new `__pycache__` bloat)
- Extended testing sessions (pytest cache accumulation)
- Long-running build cycles (`dist/` and `build/` artifacts)
- When Obsidian noticeably slower (Smart Connections re-indexing noise)

## Related

- [[07-Wiki/03-skills/vault-dead-weight-cleanup.md|Vault Dead Weight Cleanup]] — skill for quarterly cleanup
- [[07-Wiki/03-skills/vault-maintenance.md|Vault Maintenance]]
