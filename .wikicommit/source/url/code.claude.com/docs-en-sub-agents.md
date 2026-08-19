---
source:
  type: url
  url: 'https://code.claude.com/docs/en/sub-agents'
  hash: sha256:12cc07fa94c1e50e47e202b2d565884e44401d3bce47e2e2c8dc5598cb57f87a

schema:
status: generated
last_generated_at: "2026-08-19"
extracted_tokens: 24631
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/subagents.md
  - .wikicommit/entity/en/SoftwareApplication/claude-code.md
failed_pages: []
---

## Summary

Anthropic's Claude Code documentation on subagents: specialized assistants that run in their own context window with their own system prompt, tools and permissions. It sets out the built-in agents (Explore, Plan, general-purpose, and helper agents), the five-level scope precedence for custom definitions, exactly what does and does not load into a fresh subagent's context, resumption via messaging, nesting and concurrency limits, worktree isolation, and forks — subagents that deliberately inherit the whole parent conversation instead of starting fresh.
