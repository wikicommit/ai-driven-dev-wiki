---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/multi-agent-research-system'
  hash: sha256:f9af507dbe72a9650f1c11cf6ae2aa13e7f9c2f6c3a7436129197c31ddb3a3bc

schema:
status: generated
last_generated_at: "2026-08-21"
extracted_tokens: 8202
generated_pages:
  - .wikicommit/entity/en/TechArticle/how-we-built-our-multi-agent-research-system.md
  - .wikicommit/entity/en/DefinedTerm/multi-agent-orchestration.md
  - .wikicommit/entity/en/DefinedTerm/subagents.md
  - .wikicommit/entity/en/DefinedTerm/llm-as-judge.md
  - .wikicommit/entity/en/DefinedTerm/agent-computer-interface.md
failed_pages: []
---

## Summary

Anthropic's engineering account of taking a multi-agent Research feature from prototype to production, using an orchestrator-worker architecture in which a lead agent plans and spawns parallel subagents. It reports a 90.2% improvement over a single-agent baseline on an internal research eval while stating the cost plainly — multi-agent systems use roughly 15x the tokens of chat — and names most coding tasks as a poor fit today because they involve fewer truly parallelisable subtasks. It sets out eight prompting principles for orchestration, argues evaluation must judge outcomes and process rather than prescribed steps, and describes the production engineering that non-determinism forces: resumable execution, full tracing, and rainbow deployments.
