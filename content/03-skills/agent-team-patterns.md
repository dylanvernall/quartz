---
title: "Agent Team Execution Patterns"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/agentic-workflows", "#topic/coordination", "#domain/claude-code"]
summary: "Parallel agents work best on independent file domains; cross-links require reading both source and target; bidirectional linking improves hub connectivity."
sources: ["memory/feedback_agent_team_patterns.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Agent Team Execution Patterns

## Rule 1: Parallel agents work best on independent file domains

When agents touch different projects/domains, they can run simultaneously without coordination overhead. Coordination (reading other agent outputs, merging changes) introduces bottlenecks.

**How to apply**: Before spawning parallel agents, map which files each agent will modify. If any file is modified by 2+ agents, either sequence them or coordinate via explicit handoff protocol.

## Rule 2: High-confidence cross-links require reading BOTH source and target

Topical similarity (shared keywords) is a false signal. Real dependency requires explicit evidence in source document that it applies or references the target's methodology.

**How to apply**: When evaluating cross-link candidates:

1. Read source document fully
2. Read target document fully
3. Ask: "Does source explicitly mention or apply target's content?"
4. If answer is inference/assumption, confidence is LOW — skip the link
5. If answer is "yes, it directly applies," confidence is HIGH — add the link

Real example: Paper-Implementation ADRs → ADR Guide (HIGH 0.95 confidence) because ADR folder uses explicit MADR naming convention that the guide documents. Not because they're both about software development (that would be LOW confidence).

## Rule 3: Bidirectional linking improves hub connectivity

One-way links create dead ends. Reciprocal links enable discovery in both directions and increase hub centrality appropriately.

**How to apply**: When adding a cross-link from Source → Target, also add reciprocal link Target → Source (if Target is a methodology/guide document). This creates bidirectional paths and improves vault searchability.

Example: Added Paper-Implementation → ADR Guide, then added reciprocal ADR Guide → Implementation Projects. Now users can discover either direction.

## Related Skills

- [[07-Wiki/03-skills/agent-model-selection|Agent Model Selection for Scoped Tasks]]
- [[07-Wiki/03-skills/cross-linking-conservatism|Cross-Linking Conservatism]]
