---
title: "N-Version Programming"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A fault-tolerance technique of independently generating multiple candidate solutions to the same task, cited as re-emerging in agentic software engineering as a way to increase the probability of a successful outcome and enable creative exploration through parallel agent-generated pull requests."
---

N-version programming is a practice, discussed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]], of generating multiple independent versions of a solution to the same task. The paper describes its re-emergence in Agentic Software Engineering: a team of agents can generate several candidate pull requests for the same ticket in parallel, which serves both as a form of inference-time compute that increases the probability of a successful outcome through trial and error, and as a means of creative exploration.

## Usage

In the paper's motivating example, a developer resolving seven tickets triggers an agent team to generate 28 candidate pull requests in parallel (four per ticket); the developer then selects the most promising candidate per ticket, or refines the specification and re-triggers the agents if none is acceptable. The paper states its proposed [[DefinedTerm/agent-command-environment]] (ACE) must support "disciplined N-version programming," letting a developer visualize, compare, and mix components from multiple agent-generated solutions. A [[DefinedTerm/loopscript]]'s task-decomposition-and-parallelization capability — assigning one [[DefinedTerm/briefingscript]] to multiple agents — is what the paper says makes N-version programming "routine," shifting the key metric from single-task latency to overall system throughput. It also notes N-version programming as a case where a coach's guidance may involve synthesizing a final solution from different agent-generated drafts (e.g. combining the UI from one solution with the backend logic from another).

## When It Applies

The paper treats N-version programming as an existing, decades-old fault-tolerance technique being repurposed for agentic coding rather than one it originates; it cites the practice's re-emergence as made practical by the ability to run multiple LLM-based agents (or heterogeneous teams of specialized agents, such as one model for high-level planning and another for detailed code generation) in parallel against the same specification.

## Related Terms

[[DefinedTerm/loopscript]], [[DefinedTerm/briefing-engineering]]
