---
title: "Tracked Changes Markup Pattern"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/markdown", "#topic/document-editing"]
summary: "Mark document changes with HTML <ins>/<del> tags for tracked-changes style visualization without custom tools. Renders as underline/strikethrough in Obsidian."
sources: ["memory/feedback_tracked_changes_markup_pattern.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Tracked Changes Markup Pattern

## Rule: Use HTML Tags for Document Change Tracking

Use `<ins>` and `<del>` HTML tags in Markdown to mark additions and deletions, creating a tracked-changes effect similar to Microsoft Word without requiring external tools.

**Why:**
- Standard `<ins>` renders as underlined in Markdown/Obsidian reading view
- Standard `<del>` renders as strikethrough
- More readable than comment-based alternatives or custom syntax
- Works cleanly for comparing AI-revised documents or versioned content
- Renders in web and Obsidian reading mode without additional tooling

## How to Apply

### For additions/new content:
```markdown
<ins>This text was added</ins>
```

### For deletions/removed content:
```markdown
<del>This text was removed</del>
```

### For replacements (combine both):
```markdown
Changed from <del>old text</del> to <ins>new text</ins>
```

### For multi-line changes:
```markdown
<ins>### 5.1 New Section

Content of new section with full formatting.
</ins>
```

## Handling Linting Conflicts

Markdownlint (MD033) rejects inline HTML by default.

**For external deliverables** (OneDrive, client documents): Add pattern to `.markdownlintignore`:
```
OneDrive*/**/*.md
```

**For committed vault documents**: Use `--no-verify` with clear rationale in commit message explaining why HTML tags are necessary and that the document is external.

## When NOT to Use

- Core vault/project documentation (keep linter-compliant)
- Deliverables for print/PDF (HTML may not render)
- When client has strict style requirements (check first)

## Companion Action

Always include a summary block at top of document explaining revision history:

```markdown
## Changes from Original

- Added section 4.2 on new methodology
- Removed deprecated API endpoints (section 3.1)
- Updated figures 2–5 with 2026 data
```

## Related Skills

- [[07-Wiki/03-skills/markdown-standards|Markdown Standards]]
- [[07-Wiki/03-skills/vault-structure|Vault Structure & Organisation]]
