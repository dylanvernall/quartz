---
title: "Tag Refinement Standards"
created: 2026-04-14T15:30:00+12:00
modified: 2026-04-14T15:30:00+12:00
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/vault-architecture", "#topic/metadata"]
sources: ["~/.claude/projects/C--Vault-Lite/memory/feedback_tag_refinement_2026_03_19.md"]
summary: "Comprehensive tagging system with hierarchical #domain/topic structure, type tags on all documents, and standardized #_MOC for indexes."
provenance: "extracted: 1.0"
---

## Tagging Guidelines

### Type Tags (Required on ALL documents)

Always include category classification:

- `#type/adr` — Architecture Decision Records
- `#type/note` — General knowledge or observations
- `#type/guide` — How-to, cheatsheet, reference
- `#type/log` — Audit trails, session logs
- `#type/test` — Test specifications
- `#type/report` — Analysis or evaluation results
- `#type/skill` — Reusable techniques or patterns
- `#type/moc` — Map of Contents index files

### Domain Tags (Hierarchical when useful)

Use hierarchy for large topic areas:

- `#domain/air-quality` — specific sub-domain
- `#domain/vault-infrastructure` — grouped domains
- Or simple `#domain/research`, `#domain/code`

### Project Tags (Active/Recent Work)

Mark which project a document belongs to:

- `#project/my-app` or `#folder/project-name` for active/recent work

### MOC Files (Special Rule)

Maps of Contents use **ONLY**:

```yaml
tags: ["#_MOC"]
```

No additional domain/type tags. The `#_MOC` tag alone distinguishes MOCs from content files and avoids inflating tag counts.

---

## Execution Results (2026-03-19 Standardization)

Applied across 1615 vault files:

| Change | Count | Result |
|--------|-------|--------|
| MOC files standardized | 149 | `#_MOC` only |
| Missing type tags added | 775 | 57% of files had issues |
| Duplicate tags removed | 28 | Cleaned up within-file repetitions |

---

## Why Tagging Matters

Better tag consistency enables:
- **Faster vault searches** by type/domain
- **Easier filtering** for maintenance tasks
- **Clearer metadata** for future AI analysis
- **MOC distinction** from content files

---

## Script Reference

`99-System/02-Scripts/tag_refiner.py` — Reusable script for future tag audits across the vault.

---

## Related

- [[07-Wiki/03-skills/vault-log-cleanup-automation.md|Vault Log Cleanup Automation]] — vault maintenance pattern
- [[07-Wiki/03-skills/memory-system-alignment.md|Memory System Alignment]] — applies tagging to memory system
