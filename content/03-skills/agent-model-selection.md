---
title: "Agent Model Selection for Scoped Tasks"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/agentic-workflows", "#topic/cost-optimization", "#domain/claude-code"]
summary: "Use Haiku 4.5 for bounded, well-scoped agent tasks; Sonnet for coordination and complex reasoning."
sources: ["memory/feedback_agent_model_selection.md", "memory/feedback_agent_haiku_default.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Agent Model Selection for Scoped Tasks

## Rule

**Default: ALWAYS specify `model: haiku` when spawning agents unless the user explicitly requests Opus or Sonnet.**

For team leads, always use Sonnet (or higher), even if individual agents are Haiku. The lead needs to read agent outputs, validate against spec, decide which agents to spawn next, and synthesise across multiple reports.

## Why

- **Cost**: Haiku is ~1/3 the cost of Opus/Sonnet
- **Speed**: Haiku is 2–3× faster for bounded scoped tasks
- **Suitability**: Haiku is perfectly matched to agent work (explicit file domains, clear task signatures, deterministic success criteria)
- **Budget protection**: Prevents accidental high-cost runs that blow through user API budgets
- **Team lead differs**: Leads coordinate rather than execute — they need Sonnet's reasoning capability to make scheduling decisions and validate agent work

## How to Apply

### Haiku 4.5 Capability Ceiling

**Excels at**:
- Template-following (given signature, implement function)
- Format transformation (CSV → DataFrame, etc.)
- Testing (run test suite, report pass/fail)
- Validation (file structure, row counts, formats)
- Single-file debugging (compile errors, syntax)

**Struggles with**:
- Design decisions (which approach is better? — needs reasoning)
- Cross-domain synthesis (integrate module A + B + C)
- Novel problem-solving (constraint X, Y, Z — find creative solution)
- Context stitching (pull from 10 documents to synthesise decision)

### Agent Model Selection Decision Table

| Scenario | Model | Reason |
|----------|-------|--------|
| "Create CSV with 8,760 rows, these columns, this date range" | Haiku | Bounded task; success = row count + header validation |
| "Implement read_data_file() + apply_column_mapping() with test stubs" | Haiku | Function signatures explicit; tests predefined |
| "Fix failing test in test_utils_data.R" | Haiku | Success = 1 test passes (quantifiable) |
| "Design the auth architecture for new system" | Sonnet | Needs reasoning about trade-offs, security, scalability |
| "Coordinate 3 teams working on different phases" | Sonnet | Team lead needs context synthesis, cross-team reasoning |

### Cost-Benefit Analysis

| Model | Speed | Cost | When to use |
|-------|-------|------|-------------|
| Haiku | 3× faster | ~1/3 cost | Scoped tasks, deterministic success criteria |
| Sonnet | 1× | 1× | General-purpose, design decisions, team leads |
| Opus | 0.5× | ~3× | Complex reasoning, multi-step research (rarely needed) |

Example: 14 files across 3 waves using Haiku for 6 scoped agents + Sonnet team lead = ~2× faster than all Opus, same quality.

## Applied

- Met-pipeline team: 13 agents (Haiku 4.5) + team-lead (Sonnet)
- OpenAir Phase 2 Wave A: 6 Haiku agents (cost: 1/3, speed: 2–3× faster)

## Related Skills

- [[07-Wiki/03-skills/agent-team-patterns|Agent Team Execution Patterns]]
- [[07-Wiki/03-skills/agentic-workflow-orchestration|Agentic Workflow Orchestration]]
