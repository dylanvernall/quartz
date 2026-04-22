---
title: "Wikilink Path Conversion"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/vault-structure", "#topic/automation"]
summary: "Convert wikilink syntax to filesystem paths before file operations. Wikilinks [[path|display]] are vault navigation syntax — direct use creates malformed UTF-8 filenames with encoding characters."
sources: ["memory/feedback_wikilink_path_conversion.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Wikilink Path Conversion

## Rule: Always Convert Wikilinks to Filesystem Paths

Wikilink syntax (e.g., `[[01-Projects/02-01-Coding/_MOC|Display Name]]`) is Obsidian vault navigation syntax, not filesystem paths. Passing wikilinks directly to file write operations creates malformed UTF-8 filenames.

**Why**: When wikilink syntax is passed to file creation without conversion, special characters (pipes, brackets) get encoded as UTF-8 escape sequences (e.g., `\uf03a` for colons). This pollutes git with unintended files that cannot be easily cleaned up.

## How to Apply

### Detection

Identify when a path contains wikilink syntax:
- Contains double brackets: `[[...]]`
- Contains pipe character: `|DisplayName`
- Mixed with filesystem separators: `C:\path\[[nested|display]]`

### Conversion Process

1. **Remove brackets**: Strip `[[` and `]]`
   ```
   [[01-Projects/02-01-Coding/_MOC]] → 01-Projects/02-01-Coding/_MOC
   ```

2. **Remove display name**: Strip `|DisplayName` suffix
   ```
   [[path/to/file|Custom Display]] → path/to/file
   ```

3. **Keep path only**: Result should be a valid filesystem path
   ```
   01-Projects/02-01-Coding/_MOC
   C:\Vault-Lite\07-Wiki\03-skills\page.md
   ```

4. **Validate**: Ensure result contains no special characters or invalid separators

### Error Handling

If path conversion fails:
- Log error with original wikilink and reason
- Skip file creation
- Report to user with clear message

## Real-World Incident

Session 2026-03-19:
```
Input wikilink: [[C:\Users\dv\.claude\projects\c--Vault-Lite\memory\MEMORY.md|Memory Index]]
Malformed output: C\357\200\272Usersdv.claudeprojectsc--Vault-LitememoryMEMORY.md
  (UTF-8 character \uf03a encoded as \357\200\272)
```

Git status showed 2 untracked malformed filenames that should not have been created.

## Related Skills

- [[07-Wiki/03-skills/vault-structure|Vault Structure & Organisation]]
- [[07-Wiki/03-skills/wikilink-standards|Wikilink Standards]]
