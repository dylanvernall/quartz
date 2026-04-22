---
title: "Memory System Alignment"
created: 2026-04-14T10:05:00Z
modified: 2026-04-14T10:05:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/memory-management", "#topic/session-wrap-up", "#domain/vault"]
summary: "Route learnings to correct typed memory categories (feedback, project, reference, user) via session-wrap-up skill v3.0.0+."
sources: ["memory/feedback_memory_system_alignment.md"]
provenance:
  extracted: 0.95
  inferred: 0.05
  ambiguous: 0.0
---

# Memory System Alignment

## Rule

The session-wrap-up skill (v3.0.0) explicitly routes learnings to the correct typed memory system:

- **feedback** type → corrections, workflow preferences, workflow anti-patterns
- **project** type → active project status, decisions, next steps
- **reference** type → external system pointers (Linear boards, dashboards, docs)
- **user** type → user characteristics, domain expertise, preferences
- **CLAUDE.md** → permanent project-wide rules ONLY (encoding, link format, quality standards)
- **CLAUDE.local.md** → ephemeral next-session context (regenerated each session)

## Why

The skill was previously centred on SimpleMem (`/memory-compress`, `99-System/03-Data/memory/simplemem/`), which is aspirational/non-functional. The actual working system is auto-memory at `~/.claude/projects/c--Vault-Lite/memory/` with typed markdown files. The mismatch meant:

- Feedback/corrections weren't being saved to the typed memory system → learnings weren't recalled in future conversations
- MEMORY.md grew to 399 lines (limit: 200) with no pruning steps
- SimpleMem references were misleading

## How to Apply

When using `/wrap-up`:

1. **Phase 0**: Check memory health (MEMORY.md line count)
2. **Phase 2**: Route learnings to correct typed memory type using the routing table in the skill
3. **Phase 3**: Use CLAUDE.md decision gate — permanent rules → CLAUDE.md, session-specific → feedback memory
4. **Phase 2 best practices**: Check for existing memory files before creating duplicates; keep MEMORY.md < 150 lines

**Key difference**: If you discover a correction or workflow pattern (e.g., "avoid shell wildcards without quoting"), save it as a `feedback` type memory, not CLAUDE.md. This ensures it's recalled in future sessions where similar patterns recur.

## Related Skills

- [[07-Wiki/03-skills/memory-consolidation-pattern|Memory Consolidation Pattern]]
- [[07-Wiki/03-skills/vault-automation|Vault Maintenance]]
