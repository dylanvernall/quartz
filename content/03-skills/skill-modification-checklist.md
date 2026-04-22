---
title: "Skill Modification Checklist"
created: 2026-04-14T15:30:00+12:00
modified: 2026-04-14T15:30:00+12:00
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/skill-authoring", "#topic/maintenance"]
sources: ["~/.claude/projects/C--Vault-Lite/memory/feedback_skill_modification_checklist.md"]
summary: "Multi-section updates required when adding/removing phases or major features — ensure all cross-references are consistent."
provenance: "extracted: 1.0"
---

## The Problem

When modifying skill phases (adding/removing), inconsistency emerges across multiple sections (description, examples, hooks, best practices). Users reference different parts of the skill and encounter conflicting information.

## The Checklist

When **adding or removing a phase**, update all sections:

- [ ] **Header/Description** — Update title and opening description
- [ ] **extracted_entities** — Add/remove phase name from list
- [ ] **Quick Overview table** — Update phase count, total time, phase row
- [ ] **Phase-specific section** — Create/delete entire `## Phase X: ...` section
- [ ] **Examples** — Add/remove phase references from worked examples
- [ ] **Hook descriptions** — Update hook configuration if it mentions the phase
- [ ] **Best Practices** — Add/remove phase-specific guidance section
- [ ] **Version History** — Document the change with date and reasoning

## Example

Removing Phase 4 (Publish It) from session-wrap-up skill:

| Section | Change |
|---|---|
| Description | "4 phases" instead of "5 phases" |
| extracted_entities | Removed "Publish It" |
| Table | 4 rows instead of 5; time 3-5 min instead of 5-10 min |
| Phase section | Delete "## Phase 4: Publish It" entirely |
| Examples | Remove Phase 4 output example |
| Hooks | "Skips Phase 3" instead of "Phase 3 & 4" |
| Best Practices | Delete "Phase 4: Publishing" section |
| Version History | Added entry documenting removal |

## Why It Matters

Incomplete updates create confusion when users reference skill documentation inconsistently. Better to do all sections at once than discover missing updates later.

---

## Related

- [[07-Wiki/03-skills/teach-patterns-as-you-go.md|Teach Patterns as You Go]] — pattern explanation during skill development
