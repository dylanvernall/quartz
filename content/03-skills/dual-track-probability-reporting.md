---
title: "Dual-Track Probability Reporting"
created: 2026-04-20T00:00:00Z
modified: 2026-04-20T00:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/methodology", "#topic/research", "#domain/analysis"]
summary: "When live intelligence diverges from Bayesian posterior, report both values explicitly rather than overwriting — maintains rigour while surfacing current signal."
sources: ["memory/project_iran_war_nz_claims_validation_2026_04_17.md"]
provenance:
  extracted: 0.8
  inferred: 0.2
  ambiguous: 0.0
---

# Dual-Track Probability Reporting

## Pattern

When a formal Bayesian posterior and live intelligence estimate diverge, report both explicitly in documents rather than overwriting the posterior with the live figure.

**Format**: `"30% (Bayesian posterior) → 45–55%* (live intelligence, 2026-04-17, preliminary)"`

**Why**: Overwiting the posterior destroys the methodological audit trail. Showing both values:
- Preserves Bayesian rigour (posterior is from a formal update process)
- Elevates the current signal (live estimate warns decision-makers of higher risk)
- Flags the discrepancy for formal recomputation
- Allows future readers to trace the escalation

## When to Apply

- Probability estimates sourced from two different methodologies (Bayesian model vs. intelligence briefing)
- Live data signals a materially different risk profile (>10 percentage point divergence)
- Documents will be read by policymakers or decision-makers who need current signal

## Implementation

1. Add footnote to the posterior figure: `"* Preliminary — formal Bayesian recomputation pending"`
2. Add wikilink from the live estimate to the source document (e.g., `[[02d-Intelligence-Briefings]]`)
3. Update the MOC status dashboard to flag the discrepancy
4. Schedule formal Bayesian recomputation as a follow-up action

## Claims Consistency Principle

When the same probability appears across 5+ documents, inconsistency is a **quality defect**. The fix:
1. Identify the authoritative source document
2. Update all downstream documents to reference it via wikilink
3. Archive superseded figures with deprecation notices (not silent deletion)

## Related

- [[07-Wiki/03-skills/slr-pipeline-patterns.md|SLR Pipeline Patterns]] — evidence quality standards
- [[07-Wiki/03-skills/external-recommendation-validation.md|External Recommendation Validation]]
