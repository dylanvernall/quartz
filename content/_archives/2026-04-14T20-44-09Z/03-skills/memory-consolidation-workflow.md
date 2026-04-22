---
title: "Memory Consolidation Workflow"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/memory-management", "#topic/vault-maintenance"]
summary: "Quarterly dream pass workflow to keep memory index fresh: orient, gather signal (stale markers, unindexed files, drifted facts), consolidate, prune to <150 lines."
sources: ["memory/feedback_dream_consolidation_workflow.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Memory Consolidation Workflow

## Rule: Regular Dream Pass Maintenance

Run a "dream pass" consolidation workflow quarterly or after major project completion to keep the memory system healthy, remove stale entries, and maintain the MEMORY.md index at <150 lines.

**Why:** Memory directory grows with each session. Without regular pruning, index becomes cluttered with stale markers, orphaned files, and duplicate entries. A 30-minute structured pass restores clarity and speeds up future memory lookups.

## Phase 1 — Orient

1. List all memory files: `ls memory/ | wc -l`
2. Read MEMORY.md to assess current index state
3. Skim 2–3 recent memory files for style consistency

## Phase 2 — Gather Signal

Identify these issues:

**Stale markers**: `⭐ NEW` tags should only mark entries <1 week old. Strip anything older.

**Unindexed files**: Run:
```bash
ls memory/ | while read f; do grep -q "$f" MEMORY.md || echo "$f"; done
```
Review results; add missing entries if file is worth indexing.

**Stale dates**: Search for absolute dates (e.g., "18 March 2026 deadline"). If deadline has passed, update entry to reflect actual status (submitted, completed, blocked).

**Near-duplicates**: Two files on same pattern (e.g., SLR code review + testing mocking both covering "real data"). Keep both if scope differs; merge if nearly identical.

**Drifted facts**: Sample 3–4 memory files and verify claims against current codebase. If contradicted, fix the memory.

## Phase 3 — Consolidate

For each issue found, apply the appropriate action:

- **Stale markers**: Edit MEMORY.md, remove `⭐ NEW`
- **Unindexed files**: Add one-line pointer to MEMORY.md index
- **Stale dates**: Replace relative language with status update
- **Duplicates**: Merge content into one file, delete other, update MEMORY.md
- **Drifted facts**: Edit memory file to correct claim, add context

Batch related changes into single edits per file to minimize tool calls.

## Phase 4 — Prune and Index

**Line count check**: Run `wc -l MEMORY.md` — target <150 lines.

If over limit, condense entries: move detail from index into topic files.

**Verification**:
- No orphaned pointers (every file mentioned in MEMORY.md exists)
- Dates are absolute (2026-03-26, not "today")
- Status is clear (✅ COMPLETE, ⏳ IN PROGRESS)

## Result

After dream pass:
- MEMORY.md clean and current (no stale markers)
- All worth-keeping memory files indexed
- Duplicates merged, dead files removed
- Future sessions can orient in <2 minutes

## Related Skills

- [[07-Wiki/03-skills/vault-structure|Vault Structure & Organisation]]
- [[07-Wiki/03-skills/memory-system-management|Memory System Management]]
