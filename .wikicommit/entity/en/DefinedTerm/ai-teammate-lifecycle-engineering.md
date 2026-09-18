---
title: "AI Teammate Lifecycle Engineering (ATLE)"
type: "schema:DefinedTerm"
lang: en
tags: [sase]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The engineering activity proposed in Structured Agentic Software Engineering (SASE) for giving agents persistent memory and long-term context, evolving them from stateless, one-off contractors into persistent teammates that learn and grow across tasks."
---

AI Teammate Lifecycle Engineering (ATLE) is one of the structured engineering activities proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] as part of [[DefinedTerm/structured-agentic-software-engineering]] (SASE), paired there with [[DefinedTerm/ai-teammate-infrastructure-engineering]] (ATIE) under the umbrella of "SE for Agents." Its stated purpose is to enable agents to retain memory and learn over time, moving them away from "one-off contractors" who start every task from scratch and toward "life-long partners" who retain institutional knowledge.

## Usage

The paper grounds ATLE in persistent memory — agents embedded with long-term memory of project history and decision logs, maintaining continuity across tasks without the coach repeatedly supplying the same guidance — citing the DeepWiki used by [[SoftwareApplication/devin]] as an early example of an agent building and referring to its own documentation and decision logs across tasks. It also covers proactive maintenance: an agent with persistent memory and codebase access scheduled during idle compute cycles to scan for technical debt, identify documentation gaps, or propose refactorings, with such proposals filed as new [[DefinedTerm/briefingscript]]s entering the standard workflow for human review. The paper's research roadmap for ATLE calls for mechanisms retaining project history, decision logs, and architectural rationale (both continual-learning methods and external memory structures such as graphs, vector stores, and decision records, with SE-specific compression to avoid overflowing context windows), research into scheduling and valuing proactive maintenance work without distracting teams from higher-priority development, and empirical and economic models — rather than anecdotes — of how agentic SE changes the cost model behind long-standing principles (e.g. code duplication becoming easier for agents to update consistently).

## Related Terms

[[DefinedTerm/ai-teammate-infrastructure-engineering]], [[DefinedTerm/agent-execution-environment]], [[DefinedTerm/structured-agentic-software-engineering]]
