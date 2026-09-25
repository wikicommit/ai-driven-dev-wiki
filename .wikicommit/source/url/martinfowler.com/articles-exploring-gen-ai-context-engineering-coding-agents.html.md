---
source:
  type: url
  url: 'https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html'
  hash: sha256:5d6208219888475f13564a3c1495a0291ee1a06c40a75c10315de16798f766b5
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 4205
generated_pages:
  - .wikicommit/entity/en/BlogPosting/context-engineering-for-coding-agents.md
  - .wikicommit/entity/en/DefinedTerm/context-interfaces.md
failed_pages: []
---


## Summary

In this February 2026 "Exploring Gen AI" memo, Birgitta Böckeler gives a primer on the context configuration features of coding agents, separating reusable prompts (instructions and guidance) from what she calls context interfaces (tools, MCP servers, skills), and classifying features by who decides to load them: the LLM, a human, or the agent software. Using Claude Code's features as of January 2026 as the worked example (CLAUDE.md, rules, slash commands, skills, subagents, MCP servers, hooks, plugins), she recommends keeping context small and building it up gradually, lists the difficulties of sharing context configurations, and warns that context engineering offers only an illusion of control because outcomes remain probabilistic.

## Generation Notes

- "Birgitta Böckeler": excluded (privacy) — the article's author, a living individual named by the source without being its subject, per entity-policy.md.
- "Bharani Subramaniam": excluded (privacy) — a colleague of the author quoted for a one-line definition, a living individual named in passing, per entity-policy.md.
