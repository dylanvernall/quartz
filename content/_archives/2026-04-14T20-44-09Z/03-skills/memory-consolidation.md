---
title: "Memory Consolidation Pattern"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/memory-management", "#topic/maintenance", "#domain/vault"]
summary: "Run memory consolidation when file count grows (>35 files) or MEMORY.md approaches 150 lines — delete superseded, merge overlapping, fill gaps."
sources: ["memory/feedback_memory_consolidation_pattern.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Memory Consolidation Pattern

## Rule

Run memory consolidation when:
- Memory file count grows beyond 35 files
- MEMORY.md approaches or exceeds 150 lines

Workflow: delete superseded → merge overlapping → fill gaps → reformat index.

## Why

Memory files accumulate quickly. Superseded project snapshots crowd out signal; MEMORY.md grows verbose and loses index function; duplicate content causes inconsistency. Regular consolidation keeps the system healthy and navigable.

## How to Apply

### Phase 1 — Delete Superseded Files

- Early project snapshots (Phase 1–3 notes) superseded by completion summaries → delete
- Stale lock files (`.consolidate-lock`, etc.) → delete
- Technical reference files whose content is fully captured in feedback files → merge then delete

**Example**: `project_ralph_refactor_2026_03_20.md` (Phase 1–3 snapshot) superseded by `project_ralph_fastapi_refactor_complete.md` (full 6-phase completion) → delete snapshot.

### Phase 2 — Merge Overlapping Content Before Deleting

- Identify reference files with detail not in feedback versions
- Append unique content (issue tables, action plan paths, precision breakdowns) to the feedback file
- Then delete the reference file

**Example**: `slr_pipeline_code_review.md` (9-issue breakdown table + action plan path) merged into `feedback_slr_pipeline_code_review.md`, then deleted.

### Phase 3 — Fill Index Gaps

- List all memory files; cross-check against MEMORY.md line-by-line
- For each unindexed file: decide "worth indexing for future sessions?"
- Add: yes → one-line pointer to MEMORY.md
- Skip: completed sub-tasks with no future action, ad-hoc analysis notes derivable from code

**Example**: `feedback_agent_team_patterns.md` was unindexed but contains reusable patterns for multi-agent orchestration → added to feedback section.

### Phase 4 — Reformat MEMORY.md to Spec

**Target format**:
```
- [Title](file.md) — one-line hook (<150 chars)
```

**Actions**:
1. Convert all entries from `### Title` + paragraph to single-line bullet with file link
2. Move all paragraph-level detail from MEMORY.md into the topic files themselves
3. Remove "⭐ NEW" markers from entries older than ~1 week
4. Compress verbose entries: if an index line exceeds 150 chars, detail belongs in the topic file
5. **Target**: Under 60–100 lines total

**Validation**: 2026-03-26 consolidation reduced memory dir from 40 → 36 files; MEMORY.md from 113-line paragraph format to ~55-line index format.

## Edge Cases

### When to Skip Consolidation

- Memory dir < 30 files and MEMORY.md < 100 lines — not urgent
- Consolidation cost (rewriting 20+ entries) > benefit (saving 50 lines) — defer

### When to Prioritise Deletion

- Stale lock files and obvious cruft — low cost, high signal-to-noise improvement
- Superseded project snapshots with complete replacements — high confidence
- **Skip** early snapshots with NO complete replacement (they may still be referenced)

### When to Preserve

- **Feedback files** — always keep (behavioural guidance has long shelf life)
- **Active project files** — even if incomplete (context matters)
- **Reference material** with unique detail not elsewhere — keep if no duplication

## Related Skills

- [[07-Wiki/03-skills/memory-system-alignment|Memory System Alignment]]
- [[07-Wiki/03-skills/vault-maintenance|Vault Maintenance]]
