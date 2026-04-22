---
title: "Memory System Alignment"
created: 2026-04-14T15:30:00+12:00
modified: 2026-04-14T15:30:00+12:00
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/memory-management", "#topic/system-design"]
sources: ["~/.claude/projects/C--Vault-Lite/memory/feedback_memory_system_alignment.md"]
summary: "Route learnings to correct typed memory system: feedback, project, reference, user types have specific purposes and destinations."
provenance: "extracted: 1.0"
---

## The System

Session learnings should route to correct typed memory:

| Memory Type | Purpose | Example |
|---|---|---|
| **feedback** | Corrections, workflow preferences, anti-patterns | "Don't mock external data sources" |
| **project** | Active project status, decisions, next steps | "FastAPI migration complete; test baseline: 160 passing" |
| **reference** | External system pointers | "Linear board: INGEST; Grafana: api-latency dashboard" |
| **user** | User characteristics, domain expertise, preferences | "Data scientist, new to React frontend" |

## Why Typed Memory Matters

The old SimpleMem system was aspirational but non-functional. The actual working system is auto-memory at `~/.claude/projects/<project>/memory/` with typed markdown files. The mismatch meant:
- Feedback/corrections weren't being saved → learnings weren't recalled in future conversations
- MEMORY.md grew unbounded with no pruning
- SimpleMem references were misleading

## How to Apply

**When using `/wrap-up` skill:**

1. **Check memory health** — MEMORY.md line count
2. **Route learnings** to correct typed memory type using the routing table
3. **Use decision gate** — permanent rules → CLAUDE.md, session-specific → feedback memory
4. **Keep MEMORY.md <150 lines** — check for duplicates before creating new memory files

## Key Rule

If you discover a correction or workflow pattern (e.g., "avoid shell wildcards without quoting"), save it as a **feedback** type memory, not CLAUDE.md. This ensures it's recalled in future sessions.

---

## Related

- [[07-Wiki/03-skills/memory-consolidation-workflow.md|Memory Consolidation Workflow]] — maintenance pattern
- [[07-Wiki/03-skills/dream-consolidation-checklist.md|Dream Consolidation Checklist]] — regular review
