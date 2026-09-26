---
source:
  type: url
  url: 'https://www.anthropic.com/research/building-effective-agents'
  hash: sha256:611504eb30423330be060ed8f00e432a0adcb417f992b2cfb5cbf9ccd8d511bf
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 6571
generated_pages:
  - .wikicommit/entity/en/BlogPosting/building-effective-agents.md
  - .wikicommit/entity/en/DefinedTerm/augmented-llm.md
  - .wikicommit/entity/en/DefinedTerm/ai-agent.md
failed_pages: []
---

## Summary

Anthropic's account of what worked across dozens of customer teams building LLM agents, whose headline finding is negative: the most successful implementations used simple, composable patterns rather than complex frameworks or specialized libraries. It groups everything under "agentic systems" and separates workflows (LLMs and tools orchestrated through predefined code paths) from agents (the LLM directing its own process and tool usage), then inventories five workflow patterns — prompt chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer — plus the autonomous agent, built up from the augmented LLM as foundational building block. Its standing advice is to start with LLM APIs directly, find the simplest solution possible, and add complexity only when it demonstrably improves outcomes; a note records that much of the tooling landscape it describes has changed since December 2024.

## Generation Notes

- "Erik S.", "Barry Zhang": excluded (privacy) — the named authors of the source post; living individuals named by the source without being its subject, per entity-policy.md.
