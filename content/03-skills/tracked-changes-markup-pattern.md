---
title: "Tracked-Changes Markup Pattern"
created: 2026-04-14T15:47:00+12:00
modified: 2026-04-14T15:47:00+12:00
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/documentation", "#topic/versioning"]
sources: ["~/.claude/projects/c--Vault-Lite/memory/feedback_tracked_changes_markup_pattern.md"]
summary: "Use HTML <ins>/<del> tags to mark document changes for visual tracking; manage linting conflicts with .markdownlintignore."
provenance: "extracted: 1.0"
---

## Rule: HTML Tags for Tracked Changes in Markdown

**Why:**
- Standard `<ins>` renders as underlined in Markdown/Obsidian
- Standard `<del>` renders as strikethrough
- More readable than comment-based alternatives or custom syntax
- Works well for comparing AI-revised documents or versioned content
- Renders cleanly in web/Obsidian without additional tooling

**How to apply:**

### 1. For Additions/New Content

```markdown
<ins>This text was added</ins>
```

### 2. For Deletions/Removed Content

```markdown
<del>This text was removed</del>
```

### 3. For Replacements (Combine Both)

```markdown
Changed from <del>old text</del> to <ins>new text</ins>
```

### 4. For Multi-line Changes

Wrap entire sections:
```markdown
<ins>### 5.1 New Section

Content of new section goes here with full formatting.
</ins>
```

### 5. Managing Linting Conflicts

- Markdownlint (MD033) rejects inline HTML by default
- For external deliverables/OneDrive docs: Add pattern to `.markdownlintignore`:
  ```
  OneDrive*/**/*.md
  ```
- For committed vault documents: Use `--no-verify` with clear rationale in commit message

## When NOT to Use

- Core vault/project documentation (keep those linter-compliant)
- Deliverables intended for print/PDF (HTML tags may not render)
- When client has strict style requirements (check first)

## Companion Action

Always include a summary block at top of document explaining revision history (e.g., "Changes from Original" section with bullet list of major changes).
