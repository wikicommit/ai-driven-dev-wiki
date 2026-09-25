---
title: "Context as a Tool: Context Management for Long-Horizon SWE-Agents"
type: "schema:ScholarlyArticle"
lang: en
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
  description: "A 2025 arXiv paper proposing CAT, a context-management paradigm that makes context maintenance a callable tool for long-horizon software engineering agents, together with a trajectory-level supervision framework used to train a context-aware model, SWE-Compressor."
  author: ["Shukai Liu", "Jian Yang", "Bo Jiang", "Yizhi Li", "Jinyang Guo", "Xianglong Liu", "Bryan Dai"]
  datePublished: "2025-12-26"
  keywords: ["context management", "SWE agents", "long-horizon reasoning", "context compression"]
---

The paper addresses agents based on large language models working on real-world software engineering tasks that require long-horizon interaction with repository-scale codebases. It argues that most existing agents rely on append-only context maintenance or passively triggered compression heuristics, which often lead to context explosion, semantic drift and degraded reasoning in long-running interactions.

In response it proposes [[DefinedTerm/context-as-a-tool]] (CAT), a context-management paradigm that elevates context maintenance to a callable tool integrated into the agent's decision-making. To support context management for software engineering agents, the authors also propose a trajectory-level supervision framework, CAT-GENERATOR, and use it to train a context-aware model, SWE-Compressor, which they evaluate on [[Dataset/swe-bench-verified]].

## Key Points

- CAT formalizes a structured context workspace made up of stable task semantics, condensed long-term memory, and high-fidelity short-term interactions.
- Under CAT, agents proactively compress historical trajectories into actionable summaries at appropriate milestones, rather than relying on passively triggered compression.
- CAT-GENERATOR is based on an offline data-construction pipeline that injects context-management actions into complete interaction trajectories.
- On SWE-Bench-Verified, SWE-Compressor reaches a 57.6% solved rate and, according to the authors, significantly outperforms ReAct-based agents and static compression baselines while maintaining stable long-horizon reasoning under a bounded context budget.

## Notes

The paper was submitted to arXiv on 26 December 2025 and is listed under Computation and Language (cs.CL).
