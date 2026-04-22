---
title: "Permission Mode Autonomy — Switch to Auto"
created: 2026-04-20T00:00:00Z
modified: 2026-04-20T00:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/claude-code", "#topic/configuration", "#domain/claude-code"]
summary: "When a restrictive allowlist creates excessive permission prompts, switch bash/filesystem to auto mode while preserving deny rules."
sources: ["memory/feedback_permission_mode_autonomy_2026_04_20.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Permission Mode Autonomy — Switch to Auto

## Rule

When a 50+ entry allowlist in `settings.json` creates friction on every tool call, switch `bash.mode` and `filesystem.mode` from `"restricted"` to `"auto"`. Preserve all deny rules.

**Why**: Restricted mode uses an allow-list (everything blocked unless listed). Auto mode uses a deny-list (everything allowed unless denied). A 135-line manual allowlist signals that the allow-list model is the wrong fit — auto mode achieves the same safety via deny rules with zero permission prompts.

## Decision Gate

Switch to auto mode when:
- `bash.mode` or `filesystem.mode` is `"restricted"` AND
- The allowlist has 50+ entries AND
- The user or workflow is experiencing friction on routine tool calls

Keep restricted mode when:
- Project has strict security requirements
- Shared/multi-user environment
- Allowlist is small (<20 entries) and well-maintained

## Implementation

```bash
# Check current mode
jq '.permissions.bash.mode, .permissions.filesystem.mode' .claude/settings.json

# Apply switch (edit settings.json)
# bash.mode: "restricted" -> "auto"
# filesystem.mode: "restricted" -> "auto"

# For MCP filesystem, add write/rename to allowed_operations
# Keep "delete" in blocked_operations (security boundary)
```

## Settings Hierarchy

```
User settings (~/.claude/settings.json)     ← lowest priority
  Project settings (.claude/settings.json)  ← overrides user
    Local settings (.claude/settings.local.json) ← highest priority
```

If user-level `defaultMode: "auto"` is set but project overrides to `"restricted"`, the project setting wins — remove the project-level override to inherit user default.

## Safety Invariants to Preserve

Even in auto mode:
- `delete` stays in `blocked_operations`
- `denied_commands` list (destructive shell commands) stays
- `denied_paths` list (sensitive paths) stays
- Approval for push/PR creation stays (visible-to-others actions)

## Related

- [[07-Wiki/03-skills/configuration-consolidation.md|Configuration Consolidation]] — reducing settings file sprawl
