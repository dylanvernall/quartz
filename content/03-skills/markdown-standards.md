---
title: "Markdown Documentation Standards"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/documentation", "#domain/vault"]
summary: "Frontmatter requirements, field definitions, and documentation lifecycle for vault documents."
sources: [".claude/rules/documentation.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Markdown Documentation Standards

## Rule

**All vault documents require complete frontmatter with 7 fields: title, created, modified, type, retention, status, tags.**

Documents are lifecycle-managed by retention tier (permanent, seasonal, ephemeral, context-specific).

## Why

- **Discoverability**: Tags enable vault search and cross-linking
- **Lifecycle**: Retention tiers auto-expire old documents (logs, analyses)
- **Workflow**: Type and status fields indicate where documents are in their lifecycle
- **Auditability**: Created/modified timestamps track document evolution

## How to Apply

### Frontmatter Template

```yaml
---
title: "Document Title"
created: 2026-04-15T00:00:00Z
modified: 2026-04-15T00:00:00Z
type: [skill|note|moc|reference|analysis|planning|...]
retention: [permanent|seasonal|ephemeral|context-specific]
status: [draft|active|completed|archived]
tags: ["#type/note", "#domain/x", "#topic/y"]
---
```

### Type Definitions

| Type | Use | Location | Lifespan |
|------|-----|----------|----------|
| `skill` | Workflows, patterns, best practices | 03-Resources/ or 07-Wiki/ | Permanent, reusable |
| `note` | General knowledge, observations | Anywhere | Active, may archive |
| `moc` | Index/Map of Contents | Domain roots | Permanent |
| `reference` | How-to, API docs, cheatsheets | 03-Resources/ | Permanent |
| `reference-guide` | Methodology guide | 03-Resources/ | Permanent |
| `analysis` | Research findings, comparisons | 01-Projects/ or 02-Areas/ | Seasonal (90 days) |
| `planning` | Architecture, design docs | 01-Projects/ | Context-specific |
| `implementation-log` | What was built, decisions made | 01-Projects/ | Context-specific |
| `completion-report` | Post-project summary | 01-Projects/ | Seasonal |
| `session-note` | Session handoff notes | 99-System/ | Ephemeral (30 days) |
| `system-documentation` | Config, rules, system-level | 99-System/ | Permanent |

### Retention Tiers

**Permanent**: Frameworks, ADRs, reusable guides, research syntheses
- Location: 03-Resources/04-03-Methodology-Guides/
- Action: Update as practices evolve, never delete

**Seasonal**: Logs, analyses, reports
- Location: 99-System/10-Logs/ or domain-specific
- Action: Auto-delete old reports (~90 days), refresh on change

**Ephemeral**: Session notes, temp status, debug logs
- Location: Inline or 99-System/10-Logs/sessions/
- Action: Clean up regularly (~30 days)

**Context-specific**: Active project notes
- Location: Inside project directory
- Action: Archive on project completion

### Tag Vocabulary

Always include at least one tag from each category:

- **#type/**: `#type/skill`, `#type/note`, `#type/moc`, `#type/reference`
- **#domain/**: `#domain/vault`, `#domain/engineering`, `#domain/research`, `#domain/claude-code`
- **#topic/**: `#topic/documentation`, `#topic/code-quality`, `#topic/agentic-workflows`

### Writing Guidelines

**Structure**:
1. Title — clear, specific
2. Frontmatter — complete metadata
3. Context — why this document exists (1–2 sentences)
4. Main content — organized by section
5. Related resources — wikilinks to related docs
6. Last updated — timestamp and context

**Style**:
- Active voice, everyday language
- Short sentences over long explanations
- Code examples when appropriate
- Clear assumptions and limitations
- Include dates and versions for sourced claims

## Applied

- Vault: 2214 files, 96.9% have valid frontmatter
- Memory system: 81 active memory files with typed headers
- Skills: All 22+ skill pages include summary, sources, provenance

## Related Skills

- [[07-Wiki/03-skills/wikilink-standards|Wikilink Standards]]
- [[07-Wiki/03-skills/vault-structure|Vault Structure and Organization]]
