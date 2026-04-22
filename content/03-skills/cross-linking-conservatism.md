---
title: "Cross-Linking Conservatism"
created: 2026-04-14T15:30:00+12:00
modified: 2026-04-14T15:30:00+12:00
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/vault-architecture", "#topic/knowledge-graph"]
sources: ["~/.claude/projects/C--Vault-Lite/memory/feedback_cross_linking_conservatism.md"]
summary: "Use high-confidence, research-backed cross-links only. Avoid speculative topical bridges that create noise and false navigation paths."
provenance: "extracted: 1.0"
---

## The Principle

Speculative links create noise and false navigation paths. Fewer high-quality links are better than many topical links that may mislead.

## Rule 1: High-Confidence Only (0.90+)

When proposing cross-links:

1. **Require explicit evidence** from source document (not just folder proximity)
2. **Set confidence threshold at 0.90+** (HIGH only)
3. **Read both source and target** before suggesting link
4. **If you're inferring** the relationship, confidence is too low — skip it
5. **Only add links** where source explicitly applies or references target's methodology

### Example

**Added** ✓ Paper-Implementation ADRs → ADR Guide (0.95 confidence)
- Reason: ADRs explicitly use MADR format that the guide documents

**Skipped** ✗ Guitar-Transcription → Writing Guide (speculative)
- Reason: source doesn't mention writing methodology — connection is only topical

## Rule 2: Avoid Distant-Domain Bridges

Skip bridges between topically distant domains unless there's **explicit project dependency**.

Example: Environmental research ↔ Client deliverables are separate problem spaces. Adding links creates noise without improving discoverability for either domain.

---

## Related

- [[07-Wiki/03-skills/agent-team-execution-patterns.md|Agent Team Execution Patterns]] — applies cross-linking to agent work
- [[07-Wiki/03-skills/vault-log-cleanup-automation.md|Vault Log Cleanup Automation]] — related vault health pattern
