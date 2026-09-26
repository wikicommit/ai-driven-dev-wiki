---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/writing-tools-for-agents'
  hash: sha256:7541e4e46d675b2aed1175d9291d45d75f493ae908aea2afc77b29c615a324ea
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 7667
generated_pages:
  - .wikicommit/entity/en/BlogPosting/writing-effective-tools-for-agents.md
  - .wikicommit/entity/en/DefinedTerm/tool-namespacing.md
  - .wikicommit/entity/en/DefinedTerm/tool-use-design-pattern.md
failed_pages: []
---

## Summary

Anthropic's engineering guide to writing tools for LLM agents, built on the claim that a tool is a contract between a deterministic system and a non-deterministic one and so should not be written the way functions and APIs are written for other developers. The method it proposes is evaluation-driven: prototype the tools, build an evaluation from realistic multi-tool-call tasks with verifiable outcomes, run it as simple agentic loops, then paste the transcripts into Claude Code and let it analyse them and refactor the tools. It closes with five principles — build few consolidated tools rather than wrapping endpoints, namespace them, return high-signal context, bound response size, and prompt-engineer the descriptions — reporting a SWE-bench Verified result from description refinement and a retrieval-precision gain from resolving UUIDs into meaningful identifiers.

## Generation Notes

- "Ken Aizawa": excluded (privacy) — the named author of the source post, a living individual named by the source without being its subject, per entity-policy.md. The colleagues listed in the post's acknowledgements are a contributor roster and were not treated as entity candidates.
