---
title: "Memory Consolidation Workflow"
created: 2026-04-14T15:30:00+12:00
modified: 2026-04-14T15:30:00+12:00
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/memory-management", "#topic/maintenance"]
sources: ["~/.claude/projects/C--Vault-Lite/memory/feedback_memory_consolidation_pattern.md"]
summary: "Maintenance workflow: delete superseded files, merge overlapping content, fill index gaps, reformat MEMORY.md to spec."
provenance: "extracted: 1.0"
---

## When to Run

- Memory directory grows to >35 files
- MEMORY.md approaches 150 lines
- After major project completion
- Quarterly minimum

## Phase 1: Delete Superseded Files

Remove files that have been replaced by completion summaries:

- Early project snapshots (Phase 1-3 notes) superseded by completion summaries → delete
- Stale lockfiles (`.consolidate-lock`, etc.) → delete
- Technical reference files fully captured in a feedback file → merge then delete

**Example**: `project_ralph_refactor_2026_03_20.md` (Phase 1-3 snapshot) superseded by `project_ralph_fastapi_refactor_complete.md` (full 6-phase completion).

## Phase 2: Merge Overlapping Content

Before deleting duplicates:

1. Identify reference files with detail not in feedback versions
2. Append unique content (issue tables, action plan paths, precision breakdowns)
3. Delete the reference file

**Example**: `slr_pipeline_code_review.md` (9-issue breakdown table + action plan) merged into `feedback_slr_pipeline_code_review.md`, then deleted.

## Phase 3: Fill Index Gaps

1. List all memory files
2. Cross-check against MEMORY.md line-by-line
3. For each unindexed file: decide "worth indexing for future sessions?"
4. Add to index: yes → one-line pointer to MEMORY.md
5. Skip: completed sub-tasks with no future action

**Example**: `feedback_agent_team_patterns.md` was unindexed but contains reusable patterns → added to feedback section.

## Phase 4: Reformat MEMORY.md to Spec

**Target format:**
```
- [Title](file.md) — one-line hook (<150 chars)
```

**Actions:**
1. Convert all entries from `### Title` + paragraph to single-line bullet with file link
2. Move paragraph-level detail from MEMORY.md into topic files
3. Remove "⭐ NEW" markers from entries older than ~1 week
4. Compress verbose entries: if a line exceeds 150 chars, detail belongs in the topic file
5. Target: under 60 lines total

**Validation**: 2026-03-26 consolidation reduced directory from 40 → 36 files; MEMORY.md from verbose 113 lines to compact ~55 lines.

---

## Related

- [[07-Wiki/03-skills/dream-consolidation-checklist.md|Dream Consolidation Checklist]] — regular review workflow
- [[07-Wiki/03-skills/memory-system-alignment.md|Memory System Alignment]] — memory typing system
