---
title: "Verification Debt"
type: "schema:DefinedTerm"
lang: en
tags: [agents, verification, software-process]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.20456'
    hash: sha256:fcf0fa7c744985d64d3d71a71e82e882a7ad1f5133fca691f23cb211cd7ae8b3
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The backlog a team accumulates when an agent's output of code, tests, documentation and patches grows faster than the team's capacity to verify it, leaving weak tests, hidden regressions, broad patches, unvalidated dependencies and increased reviewer burden."
---

Verification debt is the shortfall that accumulates when agentic AI increases the volume of code, tests, documentation and patches faster than a team's capacity to verify that output. Koch defines the term in [[ScholarlyArticle/agentic-agile-v]] and enumerates what it consists of: weak tests, hidden regressions, broad patches, unvalidated dependencies, undocumented behaviour and increased reviewer burden. The underlying observation is that agentic systems can generate plausible engineering artifacts faster than humans can inspect them, so the bottleneck moves from code synthesis to specification quality, execution context, verification, traceability and controlled iteration.

## Usage

The term is used to explain why measured productivity gains from AI assistance can fail to materialise. Koch relays a randomized trial in which AI tools increased task completion time for experienced developers working in mature repositories, and separate research suggesting AI-assisted output shifts review and rework load toward experienced developers, and reads the two together as evidence that review and cleanup can erase perceived speedups.

Its severity is argued to depend on domain: in hardware and embedded work Koch states that verification debt can become operational or physical risk. He separately describes those domains as having stricter failure modes, since incorrect pin mappings, register values, timing assumptions, bus behaviour, reset handling or memory layout can produce failures that are costly or unsafe, and holds that there compilation is not proof. The concept is the motivation for the acceptance side of [[DefinedTerm/agentic-agile-v]]: risk-adaptive gates and evidence bundles exist so that agent output is accepted on evidence proportionate to its risk rather than on plausibility.

## When It Applies

The condition Koch states is a comparison of rates: teams accumulate verification debt if output volume grows faster than verification capacity. He separately lists test coverage, dependency setup and verification cost among the factors that decide whether agents help or hurt on a given task. Among the implications he draws for teams adopting agentic development are keeping tests inside the agent loop rather than after it, separating implementation and verification agents where risk is high, and tracking review load, defect escape, rework and lead time rather than code volume alone.

The term is one author's framing in a synthesis paper rather than a measured quantity with an established metric. Koch offers no way to measure verification debt directly, and lists among his open research questions whether evidence bundles can reduce it without eliminating productivity gains — so the concept is best read as a lens on existing productivity and maintenance-burden findings rather than as something independently established.

## Related Terms

[[DefinedTerm/agentic-agile-v]], [[ScholarlyArticle/agentic-agile-v]], [[DefinedTerm/cognitive-debt]], [[DefinedTerm/the-70-percent-problem]]
