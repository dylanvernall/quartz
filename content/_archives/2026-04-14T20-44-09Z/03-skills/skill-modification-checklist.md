---
title: "Skill Modification Checklist"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/skill-authoring", "#topic/maintenance"]
summary: "When adding/removing skill phases, update all cross-referenced sections: description, extracted_entities, overview table, examples, hooks, best practices, and version history."
sources: ["memory/feedback_skill_modification_checklist.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Skill Modification Checklist

## Rule: Update All Cross-Referenced Sections

When adding or removing a phase from a multi-phase skill, update every section that references that phase — not doing so creates inconsistency and confusion.

**Why**: Skill files reference phases in multiple places (description, extracted_entities, overview table, examples, hooks, best practices). Removing a phase from one place but not others creates contradictions when users reference different parts.

## How to Apply

### Complete Modification Checklist

When adding or removing a phase, systematically update:

- [ ] **Header/Description** — Update title and opening description (e.g., "4 phases" instead of "5 phases")
- [ ] **extracted_entities** — Remove phase name from entity list
- [ ] **Quick Overview table** — Update phase count, total time estimate, remove/add phase row
- [ ] **Phase-specific section** — Delete entire phase section (e.g., `## Phase X: ...`)
- [ ] **Examples** — Remove phase references from worked examples and output samples
- [ ] **Hook descriptions** — Update hook configuration if it mentions the removed/added phase
- [ ] **Best Practices** — Remove phase-specific guidance section
- [ ] **Version History** — Document the change with date and reasoning

### Example: Removing Phase 4 from session-wrap-up

**Before modification**:
```
5 phases, 5–10 minutes total
Phase 4: Publish It (includes git push, PR creation)
```

**After checklist completion**:
```
4 phases, 3–5 minutes total
(Phase 4 section removed entirely)
Examples updated: no longer shows Phase 4 output
Hooks updated: "Skips Phase 3 (requires human judgment)" instead of "Phase 3 & 4"
Best Practices: deleted "Phase 4: Publishing" section
Version History: "2026-04-14 — Removed Phase 4 (Publish It) because X"
```

## Quality Check

After modifying a skill:
- [ ] Description reflects new phase count
- [ ] No orphaned references to removed phase
- [ ] All example walkthroughs match new phase structure
- [ ] Hook configuration still makes sense
- [ ] Version History has dated entry

## Related Skills

- [[07-Wiki/03-skills/skill-self-containment|Skill Self-Containment]]
- [[07-Wiki/03-skills/skill-yaml-limits|Skill YAML Configuration Limits]]
