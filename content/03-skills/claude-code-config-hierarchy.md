---
title: "Claude Code Configuration Hierarchy"
created: 2026-04-20T00:00:00Z
modified: 2026-04-20T00:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/claude-code", "#topic/configuration", "#domain/claude-code"]
summary: "Hierarchical Claude Code config pattern: root CLAUDE.md → .claude/rules/ (path-scoped) → project CLAUDE.md — enables scoped overrides without cluttering global standards."
sources: ["memory/project_claude_code_restructure_2026_03_25.md"]
provenance:
  extracted: 0.9
  inferred: 0.1
  ambiguous: 0.0
---

# Claude Code Configuration Hierarchy

## Pattern

Organise Claude Code instructions in three tiers for clean separation of concerns:

```
root CLAUDE.md          ← Global standards (72% reduction via compression)
  .claude/rules/        ← Path-scoped rules (6 rule files)
    wikilinks.md
    code-quality.md
    documentation.md
    context-management.md
    agent-patterns.md
    research-workflow.md
  01-Projects/.../CLAUDE.md  ← Domain-specific overrides
    ralph/CLAUDE.md     ← FastAPI patterns
    lit-review/CLAUDE.md ← SLR pipeline
```

**Why**: A monolithic root CLAUDE.md bloats to 277+ lines and provides generic context where domain-specific context is needed. Path-scoped rules are only activated for files matching their `paths` frontmatter field — Ralph gets FastAPI context without polluting global standards.

## Rule Files Structure

Each `.claude/rules/` file uses simplified frontmatter (no standard 7-field requirement):
```yaml
---
title: "Rule Title"
paths: ["01-Projects/02-01-Coding/**", "specific/path"]
---
```

## Compression Result

- Root CLAUDE.md: 277 → 77 lines (72% reduction)
- 6 rules files created for domain separation
- Project CLAUDE.md files for Ralph and lit-review
- MCP servers enabled: notebooklm, zotero

## When to Create a Rules File

Create a new `.claude/rules/X.md` when:
- A domain has 3+ distinct standards not relevant to other domains
- Multiple projects share the same domain (reuse via path matching)
- Root CLAUDE.md has grown past 100 lines (compression signal)

## Related

- [[07-Wiki/03-skills/configuration-consolidation.md|Configuration Consolidation]] — settings.json patterns
- [[07-Wiki/03-skills/permission-mode-autonomy.md|Permission Mode Autonomy]]
