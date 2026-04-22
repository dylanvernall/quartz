---
title: "Autocompact Thrashing Mitigation"
created: 2026-04-20T00:00:00Z
modified: 2026-04-20T00:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/context-management", "#topic/cost-optimization", "#domain/claude-code"]
summary: "Three-tier strategy to stop context refilling to limit within 3 turns of compaction: grep-before-read, output limits, and subagent isolation."
sources: ["memory/feedback_autocompact_thrashing_mitigation.md"]
provenance:
  extracted: 0.95
  inferred: 0.05
  ambiguous: 0.0
---

# Autocompact Thrashing Mitigation

## Problem

Autocompact thrashing = context refills to limit within 3 turns of compaction, 3× in a row. Causes: large unsliced file reads, untruncated bash output, or compaction threshold too high.

## Three-Tier Strategy

### Tier 1 — Zero Cost, Immediate (Implemented 2026-04-20)

1. **Grep-before-read discipline**: Always run `Grep` with `-n` first to get line numbers. Use `Read` with `offset`+`limit` (max 200 lines per call). Never read whole files.
2. **`BASH_MAX_OUTPUT_LENGTH`: 150000 → 10000** — prevents single `ls` or `git log` from flooding context
3. **`autocompact_percentage_override`: 75 → 50** — earlier compaction before bloat accumulates

### Tier 2 — Medium Effort, High Reliability (Pending)

PostToolUse hook that truncates Bash/MCP output >150 lines with `"...N lines truncated"` marker. Automated — no discipline required.

### Tier 3 — Higher Cost, Selective

Spawn Explore subagent when task requires reading 5+ large files. Isolates exploration to a dedicated context window. Use consciously — costs 2× tokens.

## Cost-Benefit

| Tier | Token Cost | Reliability | When to Use |
|---|---|---|---|
| 1 | None | Medium (discipline) | Always — baseline |
| 2 | None | High (automated) | After Tier 1 proves insufficient |
| 3 | 2× (subagent) | High | Large code investigations (5+ files) |

## Monitoring

Track thrashing frequency over 5–10 sessions:
- Thrashing persists → large tool outputs still occurring; implement Tier 2
- Thrashing stops → Tier 1 is sufficient
- Rare isolated incidents → Tier 1 + manual `grep` discipline works

## Related

- [[07-Wiki/03-skills/project-exploration.md|Project Exploration]] — Explore subagent pattern (Tier 3)
- [[07-Wiki/03-skills/directory-structure-mapping.md|Directory Structure Mapping]]
