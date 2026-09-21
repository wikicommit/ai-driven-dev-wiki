---
title: "AutoGen"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, multi-agent, orchestration, agent-tooling]
sources:
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/agent/multi-agent/'
    hash: sha256:644e8c22de6fd778cefa3c3c44647eee3beb025a3fb81617e0411c473018e2c9
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A multi-agent conversation-orchestration framework in which several role-carrying agents exchange messages to reach an answer. Its documented patterns include a debate arrangement where solver agents argue over several rounds and an aggregator settles the result by majority vote. Microsoft merged it with Semantic Kernel into the Microsoft Agent Framework in 2025."
  applicationCategory: "Agent orchestration framework"
  featureList: "unified multi-agent conversation orchestration; debate pattern with solver and aggregator agents; majority voting over a final round's outputs; RoundRobin conversation mode; callback functions for logging each agent's decisions"
---

AutoGen is a framework providing unified orchestration of conversations between multiple LLM-driven
agents. Where [[SoftwareApplication/langgraph]] connects agents as a graph and
[[SoftwareApplication/crewai]] assembles them as a role-carrying team, AutoGen's organising idea in
the account given here is the conversation itself: agents are given roles and then talk to one
another until a result is reached.

## Capabilities

The source's worked example of role separation is a travel-planning arrangement in which a
`planner_agent` produces an initial plan, a `language_agent` supplies language advice, and a
`travel_summary_agent` consolidates the several perspectives into a final plan. Of these the source
maps the first to the Planner role of a [[DefinedTerm/llm-based-multi-agent-system]] and the second
to the Reviewer role; it illustrates the Orchestrator role from a different framework rather than
from this example.

Its documented answer to disagreement between agents is a **debate** pattern, in which agents
exchange positions over several rounds and correct one another. Solver agents propose answers and an
Aggregator agent collects them, settling the result by **majority vote** over the solvers' outputs
from the final round. The source presents this as one of three arbitration strategies available to
multi-agent systems generally, the others being confidence-weighted voting and trust-value routing;
majority voting is the one it describes AutoGen as documenting.

For conversation structure the source names a **RoundRobin** mode, and for traceability it notes that
callback functions can be used in AutoGen code to emit each agent's decision detail into a unified
log, so that a run's reasoning can be correlated afterwards.

## Adoption & Ecosystem

The source records that **Microsoft merged AutoGen with Semantic Kernel into
[[SoftwareApplication/microsoft-agent-framework]] in 2025**, ending a period in which the company
maintained two parallel multi-agent frameworks. It reads that consolidation as a signal that the
field has moved from competing on features to converging on a few projects teams are willing to
depend on, rather than migrating repeatedly between experimental ones.

## Related Terms

- [[SoftwareApplication/microsoft-agent-framework]] — what it and Semantic Kernel were merged into
- [[DefinedTerm/llm-based-multi-agent-system]] — the arrangement this framework coordinates
- [[SoftwareApplication/langgraph]] — the graph-structured alternative the same source compares it with
- [[SoftwareApplication/crewai]] — the role-based alternative the same source compares it with
