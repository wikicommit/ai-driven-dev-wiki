---
source:
  type: url
  url: 'https://zenn.dev/globis/articles/d0c73d2b176ba5'
  hash: sha256:d007e48e9860eef6953063dd12b23e8be1cf1576ddabcc4574d8a292c21d4357
  license:

schema:
status: partial
last_generated_at: "2026-09-22"
extracted_tokens: 2384
generated_pages:
  - .wikicommit/entity/en/BlogPosting/growing-ai-code-review-with-single-responsibility.md
  - .wikicommit/entity/en/DefinedTerm/code-review-agent.md
  - .wikicommit/entity/en/DefinedTerm/sub-agent-architecture.md
failed_pages: []
---

## Summary

A DevEx team at GLOBIS reports that a single general-purpose AI code reviewer produced enough off-target comments that teammates began ignoring it, and describes splitting the reviewer into many single-concern agents — applying the single responsibility principle to the reviewer itself — as the fix. Each agent is a Markdown file with YAML frontmatter under a Claude Code plugin, and the orchestrator selects one by reading its `description` field, so trigger conditions are expressed by writing that description concretely rather than configured separately. The post details two agents, one detecting flaky-test patterns and one detecting pagination without a unique order clause, and describes feeding past production failures back into the agents as accumulated knowledge.

## Generation Notes

- "emi084": excluded (privacy) — the post's bylined author, a named living individual; entity-policy.md rules out a page about a living individual, and the switch is on. No existing page.
