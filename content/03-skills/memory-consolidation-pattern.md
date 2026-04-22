---
title: "Memory Consolidation Pattern"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/memory-management", "#domain/vault"]
summary: "Four-phase maintenance workflow for memory system — delete superseded, merge overlapping, fill gaps, reformat index."
sources: ["memory/feedback_memory_consolidation_pattern.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Memory Consolidation Pattern

## Rule

**Run memory consolidation when file count > 35 or MEMORY.md > 150 lines. Workflow: delete superseded → merge overlapping → fill gaps → reformat index.**

## Why

- **Signal quality**: Memory files accumulate fast. Superseded project snapshots crowd out actionable guidance.
- **Index function**: MEMORY.md grows verbose and loses its utility as a quick reference.
- **Consistency**: Duplicate content causes inconsistency when both versions exist.

## How to Apply

### Phase 1 — Delete Superseded Files

Identify and delete files that have been completely replaced by newer versions.

- **Early project snapshots**: Phase 1-3 notes → delete if complete replacement exists
- **Stale lockfiles**: `.consolidate-lock`, etc. → delete immediately
- **Technical references**: Content fully captured in a feedback file → merge then delete

**Example**: `project_ralph_refactor_2026_03_20.md` (Phase 1-3 snapshot) is superseded by `project_ralph_fastapi_refactor_complete.md` (full 6-phase completion) → delete.

### Phase 2 — Merge Overlapping Content

Identify reference files with detail not captured in feedback versions. Append unique content, then delete the reference.

**Example**: `slr_pipeline_code_review.md` contains a 9-issue breakdown table + action plan not in feedback version → append to `feedback_slr_pipeline_code_review.md`, then delete original.

**What to preserve**: Issue tables, action plan paths, precision breakdowns.

### Phase 3 — Fill Index Gaps

List all memory files and cross-check against MEMORY.md line-by-line. For each unindexed file, decide: "Worth indexing for future sessions?"

**Add to index**: Yes → one-line pointer to MEMORY.md
**Skip**: Completed sub-tasks with no future action, ad-hoc analysis notes derivable from code.

**Example**: `feedback_agent_team_patterns.md` is unindexed but contains reusable multi-agent patterns → add to feedback section.

### Phase 4 — Reformat MEMORY.md

Convert MEMORY.md from paragraph format to compact index format.

**Target format**:
```markdown
- [Title](file.md) — one-line hook (<150 chars)
```

**Actions**:
1. Convert all entries from `### Title` + paragraph to single-line bullet with file link
2. Move paragraph-level detail from MEMORY.md into the topic files themselves
3. Remove markers from entries older than ~1 week
4. Compress verbose entries: if an index line exceeds 150 chars, move detail to the topic file
5. Target: < 150 lines total

**Validation example**: 2026-03-26 consolidation reduced memory dir from 40 → 36 files; MEMORY.md from 113 lines (paragraph format) to 55 lines (index format).

### Edge Cases

**Skip consolidation if**:
- Memory dir < 30 files AND MEMORY.md < 100 lines — not urgent
- Consolidation cost > benefit (rewriting 20+ entries vs saving 50 lines) — defer

**Prioritize deletion**:
- Stale lockfiles and obvious cruft — low cost, high signal improvement
- Superseded project snapshots WITH complete replacements — high confidence
- Skip early snapshots WITH NO replacement — they may still be referenced

**Always preserve**:
- Feedback files — behavioral guidance has long shelf life
- Active project files — even if incomplete (context matters)
- Reference material with unique detail not elsewhere — keep if no duplication

## Applied

- 2026-03-26: Reduced memory dir 40 → 36 files; MEMORY.md 113 → 55 lines
- 2026-04-14: Consolidated 27 completed project snapshots, kept 5 active + 30 feedback files
- Current: 81 active memory files, MEMORY.md 122 lines (healthy index)

## Related Skills

- [[07-Wiki/03-skills/memory-system-management|Memory System Management]]
- [[07-Wiki/03-skills/memory-system-alignment|Memory System Alignment]]
