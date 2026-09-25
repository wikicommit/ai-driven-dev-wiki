---
title: "NL2Repo-Bench"
type: "schema:Dataset"
lang: en
aliases: ["NL2Repo Bench"]
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
  description: "A benchmark for evaluating the long-horizon repository generation ability of coding agents, in which an agent must build a fully installable Python library from a single natural-language requirements document and an empty workspace."
---

NL2Repo-Bench is a benchmark, introduced in [[ScholarlyArticle/nl2repo-bench-towards-long-horizon-repository-generation-evaluation-of-coding-agents]], that is designed to evaluate the long-horizon repository generation ability of coding agents — whether they can sustain coherent reasoning, planning and execution long enough to build a complete software repository rather than a localized piece of code.

## Contents

Each task gives an agent only a single natural-language requirements document and an empty workspace. From that, the agent must autonomously design the architecture, manage dependencies, implement multi-module logic, and produce a fully installable Python library. Results are reported as test pass rates, which the paper describes as making the benchmark a verifiable testbed.

## Use

[[ScholarlyArticle/nl2repo-bench-towards-long-horizon-repository-generation-evaluation-of-coding-agents]] evaluates state-of-the-art open- and closed-source models on the benchmark and reports that even the strongest agents achieve below 40% average test pass rates and rarely complete an entire repository correctly. It identifies failure modes including premature termination, loss of global coherence, fragile cross-file dependencies, and inadequate planning over hundreds of interaction steps.
