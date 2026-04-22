---
title: "SLR + Web Search Synthesis"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/research-methodology", "#topic/synthesis"]
summary: "For rapidly-evolving topics, combine formal SLR (PRISMA, peer-reviewed, 12-18 month lag) with web search (current practitioner insights). Blend for both rigor and currency."
sources: ["memory/feedback_slr_web_search_synthesis.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# SLR + Web Search Synthesis

## Rule: Two-Track Research for Emerging Domains

For topics with rapid practitioner evolution (agentic coding, AI tools, frameworks), use parallel research tracks: formal systematic literature review (PRISMA) for rigor + web search for currency.

## Why

**Academic papers** (peer-reviewed):
- Rigorous but lag 12–18 months behind practice
- Foundation for understanding patterns and theory

**Web search** (blog posts, docs, announcements):
- Current (published last 30–60 days)
- Captures practitioner insights faster than conferences
- Often lack formal rigor

**Synthesis**: Combine both for accurate "snapshot" of field right now, with both academic foundation and practitioner benchmarks.

## How to Apply

### Phase 1: Design SLR with PRISMA 2020

- Use formal research databases: arXiv, Semantic Scholar, CrossRef
- Define inclusion/exclusion criteria
- Document screening and data extraction
- Apply quality assessment framework
- Result: 500+ academic papers analyzed, documented with methodology

### Phase 2: Simultaneously Run Web Search

- Search for recent posts/announcements (last 30–60 days)
- Target: official docs, practitioner blogs, benchmark leaderboards
- Capture current tool versions, benchmarks, recommendations
- Result: 6–10 recent web sources for practitioner validation

### Phase 3: Integrate Both Tracks

**Academic findings** → architectural patterns, design principles, established methodologies

**Web findings** → current tooling, recent benchmarks, emerging best practices

Synthesize into unified narrative with all claims sourced.

### Phase 4: Source Everything

Apply "no arbitrary values" rule strictly:
- Every numeric claim: page number + URL
- Every recommended tool: version + source
- Every benchmark: publication date + link
- Note publication dates clearly (Feb 2026 benchmarks vs June 2025 preprints)

## Real-World Example

**Agentic Coding Meta** (2026-03-24):

**Academic track** (PRISMA):
- arXiv: 450+ agent architecture papers
- Semantic Scholar: 380+ related papers
- Result: SWE-Agent, AutoCodeRover design patterns, multi-agent coordination frameworks

**Web track**:
- Claude Code docs (Feb 2026)
- GitHub Blog (recent releases)
- SWE-bench leaderboards (current as of Feb 2026)
- Result: Claude Opus 4.6 scores (78.2%), Plan Mode impact (40–60% rework reduction), emerging AGENTS.md standard

**Synthesis**: 1182 total citations, all sourced, PRISMA methodology documented, current as Feb 2026

## Cost-Benefit

- **Time**: 3–5 hours for full SLR synthesis
- **Rigor**: PRISMA 2020 compliance + formal quality assessment
- **Currency**: Current as Feb 2026 vs June 2025 for academic-only approach
- **Reusability**: Config + methodology ready for quarterly updates

## Related Skills

- [[07-Wiki/03-skills/slr-pipeline-patterns|SLR Pipeline Code Patterns]]
- [[07-Wiki/03-skills/binary-evaluation-strategy|Binary Evaluation Strategy]]
