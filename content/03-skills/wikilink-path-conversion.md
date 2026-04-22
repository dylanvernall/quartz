---
title: "Wikilink vs Filesystem Path Handling"
created: 2026-04-14T15:45:00+12:00
modified: 2026-04-14T15:45:00+12:00
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/vault-architecture", "#topic/file-operations"]
sources: ["memory/feedback_wikilink_path_conversion.md"]
summary: "Convert wikilink syntax to filesystem paths before file creation to avoid malformed UTF-8 filenames and git pollution."
provenance: "extracted: 1.0"
---

## Rule: Always Convert Wikilink Syntax to Filesystem Paths

**Why:** Wikilink syntax (vault navigation format using square brackets) is meant for navigating, not for filesystem paths. Passing wikilink format directly to file write operations creates malformed UTF-8 filenames with encoding characters instead of proper filesystem paths, polluting git with unintended files.

**How to apply:**

1. **Detection** — If path contains double square brackets or pipe separators, it's in wikilink format
2. **Conversion** — Strip wikilink formatting:
   - Remove opening and closing brackets
   - Remove pipe character and display name suffix
   - Keep only the path portion (e.g., `01-Projects/02-01-Coding/_MOC`)
3. **Validation** — Verify result is valid filesystem path (no special characters, valid separators)
4. **Error handling** — If path conversion fails, log error and skip file creation with message to user

### Example of Problem

Do NOT convert Windows absolute paths through wikilink syntax. Using a Windows file path (e.g., C:\Users\name\.claude\...\memory.md) inside wikilink format will create a malformed UTF-8 filename with encoding characters instead of a proper filesystem path. Always use vault-relative paths only.

### Correct Handling

```
Input path: C:\Users\dv\.claude\projects\c--Vault-Lite\memory\MEMORY.md
Alternative: C:\Vault-Lite\memory\MEMORY.md (relative to vault root)
Output: Direct filesystem write to actual path, no formatting wrappers
```
