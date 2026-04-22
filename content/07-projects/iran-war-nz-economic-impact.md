---
title: "Iran-War-NZ Economic Impact — Claims Validation"
created: 2026-04-17T00:00:00Z
modified: 2026-04-20T00:00:00Z
type: completion-report
retention: seasonal
status: completed
tags: ["#type/project", "#domain/analysis", "#topic/research"]
summary: "Claims consistency validation across 5 documents; dual-track probability reporting (30% posterior + 45–55% live intelligence); resolved T&T revenue discrepancy."
---

# Iran-War-NZ Economic Impact — Claims Validation

## Overview

**Date**: 2026-04-17  
**Status**: Completed  
**Scope**: Quality improvements across Iran-War-NZ-Economic-Impact vault documents  
**Focus**: Claims consistency validation (user priority)

## Quality Metrics Addressed

### 1. Claims Consistency — Probability Escalation (PRIMARY)

**Problem**: Prolonged scenario probability divergence across documents
- **Bayesian posterior**: 30% (from formal update process)
- **Live intelligence**: 45–55% (2026-04-17, MFAT briefings)
- **Impact**: Inconsistent figures misleading policymakers

**Resolution**: Applied dual-track probability reporting across 5 files
- 05a-Scenario-Matrix (line 230): "30% (posterior) → 45–55%*" with footnote
- 06a-Executive-Summary (line ~118): Added probability context + wikilink to source
- _MOC.md (lines 112, 182): Key Assumptions Log + Status Dashboard updated
- All documents now reference 02d-MFAT-Intelligence-Briefings as source

**Rationale**: Preserves Bayesian rigour (posterior from formal process) while elevating current intelligence signal. Flags escalation as "preliminary pending formal recomputation" — prevents false precision while warning decision-makers of higher risk.

### 2. Claims Consistency — Revenue Discrepancy (SECONDARY)

**Problem**: T&T quarterly revenue conflict
- Old file (04c): ~NZ$25M/quarter
- Active file (04d): ~NZ$50M/quarter

**Resolution**: Archived 04c with deprecation banner explaining revision and directing readers to active files (04c-Construction-Sector, 04d-TandT-Firm-Exposure)

**Outcome**: Stale figures cannot mislead; git history preserved for audit trail

### 3. Structural Integrity (VERIFIED)

**Status**: No changes needed
- H1 heading convention: Vault uses H2 post-frontmatter (correct per standard)
- Previous session fixed actual structural issue (duplicate Section 8 headings)

### 4. Citation Traceability (ENHANCED)

**Action**: Added wikilinks to 02d-MFAT-Intelligence-Briefings
- All probability claims now trace to explicit source
- Standard: Every significant claim references its source document

### 5. Frontmatter Currency (DEFERRED)

**Status**: Not user priority
- Timestamps remain stale on draft files
- Can be addressed in next round if needed

## Economic Significance

The Prolonged scenario (45–55% live probability) has highest impact on NZ economy:
- **GDP**: –1.5%+
- **Unemployment**: +0.5–0.8 percentage points
- **NZD depreciation**: 6–8%
- **Dairy margin**: –12%+, forced deleveraging, sector restructuring
- **T&T sector**: –10–15% sustained revenue, potential 10–15% headcount reduction

Inconsistent probability estimates = incorrect decision-making. Escalating the live estimate signals materially higher risk profile.

## Files Modified

| File | Changes | Type |
|------|---------|------|
| 05a-Scenario-Matrix.md | Line 230: Prolonged prob dual-track format + footnote | substantive |
| 06a-Executive-Summary.md | Line ~118: Probability context + wikilink to source | substantive |
| _MOC.md | Lines 112, 182: Key Assumptions Log + Status Dashboard | substantive |
| 04c-Construction-Goods-Imports-And-T+T.md | Status: archived; deprecation notice added | substantive |
| 04d-TandT-Firm-Exposure.md | Verified (no changes; correct) | verification |

## Key Learnings

### Dual-Track Probability Best Practice

Keep both posterior and live estimate visible when they diverge (>10 pp):
- Maintains methodological rigour
- Elevates current signal without losing context
- Flags as preliminary to prevent false precision
- Preserves audit trail for future recomputation

### Skill Limitations in Project Work

Initial request: Use `/brainstorm` skill for quality metrics — not available (disabled model invocation)

**Resolution**: Defined metrics inline from exploration findings — worked equally well

**Lesson**: For vault projects, use plan template + exploration rather than forcing unavailable skills

## Related

- [[07-Wiki/03-skills/dual-track-probability-reporting.md|Dual-Track Probability Reporting]] — methodology for diverging estimates
- [[07-Wiki/03-skills/external-recommendation-validation.md|External Recommendation Validation]]
