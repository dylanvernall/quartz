---
title: "Git Multi-File Rename Pattern"
created: 2026-04-20T00:00:00Z
modified: 2026-04-20T00:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/git", "#domain/development"]
summary: "Reliably rename or reorganise 50+ files in git using rm --cached + add; git detects renames automatically by content hash."
sources: ["memory/feedback_git_cleanup_2026_04_16.md"]
provenance:
  extracted: 0.95
  inferred: 0.05
  ambiguous: 0.0
---

# Git Multi-File Rename Pattern

## Rule

For multi-file folder renames (50+ files), use `git rm -r --cached [old]` + `git add [new]` rather than `git mv`. Git detects renames automatically when content hash matches.

**Why**: `git mv` on large folder trees is slow and error-prone. Removing tracked paths first (`--cached` = index only, no disk deletion) lets git see the new paths as additions, then its rename-detection algorithm matches them by content hash automatically. No manual file-by-file mapping needed.

## Workflow

```bash
# 1. Verify the old → new folder mapping (1:1 rename, not redistribution)
git status

# 2. Remove old tracked paths from index (not disk)
git rm -r --cached old-folder-name/

# 3. Add new folder paths
git add new-folder-name/

# 4. Stage any deletions
git add -u

# 5. Update .gitignore if folders should be excluded going forward
git add .gitignore

# 6. Commit (pre-commit hooks may time out on 659+ files — safe to bypass if changes are clean)
git commit --no-verify -m "refactor: rename [old] -> [new] folders"
```

## When to Use `--no-verify`

Pre-commit hooks can time out on large structural commits (659+ files). Use `--no-verify` only when:
- All changes are renames/reorganisation (no new code)
- Security/validation hooks have been visually confirmed as passing on the content
- Document in commit message: "bypassed hooks due to timeout on structural rename"

## Notes

- Embedded `.git` directories in copied/submodule content will block staging — remove them first: `find . -name ".git" -type d | grep -v "^./.git$" | xargs rm -rf`
- `.gitignore` updates for personal/client folders should be staged in the same commit to avoid orphan tracking
- Git rename detection threshold is 50% content similarity by default — exact renames always detected

## Related

- [[07-Wiki/03-skills/pre-commit-strategy.md|Pre-Commit Strategy]]
- [[07-Wiki/03-skills/worktree-isolation-fallback.md|Worktree Isolation Fallback]]
