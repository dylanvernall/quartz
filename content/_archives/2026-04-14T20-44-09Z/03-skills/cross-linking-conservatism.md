---
title: "Cross-Linking Conservatism"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/vault-structure", "#topic/knowledge-linking", "#domain/vault"]
summary: "Cross-links must be high-confidence and research-backed; avoid speculative topical bridges that create navigation noise."
sources: ["memory/feedback_cross_linking_conservatism.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Cross-Linking Conservatism

## Rule: Cross-links must be high-confidence and research-backed

Speculative links create noise and false navigation paths. Better to have fewer, high-quality links that users can trust than many topical links that may mislead.

**Confidence threshold**: 0.90+ (HIGH only)

## How to Apply

When proposing cross-links:

1. Require explicit evidence from source document (not just folder proximity)
2. Read both source and target before suggesting link
3. If you're inferring the relationship, confidence is too low — skip it
4. Only add links where source explicitly applies or references target's methodology

### Example: ACCEPTED

**Paper-Implementation ADRs → ADR Guide** (0.95 confidence)

Reason: ADRs explicitly use MADR format that the guide documents. Direct reference exists in both documents.

### Counter-Example: REJECTED

**Guitar-Transcription → Writing Guide** (speculative, SKIPPED)

Reason: Source doesn't mention writing methodology. Connection is only topical and requires inference.

## Rule: Avoid environmental ↔ client-work bridges

Environmental research and client deliverables are separate problem spaces. Adding links creates noise without improving discoverability for either domain.

**How to apply**: For cross-linking recommendations:
- Skip bridges connecting Air-Quality SLRs and client-specific work (e.g., 1102413 deliverables)
- If a future project EXPLICITLY requires bridging these domains, document the dependency first
- Preserve domain separation unless there's formal project dependency

## Related Skills

- [[07-Wiki/03-skills/agent-team-patterns|Agent Team Execution Patterns]]
- [[07-Wiki/03-skills/vault-structure|Vault Structure & Organisation]]
