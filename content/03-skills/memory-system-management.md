---
title: "Memory System Management"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/memory-management", "#domain/vault"]
summary: "Typed memory system with routing (feedback, project, reference, user) and session wrap-up integration."
sources: ["memory/feedback_memory_system_alignment.md", "memory/feedback_dream_consolidation_workflow.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Memory System Management

## Rule

**Route learnings to typed memory: feedback (corrections, workflows), project (status, decisions), reference (external systems), user (characteristics). Use CLAUDE.md for permanent rules only; CLAUDE.local.md for ephemeral next-session context.**

## Why

- **Recall**: Typed memory is automatically loaded in future sessions. Without typing, learnings are lost.
- **Signal**: Routing prevents CLAUDE.md bloat (permanent rules only) and MEMORY.md confusion (index not content).
- **Consistency**: Explicit routing prevents duplicates and misalignment between memory types.

## How to Apply

### Memory Typing

Five memory types, each with distinct location and lifecycle:

| Type | Use | Location | Lifecycle | Recall |
|------|-----|----------|-----------|--------|
| **feedback** | Workflow corrections, patterns, preferences | `.claude/memory/feedback_*.md` | Session-agnostic, long lifespan | Automatic, every session |
| **project** | Active project status, decisions, blockers | `.claude/memory/project_*.md` | During project, archive on completion | Automatic when relevant |
| **reference** | External system pointers (dashboards, boards) | `.claude/memory/reference_*.md` | Long-term reference | On-demand reference |
| **user** | User characteristics, domain expertise, role | `.claude/memory/user_*.md` | Persistent across projects | Automatic, every session |
| **CLAUDE.md** | Permanent rules, standards, encoding | In project root | Permanent, checked in to git | Automatic, per project |

### Routing Decision Table

| Finding | Type | Example |
|---------|------|---------|
| "User corrected my approach — avoid X, do Y instead" | feedback | `feedback_confirm_before_completing.md` |
| "Current project status is X; blockers are Y; next: Z" | project | `project_met_pipeline_2026_04_01.md` |
| "User's Linear board is at [URL]" | reference | `reference_linear_board_ingest.md` |
| "User is a data scientist with 10 years Go experience" | user | `user_role_and_expertise.md` |
| "All .md files must have frontmatter" | CLAUDE.md | Permanent rule, project-wide |

### Session Wrap-Up Integration

Use `/session-wrap-up` skill (v3.0.0+) to route learnings automatically.

**Workflow**:
1. **Phase 0**: Check memory health (MEMORY.md line count)
2. **Phase 2**: Route learnings using the routing table above
3. **Phase 3**: Decision gate — permanent → CLAUDE.md, session-specific → feedback memory
4. **Best practice**: Check for existing memory files before creating duplicates; keep MEMORY.md < 150 lines

### Example: Saving a Correction

**Session scenario**: User says "Stop auto-completing scope, ask clarifying questions instead."

**Correct routing**:
```markdown
---
name: Confirm ambiguous requests before auto-completing
type: feedback
---

Rule: When user asks to "continue" or "add to" incomplete instructions,
ask what comes next rather than inferring.

Why: Auto-completing wastes effort and requires rework.

How to apply: If request is ambiguous (e.g., "continue from X" without
specifying X continues to), pause and ask before generating content.
```

Save as: `.claude/projects/c--Vault-Lite/memory/feedback_confirm_before_completing.md`

Add to MEMORY.md:
```
- [Confirm before auto-completing](feedback_confirm_before_completing.md) — ask clarifying questions when scope is ambiguous
```

### CLAUDE.md vs CLAUDE.local.md

**CLAUDE.md** (permanent, checked in):
- Encoding standards (ASCII only, no emojis)
- Wikilink formats (absolute paths, MOC suffix)
- Code quality targets (complexity < 7, CC / TDD)
- File structure and retention tiers
- Commit message format

**CLAUDE.local.md** (ephemeral, .gitignored):
- Current session date and objective
- Completed work (with commit hashes)
- Key decisions made THIS SESSION
- Blockers and open questions
- Regenerated at end of each session

## Applied

- /session-wrap-up skill: 4-phase typing workflow (2026-04-08+)
- Memory system: 81 active typed files (feedback/project/reference/user)
- MEMORY.md: 122 lines, <150 target (healthy index)

## Related Skills

- [[07-Wiki/03-skills/memory-consolidation-pattern|Memory Consolidation Pattern]]
- [[07-Wiki/03-skills/memory-system-alignment|Memory System Alignment]]
