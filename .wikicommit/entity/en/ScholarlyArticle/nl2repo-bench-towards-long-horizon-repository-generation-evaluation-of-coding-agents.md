---
title: "NL2Repo-Bench: Towards Long-Horizon Repository Generation Evaluation of Coding Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, benchmarks, long-horizon-tasks]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2512.12730'
    hash: sha256:d919d03051da310695fcac6050d2075a19b250259683895f607de562dac04173
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A 2025 arXiv paper presenting NL2Repo-Bench, a benchmark for evaluating whether coding agents can build a complete, installable Python library from a single natural-language requirements document, and reporting that long-horizon repository generation remains largely unsolved."
  datePublished: "2025-12-14"
  keywords: ["coding agents", "repository generation", "long-horizon evaluation", "benchmark"]
---

The paper argues that although recent coding agents suggest rapid progress toward autonomous software development, existing benchmarks do not rigorously evaluate the long-horizon capabilities needed to build complete software systems. Most prior evaluations, it says, focus on localized code generation, scaffolded completion or short-term repair tasks, leaving open whether agents can sustain coherent reasoning, planning and execution over the extended horizons that real-world repository construction demands.

To address this it presents [[Dataset/nl2repo-bench]], a benchmark explicitly designed to evaluate the long-horizon repository generation ability of coding agents. Given only a single natural-language requirements document and an empty workspace, an agent must autonomously design the architecture, manage dependencies, implement multi-module logic and produce a fully installable Python library. Experiments across state-of-the-art open- and closed-source models lead the authors to conclude that long-horizon repository generation remains largely unsolved.

## Key Points

- In the benchmark's task setting, an agent receives only a natural-language requirements document and an empty workspace, and must produce a fully installable Python library.
- Even the strongest agents evaluated achieve below 40% average test pass rates and rarely complete an entire repository correctly.
- The authors' analysis identifies long-horizon failure modes including premature termination, loss of global coherence, fragile cross-file dependencies, and inadequate planning over hundreds of interaction steps.
- The authors present the benchmark as a rigorous, verifiable testbed for sustained agentic competence, and identify long-horizon reasoning as a central bottleneck for the next generation of autonomous coding agents.

## Notes

The paper was first submitted to arXiv on 14 December 2025 and revised on 8 January 2026 (version 2). It lists 49 authors and is filed under Computation and Language (cs.CL).
