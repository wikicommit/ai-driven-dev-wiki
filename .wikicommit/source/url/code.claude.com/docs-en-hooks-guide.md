---
source:
  type: url
  url: 'https://code.claude.com/docs/en/hooks-guide'
  hash: sha256:155e5ab620eab496f8385a3e87ca54687af20c5b57321f14baee4017a74188b1

schema:
status: generated
last_generated_at: "2026-08-19"
extracted_tokens: 15406
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/agent-hooks.md
  - .wikicommit/entity/en/SoftwareApplication/claude-code.md
failed_pages: []
---

## Summary

Anthropic's Claude Code guide to hooks: user-defined commands that Claude Code runs at specific points in its lifecycle, offered as the deterministic alternative to instructions the model may or may not follow. It documents around thirty lifecycle events and what each one's matcher filters, five handler types (command, HTTP, MCP tool, a single-turn prompt hook, and an experimental agent hook), the stdin/stdout/exit-code contract and its structured-JSON alternative, how results from multiple matching hooks are combined, and the seven locations hook configuration can live in — including skill and subagent frontmatter.
