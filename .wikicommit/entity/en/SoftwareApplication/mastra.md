---
title: "Mastra"
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
  description: "A TypeScript-first multi-agent framework aimed at web developers, characterised by native TypeScript integration, working with existing REST APIs, graph-based workflows, and needing no separate AI infrastructure."
  applicationCategory: "Agent orchestration framework"
  featureList: "native TypeScript integration; works with existing REST APIs; graph-based workflows; requires no separate AI infrastructure"
---

Mastra is a TypeScript-first framework for designing [[DefinedTerm/llm-based-multi-agent-system]]s,
aimed at web developers. It is one of six coordination frameworks its source compares, and the
account it gives is about the environment the framework expects as much as about how it coordinates:
its stated advantages are native TypeScript integration, working with existing REST APIs,
graph-based workflows, and requiring no separate AI infrastructure to be stood up.

## Capabilities

The source's account of it is short and concerns fit rather than mechanism. Its stated best use is
web applications and TypeScript projects, and in the same chapter's mapping of frameworks onto
architecture patterns it is named — alongside [[SoftwareApplication/langgraph]] — as suited to the
**hybrid** pattern, which combines centralised control for global decisions with decentralised
execution for local optimisation. The parenthetical reason given for that match is that Mastra
combines business logic with the coordination flow.

## Adoption & Ecosystem

The source's framing of framework choice bears on Mastra as on the rest of the set: it argues the
choice is an architectural decision rather than a feature comparison, and that the coordination
frameworks on the market do not solve the underlying problem of selective, semantic context transfer
between agents — each either shares everything, which is slow and expensive, or shares summaries,
which lose detail. What a framework supplies is the mechanism; the coordination overhead remains the
thing to watch.

That chapter is descriptive throughout and reports no measurements or benchmarks of its own, and it
is the only source held here for this page.

## Related Terms

- [[DefinedTerm/llm-based-multi-agent-system]] — the arrangement this framework coordinates
- [[SoftwareApplication/langgraph]] — the framework named alongside it for the same architecture pattern
- [[SoftwareApplication/crewai]] — the role-based alternative in the same comparison
