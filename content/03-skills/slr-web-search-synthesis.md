---
title: "SLR + Web Search for Meta Synthesis"
created: 2026-04-14T15:46:00+12:00
modified: 2026-04-14T15:46:00+12:00
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/research", "#topic/methodology"]
sources: ["~/.claude/projects/c--Vault-Lite/memory/feedback_slr_web_search_synthesis.md"]
summary: "Combine academic SLR (PRISMA formal) with web search (current practitioner insights) for accurate, current meta snapshots."
provenance: "extracted: 1.0"
---

## Rule: Two-Track Synthesis for Rapidly-Evolving Topics

**Why:**
- Academic papers (peer-reviewed) are rigorous but lag by 12-18 months
- Blog posts and docs (web) are current but may lack rigor
- Practitioners move faster than conferences/journals
- Snapshot of field "right now" requires both sources

**How to apply:**

1. **Design SLR** with PRISMA 2020 structure (formal databases: arXiv, Semantic Scholar, CrossRef)
2. **Run web search** simultaneously for recent posts/announcements (last 30-60 days)
3. **Integrate both** in synthesis: academic = architectural patterns, web = current tooling/benchmarks
4. **Apply "no arbitrary values" rule**: every numeric claim sourced with page/URL
5. **Note publication dates** clearly (Feb 2026 benchmarks vs Nov 2025 preprints)

## Example: Agentic Coding Meta (2026-03-24)

**Academic track:** arXiv (450+ agent papers) + Semantic Scholar (380+)
- SWE-Agent, AutoCodeRover architectures
- Design patterns

**Web track:** Claude Code docs, GitHub Blog, eesel.ai, SWE-bench leaderboards
- Claude Opus 4.6 78.2% benchmark
- Plan Mode 40-60% rework reduction
- AGENTS.md emerging standard

**Synthesis:** Integrated both sources, all claims sourced, PRISMA methodology documented.

## Cost-Benefit

| Dimension | Result |
|-----------|--------|
| Time | ~3-5 hours for full SLR synthesis (1182 citations) |
| Rigor | PRISMA 2020 compliance + formal quality assessment |
| Currency | Current as of Feb 2026 (vs June 2025 for academic-only) |
| Reusability | Config + methodology ready for quarterly updates |

**Confidence:** High (80%+) — validated in Agentic Coding SLR

## Related

See [[07-Wiki/03-skills/_MOC|Skills MOC]] for related research and methodology pages.
