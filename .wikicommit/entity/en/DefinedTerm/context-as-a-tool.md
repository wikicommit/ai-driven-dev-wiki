---
title: "Context as a Tool (CAT)"
type: "schema:DefinedTerm"
lang: en
aliases: ["CAT"]
tags: [context-management, coding-agents, long-horizon-tasks]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2512.22087'
    hash: sha256:3857d40229fe2714ee99e18d90dfd5603a1008977871861caf73748818d67851
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A context-management paradigm for LLM-based software engineering agents, proposed in a 2025 arXiv paper, that makes context maintenance a callable tool within the agent's decision-making so that the agent proactively compresses its history at appropriate milestones."
---

Context as a Tool (CAT) is a context-management paradigm, proposed in [[ScholarlyArticle/context-as-a-tool-context-management-for-long-horizon-swe-agents]], that elevates context maintenance to a callable tool integrated into an agent's decision-making process. It formalizes a structured context workspace consisting of stable task semantics, condensed long-term memory, and high-fidelity short-term interactions, and lets the agent proactively compress its historical trajectory into actionable summaries at appropriate milestones.

## Usage

The paper proposes CAT for software engineering agents that work over long horizons on repository-scale codebases, as an alternative to the append-only context maintenance and passively triggered compression heuristics it says most existing agents rely on. To train agents to use it, the authors propose a trajectory-level supervision framework, CAT-GENERATOR, built on an offline data-construction pipeline that injects context-management actions into complete interaction trajectories, and use it to train a context-aware model, SWE-Compressor.

## When It Applies

The paradigm is aimed at long-running interactions in which, according to its authors, append-only context and passive compression lead to context explosion, semantic drift and degraded reasoning. It assumes an agent trained to take context-management actions, which the authors supply through CAT-GENERATOR. Its support is a single paper's measured result: on SWE-Bench-Verified, SWE-Compressor reaches a 57.6% solved rate, which the authors report as significantly outperforming ReAct-based agents and static compression baselines while keeping reasoning stable under a bounded context budget.

## Related Terms

- [[DefinedTerm/compaction]] — summarizing a conversation's history to keep it within the context window
- [[DefinedTerm/context-engineering]] — the broader practice of managing what enters an agent's context
