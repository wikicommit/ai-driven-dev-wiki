---
title: "Agno"
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
  description: "A multi-agent framework whose source says it emphasises high performance and efficiency, aimed at running large numbers of agents at once. The figures given for it are agent creation in microseconds and a memory footprint of a few kilobytes per agent."
  applicationCategory: "Agent orchestration framework"
  featureList: "multimodal support; very low per-agent creation time and memory footprint, aimed at high-volume concurrent agent workloads"
---

Agno is a framework for building [[DefinedTerm/llm-based-multi-agent-system]]s whose stated emphasis
is high performance and efficiency. Among the six coordination frameworks its source compares, it is
the one whose stated advantages are figures for what an individual agent costs to create and hold,
rather than a description of the workflow shapes it can express.

## Capabilities

The figures the source gives are agent creation in microseconds — around 2μs per agent — and a
memory footprint of roughly 3.75 KiB per agent. The first is given there as the project's own
official claim as of writing; the second is given without attribution. Neither states the hardware or
workload it was obtained on. The framework is also described as supporting multimodal.

## Adoption & Ecosystem

The source states that Agno suits all four of the architecture patterns it examines but is optimised
for high-performance scenarios where milliseconds matter, and it is the framework that account
matches to the **decentralised** pattern, in which agents communicate directly and make local
decisions with no central coordinator — an arrangement it describes as resilient but hard to make
globally consistent. Its stated best use is high-volume operation, the example given being a
real-time trading system analysing hundreds of stocks simultaneously.

Where a workload's first concern is lowering latency and raising throughput, the source names Agno's
or [[SoftwareApplication/langgraph]]'s parallel capabilities as likely the better fit; where the goal
is standing a team up quickly with clear responsibilities, it names [[SoftwareApplication/crewai]] as
the fastest route. That recommendation is presented there as a judgement, with no measurement given
in support of it.

The same chapter cautions against reaching for a framework of this kind at all where coordination
overhead would outweigh the gains from specialisation, and against building structure that a better
model would make redundant — advice that applies to Agno as to the rest of the set.

## Related Terms

- [[DefinedTerm/llm-based-multi-agent-system]] — the arrangement this framework coordinates
- [[DefinedTerm/decentralized-pattern]] — the architecture the source matches it to
- [[SoftwareApplication/langgraph]] — the alternative named for parallelism in the same comparison
