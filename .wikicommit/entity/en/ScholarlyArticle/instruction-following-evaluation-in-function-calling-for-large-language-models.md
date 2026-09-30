---
title: "Instruction-Following Evaluation in Function Calling for Large Language Models"
type: "schema:ScholarlyArticle"
lang: en
tags: [function-calling, benchmarks, evaluation, instruction-following]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.18420'
    hash: sha256:b8a9e39c6857fbac6ae53a52d3e2e3d60b5b0399ba0aa6f9a8dfc3350061e1a6
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A preprint introducing IFEval-FC, a benchmark that checks whether LLMs follow verifiable format instructions embedded in the parameter descriptions of JSON function schemas, and finding that even state-of-the-art models frequently fail them."
  author: ["Nikolai Skripko"]
  datePublished: "2025-09-24"
---

This short preprint, from the Higher School of Economics and SberDevices in Moscow, points to a gap in
how [[DefinedTerm/function-calling]] is evaluated. Existing benchmarks such as the
[[Dataset/berkeley-function-calling-leaderboard]], τ2-Bench and ACEBench, the author argues, evaluate
argument correctness or API selection but do not test whether a model adheres to format instructions
embedded in parameter descriptions — for example enclosing values in double quotes, using ISO date
formats, or starting a name with a capital letter. Such instructions are simple, yet frequently
overlooked or misinterpreted by LLMs, which leads to invalid function calls and downstream failures in
agent workflows.

To measure this, the paper introduces [[Dataset/ifeval-fc]], a benchmark inspired by IFEval that
embeds objectively verifiable format instructions directly in the description field of one parameter of
a JSON schema and scores the resulting function call with algorithmic checks rather than human or
LLM-as-a-judge assessment. It contains 750 test cases, each a function with an embedded format for one
of its input parameters and a corresponding user query.

## Key Points

- Existing function-calling benchmarks, according to the author, evaluate functional correctness or API
  selection but overlook whether arguments are correctly formatted, leaving a dimension of agent
  robustness under-evaluated.
- Even state-of-the-art proprietary models such as GPT-5 and Claude Opus 4.1 frequently fail to adhere
  to basic formatting rules in function calls.
- The latest models perform significantly better than their predecessors, but no evaluated model
  surpassed 80% accuracy, which the author takes to mean precise instruction following in function
  calling remains an open problem despite being trivial for humans.
- During dataset construction, Anthropic's most recent models such as Claude Opus 4.1 refused to call a
  function significantly more often than other models, often asking the user for clarification when
  subtle uncertainties arose; the benchmark adds a system message instructing the model always to call
  a function.
- Trivial case constraints such as all-uppercase or all-lowercase reached 90-100% accuracy across
  models during development and were excluded from the final evaluation to keep the benchmark
  discriminative.

## Notes

The author notes that in the current setup only one function is available for the model to call, and
plans to make the benchmark harder by adding more functions — so that the model must first select the
correct one — and by selecting more difficult samples; multilingual support modelled on M-IFEval is
another stated direction. The code and data are published at <https://github.com/Skripkon/IFEval-FC>.
