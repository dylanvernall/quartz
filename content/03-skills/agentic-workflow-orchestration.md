---
title: "Agentic Workflow Orchestration"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/agentic-workflows", "#domain/claude-code"]
summary: "Orchestrating multi-agent workflows with parallel execution, scope independence, and confidence thresholds."
sources: ["memory/feedback_agent_team_patterns.md", ".claude/rules/agent-patterns.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Agentic Workflow Orchestration

## Rule

**Parallel agents require independent file domains. High-confidence cross-links need explicit evidence from both source AND target documents. Reciprocal linking improves hub connectivity.**

## Why

- **Parallelism**: Independent file domains = zero coordination overhead. Shared files = bottleneck.
- **Reliability**: Topical similarity is a false signal. Real dependency requires explicit evidence in the source document mentioning or applying the target.
- **Discoverability**: One-way links create dead ends. Bidirectional links improve vault searchability and hub visibility.

## How to Apply

### Define Independent Scopes

Map which files each agent will modify before spawning.

**Pattern**:
```
Main task: "Audit all domains"
├─ Agent 1: "Audit 01-Projects/" (owns 01-Projects/** files)
├─ Agent 2: "Audit 02-Areas/" (owns 02-Areas/** files)
└─ Agent 3: "Audit 03-Resources/" (owns 03-Resources/** files)
```

Result: All independent → can run in parallel.

**Exception**: If agents must coordinate on shared files, sequence them instead:
```
→ Agent 1: Find outdated links
→ Agent 2: (awaits Agent 1 results) Fix links found
```

### High-Confidence Cross-Linking

**Pattern**: Read BOTH source and target before deciding.

1. Read source document fully
2. Read target document fully
3. Ask: "Does source explicitly mention or apply target's content?"
4. If answer is inference/assumption → confidence is LOW → skip the link
5. If answer is "yes, explicit application" → confidence is HIGH → add the link

**Real example**: Paper-Implementation ADRs → ADR Guide (confidence 0.95) because the ADR folder uses explicit MADR naming that the guide documents. NOT because both are about software (low confidence).

### Bidirectional Linking

When adding cross-link Source → Target, also add reciprocal Target → Source (especially for methodology/guide documents).

**Pattern**:
- Forward: Paper-Implementation → ADR Guide
- Reciprocal: ADR Guide → Implementation Projects
- Result: Both hubs now visible in each direction, improved centrality

### Confidence Scoring

Document decisions with explicit reasoning:

```markdown
## Link: Paper A → Tooling Hub

**Rationale**: Paper A describes "agentic code synthesis",
             tooling hub covers "Claude Code agent patterns"

**Confidence**: 0.92 (high)
- Explicit overlap in 3 sections
- Both documents read in full
- Semantic relationship clear

**Assumption**: "Agentic code synthesis" maps to Claude Code patterns

**Gaps**: Paper from Feb 2026; tooling may have evolved
```

## Applied

- Met-pipeline team: 13 Haiku agents (independent modules) + Sonnet team lead = parallel execution
- Vault cross-linking: 40+ bidirectional project ↔ methodology links, all confidence >= 0.85
- Memory consolidation: 22 skill pages with reciprocal references to related skills

## Related Skills

- [[07-Wiki/03-skills/agent-model-selection|Agent Model Selection for Scoped Tasks]]
- [[07-Wiki/03-skills/agent-team-patterns|Agent Team Execution Patterns]]
- [[07-Wiki/03-skills/cross-linking-conservatism|Cross-Linking Conservatism]]
