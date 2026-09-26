---
source:
  type: url
  url: 'https://simonwillison.net/2025/Sep/30/designing-agentic-loops/'
  hash: sha256:616bc39546fd4aab969e3a8ec0a6fa01330405714c063a028ab4419f84132964
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 3575
generated_pages:
  - .wikicommit/entity/en/BlogPosting/designing-agentic-loops.md
  - .wikicommit/entity/en/DefinedTerm/designing-agentic-loops.md
  - .wikicommit/entity/en/DefinedTerm/yolo-mode.md
  - .wikicommit/entity/en/DefinedTerm/sandboxing.md
failed_pages: []
---

## Summary

A blog post naming "designing agentic loops" as a distinct skill for working with coding agents: reducing a problem to a clear goal plus a set of tools an agent can iterate against, so the agent can brute-force its way to a solution. It works through the safety question this raises (the post's "YOLO mode", where every command is approved by default, and the three ways to survive it: a sandbox, someone else's computer, or accepting the risk), argues that shell commands usually beat MCP as the tools to expose, recommends issuing tightly scoped and budget-capped credentials, and identifies the problems worth this treatment as those with clear success criteria and tedious trial and error.

## Generation Notes

- "Simon Willison": excluded, privacy — the post's author, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. Not a relevance judgment: he is central to this source. No page exists for this entity.
- "Solomon Hykes": excluded, privacy — quoted in a single line ("An AI agent is an LLM wrecking its environment in a loop"), a living individual named only as the source of that quote. No page exists for this entity.
