---
title: "Vault Structure and Organization"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/vault-organization", "#domain/vault"]
summary: "Vault domain structure (01-Projects, 02-Areas, 03-Resources, 99-System), file placement, and MOC navigation."
sources: [".claude/rules/wikilinks.md", "memory/feedback_wikilink_path_conversion.md", ".claude/CLAUDE.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Vault Structure and Organization

## Rule

**Vault has 4 domains (01-Projects, 02-Areas, 03-Resources, 99-System). Each domain has a `_MOC.md` index. New files belong in the appropriate domain based on their type and lifespan.**

## Why

- **Predictability**: Consistent structure means files are always findable in the same location
- **Discoverability**: MOC indices enable navigation without full vault knowledge
- **Lifecycle**: Domain structure aligns with retention tiers (permanent resources in 03-, ephemeral logs in 99-)
- **Collaboration**: Clear rules prevent file placement drift and redundancy

## How to Apply

### Four Domain Structure

| Domain | Purpose | Contents | Files | MOC |
|--------|---------|----------|-------|-----|
| `01-Projects/` | Active and completed projects | Coding, research, infrastructure work | Implementation logs, design docs, completion reports | `01-Projects/_MOC.md` |
| `02-Areas/` | Areas of interest/responsibility | Knowledge domains, topic areas | Topic guides, area-specific docs | `02-Areas/_MOC.md` |
| `03-Resources/` | Permanent reference material | Guides, checklists, methodology | How-to docs, research syntheses, frameworks | `03-Resources/_MOC.md` |
| `99-System/` | System and meta | Vault maintenance, logs, configuration | Scripts, logs, rules, system docs | `99-System/_MOC.md` |

### File Placement Rules

**Decide domain based on lifespan and purpose:**

| File Type | Domain | Why |
|-----------|--------|-----|
| **Implementation log** (what was built, decisions) | 01-Projects/ | Active during project; archived on completion |
| **Design doc** (architecture, approach) | 01-Projects/ | Project-specific; archive on completion |
| **Research synthesis** (permanent guide) | 03-Resources/04-03-Methodology-Guides/ | Permanent, reusable across projects |
| **Completion report** (post-project summary) | 01-Projects/ | Context-specific; may archive |
| **Session handoff** (ephemeral context) | 99-System/10-Logs/sessions/ | Ephemeral (30 days); regenerated each session |
| **Vault maintenance log** | 99-System/10-Logs/ | Seasonal (90 days); auto-expires |
| **Code quality standard** | 03-Resources/ or .claude/rules/ | Permanent, shared rule |
| **Broken link report** | 99-System/10-Logs/ | Seasonal report; refreshed regularly |

### MOC Navigation

Every domain has a `_MOC.md` file that indexes that domain's contents.

**Pattern**:
- Root MOC: `_MOC.md` (links to all 4 domain MOCs)
- Domain MOC: `01-Projects/_MOC.md` (indexes all projects)
- Sub-domain MOC: `01-Projects/02-01-Coding/_MOC.md` (indexes coding projects)
- Wiki MOC: `07-Wiki/index.md` (wiki knowledge index)

**Using MOCs**:
1. Start at root `_MOC.md` or domain MOC
2. Follow wikilinks to narrower domains
3. Each MOC shows available topics and starting points
4. Linked pages show their own related content

### Project Organization Example

```
01-Projects/
├─ 02-01-Coding/
│  ├─ _MOC.md (index: Ralph, OpenAir, etc.)
│  ├─ ralph/
│  │  ├─ CLAUDE.md (project-specific rules)
│  │  ├─ README.md (overview)
│  │  ├─ 01-design.md
│  │  └─ 02-implementation.md
│  └─ openair-phase-2/
│     ├─ CLAUDE.md
│     └─ [project files]
└─ 02-02-AI-Research/
   ├─ _MOC.md
   └─ [research projects]
```

### Placement Checklist

Before creating a new file, ask:

1. **Is this permanent or temporary?** → Permanent (03-Resources or .claude/rules/), Temporary (99-System/logs/)
2. **Is this project-specific or reusable?** → Project-specific (01-Projects/), Reusable (03-Resources/)
3. **Does this have an end date?** → Yes (01-Projects/ or 99-System/), No (03-Resources/)
4. **What domain is closest?** → Check `_MOC.md` files; ask if uncertain

## Applied

- Vault: 2214 files organized across 4 domains + 07-Wiki (knowledge base)
- Projects: 5 active project folders; 30+ completed projects in archive
- Resources: 200+ methodology guides, references, and standards
- System: Scripts, logs, configuration, rules in 99-System/

## Related Skills

- [[07-Wiki/03-skills/wikilink-standards|Wikilink Standards and Path Conventions]]
- [[07-Wiki/03-skills/markdown-standards|Markdown Documentation Standards]]
- [[07-Wiki/03-skills/vault-automation|Vault Automation Patterns]]
