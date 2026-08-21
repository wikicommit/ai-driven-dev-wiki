---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/building-effective-agents'
  hash: sha256:89d6d2e67b90631137ed1aba80dbebb0264d98646e0db9850e22d6a6c80c67cf

schema:
status: generated
last_generated_at: "2026-08-21"
extracted_tokens: 6563
generated_pages:
  - .wikicommit/entity/en/TechArticle/building-effective-agents.md
  - .wikicommit/entity/en/DefinedTerm/agentic-system.md
  - .wikicommit/entity/en/DefinedTerm/agent-computer-interface.md
  - .wikicommit/entity/en/DefinedTerm/multi-agent-orchestration.md
  - .wikicommit/entity/en/DefinedTerm/llm-as-judge.md
  - .wikicommit/entity/en/DefinedTerm/coding-agent.md
failed_pages: []
---

## Summary

Anthropic's guidance on building LLM agents, drawn from working with dozens of teams, whose headline finding is that the most successful implementations used simple composable patterns rather than complex frameworks. It separates workflows (LLMs and tools orchestrated through predefined code paths) from agents (LLMs directing their own processes), catalogues five workflow patterns — prompt chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer — plus the autonomous agent, and argues for the simplest solution that works, since agentic systems trade latency and cost for task performance. Its appendix on agent-computer interfaces argues tool formats and descriptions deserve as much design effort as human-computer interfaces.
