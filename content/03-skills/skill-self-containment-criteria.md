---
title: "Skill Self-Containment Criteria"
created: 2026-04-20T00:00:00Z
modified: 2026-04-20T00:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/skill-development", "#domain/claude-code"]
summary: "Criteria for determining whether a Claude Code skill is self-contained enough to publish externally (no Vault-Lite path dependencies)."
sources: ["memory/project_claude_skills_publication_2026_04_17.md"]
provenance:
  extracted: 0.85
  inferred: 0.15
  ambiguous: 0.0
---

# Skill Self-Containment Criteria

## Rule

A skill is publishable (self-contained) if it has **no functional dependency on vault-specific paths** (`00-Inbox/`, `01-Projects/`, etc.). Wikilinks in "Related Resources" sections are cosmetic and do not block publication.

**Why**: Skills that reference vault-internal paths break for users without that exact vault structure. The distinction between functional paths (used in logic/commands) and cosmetic links (documentation only) determines portability.

## Self-Containment Test

| Dependency Type | Publishable? | Action |
|---|---|---|
| No vault paths referenced | Yes | Publish as-is |
| Vault paths in "Related" wikilinks only | Yes | Include — cosmetic only |
| Vault paths in commands/scripts/logic | No | Parameterise or remove |
| Depends on vault-specific MCP servers | No | Mark vault-only |
| Depends on vault data files | No | Mark vault-only |

## Examples from 2026-04-17 Publication

**Published (39 skills)**: agent-development, autoresearch, code-reviewer, tech-debt, hallucination-detector, skill-creator, systematic-lit-review, session-wrap-up, etc.

**Excluded (16 vault-specific)**:
- `openspace-delegate` — depends on OpenSpace MCP server
- `obsidian-markdown`, `json-canvas` — vault format skills
- `commit-push-pr` — depends on vault git workflow
- `claude-history-ingest`, `notebooklm` — vault infrastructure skills
- `data-analysis-skills`, `machine-learning-skills` — vault data paths

## Sync Strategy

After publication, keep vault source and published repo in sync by:
1. Comparing file timestamps between vault `skills/` and repo
2. Copying updated Python scripts from vault source to repo
3. Commit sync changes immediately (don't accumulate drift)

Published repo: `https://github.com/dylanvernall/Claude-Skills`

## Related

- [[07-Wiki/03-skills/skill-modification-checklist.md|Skill Modification Checklist]]
- [[07-Wiki/03-skills/skill-yaml-limits.md|Skill YAML Limits]]
