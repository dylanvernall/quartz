---
title: "Tag Refinement Standards"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/vault-maintenance", "#topic/metadata"]
summary: "Standardize vault tags: type tags on all files, domain hierarchy for grouping, MOCs strictly #_MOC only. 57% of vault had tag issues; consistent tagging enables faster searches and filtering."
sources: ["memory/feedback_tag_refinement_2026_03_19.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Tag Refinement Standards

## Rule: Consistent, Hierarchical Tagging System

Implement comprehensive tag standardization across all vault files to enable faster discovery, filtering, and metadata analysis.

**Execution results** (2026-03-19):
- 1615 files processed
- 929 files modified (57% had tag issues)
- 149 MOC files standardized to `["#_MOC"]`
- 775 missing type tags added
- 28 duplicate tags removed

## Why

Consistent tagging enables:
- Faster vault searches by type/domain
- Easier filtering for maintenance tasks
- Clearer metadata for future AI analysis
- MOC distinction from content files

## How to Apply

### Type Tags (Required on All Files)

Always include one or more type tags:
- `#type/adr` — Architecture Decision Records
- `#type/note` — General notes and observations
- `#type/guide` — How-to guides and methodology
- `#type/log` — Session logs and activity records
- `#type/test` — Test files and test documentation
- `#type/report` — Analysis reports and summaries
- `#type/skill` — Reusable workflow/skill documentation

**Inference**: Derive from filename patterns (adr, readme, report, log, test, note)

### Domain Tags (Use Hierarchy When Grouping)

Format: `#domain/topic` for related groupings:
- `#domain/air-quality` — Environmental research
- `#domain/vault-infrastructure` — System management
- `#domain/code-quality` — Development standards
- `#domain/agentic-workflows` — Autonomous execution patterns

Simple tags for one-off topics (no hierarchy):
- `#skill-audit`, `#pre-commit`, `#memory-management`

### Project Tags

Use for active/recent work:
- `#project/name` — Project-specific tags
- `#folder/name` — Folder-scoped work

### MOC Files

MOC files get exactly this tag set, nothing else:
```yaml
tags: ["#_moc"]
```

Never add additional tags to MOC files — the single `#_MOC` tag is the identifying marker.

## Quality Checklist

When refining tags:
- [ ] Every file has at least one `#type/` tag
- [ ] No placeholder tags like `#domain/x` or `#type/y`
- [ ] MOC files have exactly `["#_MOC"]`, no additional tags
- [ ] Domain tags use hierarchy only when grouping related concepts
- [ ] No duplicate tags within a file
- [ ] Project-specific work tagged with `#project/name`

## Tooling

**Script**: `99-System/02-Scripts/tag_refiner.py` — reusable for future tag audits. Can be run periodically to detect regressions.

## Related Skills

- [[07-Wiki/03-skills/vault-structure|Vault Structure & Organisation]]
- [[07-Wiki/03-skills/memory-consolidation|Memory Consolidation]]
