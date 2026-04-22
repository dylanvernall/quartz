---
title: "Skill YAML Configuration Limits"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/skill-development", "#domain/vault"]
summary: "Only name and description YAML fields are read by Claude Code skill harness; other fields ignored."
sources: ["memory/feedback_skill_yaml_harness_limitations.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Skill YAML Configuration Limits

## Rule

When creating or updating SKILL.md files, include ONLY these YAML fields:
- `name` (required, used for skill identification)
- `description` (required, used for trigger phrase matching)

DO NOT include: `version`, `status`, `tags`, `created`, `modified` — these are silently ignored by the harness and create validation noise.

## Why

During skills library audit, added frontmatter with version/status/tags to three skills. IDE PostToolUse hook rejected them with "Attribute not supported" errors. Grep investigation revealed the harness only calls these two fields during skill loading. Extra fields don't break anything but add validation overhead and confusion.

## How to Apply

### When Creating New Skills

Include only `name` and `description` in YAML:

```yaml
---
name: skill-name
description: One-line description used for trigger matching
---
```

### When Updating Existing Skills

Remove unsupported fields (version, status, tags, created, modified) to pass pre-commit hooks.

### When Reviewing Skill PRs

Flag unnecessary YAML fields for cleanup during code review.

### Supported Fields (Observed)

The harness whitelist includes: argument-hint, compatibility, description, disable-model-invocation, license, metadata, name, user-invocable.

Use only these fields when additional configuration is needed.

## Applied

- Tested on: code-hypergraph-linting, systematic-lit-review, transcript-synthesis
- Cleaned up: 3 skill files with extraneous frontmatter
- Result: Pre-commit validation now passes

## Related Skills

- [[07-Wiki/03-skills/skill-modification-checklist|Skill Modification Checklist]]
- [[07-Wiki/03-skills/skill-modification-checklist|Skill Development Standards]]
