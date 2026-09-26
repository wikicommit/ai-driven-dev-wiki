---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/multi-agent-research-system'
  hash: sha256:9d24a3bfa582cdeb35b5470314362e43ded1cceb6659830329c69fe72147a2e4
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 8209
generated_pages:
  - .wikicommit/entity/en/BlogPosting/how-we-built-our-multi-agent-research-system.md
  - .wikicommit/entity/en/DefinedTerm/sub-agent-architecture.md
  - .wikicommit/entity/en/DefinedTerm/llm-as-a-judge.md
failed_pages: []
---

## Summary

Anthropic's engineering account of its Research feature, built as an orchestrator-worker multi-agent system in which a lead agent plans, spawns subagents that search in parallel with their own context windows, and synthesises what they return. It reports a 90.2% improvement over a single-agent baseline on an internal research eval, attributes most of the measured performance variance on BrowseComp to token usage, and states the cost plainly at roughly 15x the tokens of a chat — while naming domains it considers a poor fit, most coding tasks among them. The rest covers the prompt-engineering principles that made delegation work, how to evaluate a system that never takes the same path twice, and the production problems that followed: compounding errors in stateful agents, non-deterministic debugging, rainbow deployments, and a synchronous-execution bottleneck.

## Generation Notes

- "Jeremy Hadfield", "Barry Zhang", "Kenneth Lien", "Florian Scholz", "Jeremy Fox", "Daniel Ford": excluded (privacy) — the named authors of the source post; living individuals named by the source without being its subject, per entity-policy.md.
