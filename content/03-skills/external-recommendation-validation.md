---
title: "External Recommendation Validation"
created: 2026-04-14T10:00:00Z
modified: 2026-04-14T10:00:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/validation", "#topic/code-quality", "#domain/development"]
summary: "Vet ChatGPT/external tools before implementing; test findings on real codebase to avoid false positives and framework mismatches."
sources: ["memory/feedback_chatgpt_cleanup_claims_validation.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# External Recommendation Validation

## Rule

When receiving cleanup/tooling recommendations from external sources (ChatGPT, forums, etc.), always validate against your actual stack and existing tools before implementing.

## Why

External LLM advice is framework-correct but often repo-specific decisions are generic. The vault may not need 80% of the recommendations because:

1. Stack mismatch (advice for Node/React when you're Python/Markdown)
2. Existing tools already cover the gap
3. False positives in your specific codebase
4. Implementation friction (Windows CLI issues, missing binaries)

## How to Apply

### Validation Workflow

1. **Classify recommendations** by accuracy (correct in principle vs applicable to your stack)
2. **Test on real codebase** before committing to implementation
3. **Check for existing coverage** — does another tool already do this?
4. **Document findings** with verdict and reasoning

### Example: ChatGPT Claude Code Cleanup Claims

**Audit scope**: Vault-Lite is Python + Markdown (Obsidian), no root JS/TS.

**Result**: 7 claims accurate and applicable, 7 overstated/N/A.

#### ✅ Implemented: Vulture for Unused Python

**Verdict**: 100% correct.  
**Action**: Added to `.pre-commit-config.yaml` with 80% confidence threshold, non-blocking (warn-only).  
**Why**: Nothing in the current pre-commit hooks caught dead Python code across multiple projects.  
**Status**: ✓ Installed, tested cleanly on `99-System/02-Scripts/`.

#### ⏸ Deferred: lychee for External URL Checking

**Verdict**: Correct in principle, but implementation blocked.  
**Gap**: Existing link-decay hook checks wikilinks only; 95+ documentation files with external URLs never checked.  
**Blocker**: Python lychee wrapper on Windows has CLI issues; requires Rust binary install.  
**Status**: Commented out in `.pre-commit-config.yaml` with setup instructions for future enablement.

#### ❌ Rejected: Other Claims

| Claim | Verdict | Reason |
|---|---|---|
| Ruff (flake8 replacement) | Valid, not needed | flake8 + isort already working, no regression |
| Vale (prose linting) | Duplicate effort | Custom prose-slop-detector covers this |
| ast-grep, Knip, PMD CPD, jscodeshift | Not applicable | JS/Java-only; no root JS/TS in vault |
| Semgrep plugin | Already covered | security-credentials hook does this |

## Key Insight

LLM advice on tooling tends to be framework-correct but repo-agnostic. Always validate decision-making against:
- Your actual stack (not assumed stack)
- Existing tools (don't duplicate)
- Real codebase testing (not theory)

## Related Skills

- [[07-Wiki/03-skills/code-quality|Code Quality Standards]]
- [[07-Wiki/03-skills/pre-commit-strategy|Pre-Commit Hook Strategy]]
