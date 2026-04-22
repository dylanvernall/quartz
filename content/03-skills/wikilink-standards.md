---
title: "Wikilink Standards and Path Conventions"
created: 2026-04-15T00:02:00Z
modified: 2026-04-15T00:02:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/documentation", "#domain/vault"]
summary: "Absolute path wikilinks, MOC suffix conventions, and link validation patterns."
sources: [".claude/rules/wikilinks.md", "memory/feedback_wikilink_path_conversion.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Wikilink Standards and Path Conventions

## Rule

**Always use absolute paths from vault root. MOC links include `/_MOC` suffix. Never use relative paths or plain filenames.**

## Why

- **Ambiguity prevention**: Relative paths break when files move. Absolute paths are stable.
- **Consistency**: One true path for every document prevents duplicate index entries.
- **MOC discoverability**: `/_MOC` suffix signals index/navigation files in search and link analysis.
- **Tool compatibility**: Vault navigation scripts and link checkers expect absolute paths.

## How to Apply

### Absolute Path Pattern

**Format**: `` [[absolute/path/from/vault/root|Display Name]] ``

✓ `[[01-Projects/02-01-Coding/_MOC|Coding]]`
✗ `[[../Coding/_MOC|Coding]]` — relative
✗ `[[Coding]]` — ambiguous, no path

### MOC Suffix Convention

Master of Content (MOC) files index a domain. Always include `/_MOC` in the wikilink path (but NOT in the filename itself).

✓ Link format: `[[01-Projects/_MOC|Projects]]`
✓ File path: `01-Projects/_MOC.md` (the file is literally named `_MOC.md`)
✗ Link format: `[[01-Projects|Projects]]` — missing suffix, not recognized as index

### Sub-Domain Links

For deeper structures:

✓ `[[01-Projects/02-01-Coding/_MOC|Coding Projects]]`
✓ `[[01-Projects/02-02-Research/_MOC|Research Projects]]`
✗ `[[01-Projects/02-01-Coding|Coding Projects]]` — missing `/_MOC`

### Direct Document Links

Non-MOC documents: no suffix needed.

✓ `[[01-Projects/02-01-Coding/ralph/README.md|Ralph FastAPI Refactor]]`
✓ `[[03-Resources/04-02-References/Claude-Code-Cheatsheet|Claude Code Cheatsheet]]`
✗ `[[ralph/README.md|Ralph]]` — relative

### Link Validation

Run the link decay detector to find and fix broken links:

```bash
python 99-System/02-Scripts/link_decay_detector.py --report
```

This identifies:
- Broken wikilinks (targets don't exist)
- Missing MOC suffixes on index files
- Path inconsistencies
- Orphaned documents

### Common Mistakes

| Mistake | Fix |
|---------|-----|
| `[[../Skills|Skills]]` | `[[07-Wiki/03-skills/_MOC\|Skills]]` |
| `[[Skills]]` | `[[07-Wiki/03-skills/03-skills\|Skills]]` |
| `[[01-Projects]]` | `[[01-Projects/_MOC\|Projects]]` |
| `skill-name.md` plain text | `[[07-Wiki/03-skills/skill-name\|Skill Name]]` |

## Applied

- Vault: 85 MOC wikilinks in 02-Documentation/Claude/_MOC.md, all converted to absolute paths
- Wiki: 22 skill pages use absolute wikilinks to related skills
- Broken link detection: Zero broken wikilinks post-conversion

## Related Skills

- [[07-Wiki/03-skills/vault-structure|Vault Structure and Organization]]
- [[07-Wiki/03-skills/markdown-standards|Markdown Documentation Standards]]
