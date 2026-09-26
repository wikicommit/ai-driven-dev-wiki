---
source:
  type: url
  url: 'https://hidekazu-konishi.com/entry/claude_code_hooks_complete_guide.html'
  hash: sha256:66f427a7be411fa79c42761b1304353ab4194737429bda9adf85af056786ff4a
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 16579
generated_pages:
  - .wikicommit/entity/en/BlogPosting/claude-code-hooks-complete-guide.md
  - .wikicommit/entity/en/DefinedTerm/agent-hooks.md
failed_pages: []
---

## Summary

Hidekazu Konishi's June 2026 guide treats hooks in Claude Code's CLI as a deterministic enforcement layer, contrasting them with prompts and CLAUDE.md, which the model follows only probabilistically. It walks through where each of roughly thirty hook events fires in a turn, how a hook answers through exit codes or JSON (with PreToolUse using a distinct permissionDecision shape), how matchers and the settings hierarchy scope hooks, and a set of worked examples. It closes by comparing hooks with permissions and CLAUDE.md and by setting out the security model and common pitfalls of hooks that run with the user's full shell privileges.

## Generation Notes

- "Hidekazu Konishi": excluded (privacy) — the guide's author, a living individual named by the source without being its subject, per entity-policy.md.
