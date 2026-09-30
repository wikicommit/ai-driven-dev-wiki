---
title: "When2Tool"
type: "schema:Dataset"
lang: en
tags: [agents, tool-use, benchmarks]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.09252'
    hash: sha256:7d08538d9f45eb05bc7d8ea511fcfef0aca596fc3189f3397a075cc61cb6838e
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A benchmark of 18 tool-use environments for studying whether an LLM agent knows when it needs to call a tool, with easy, medium and hard difficulty levels that place a decision boundary between tasks that do and do not need a tool."
  url: "https://github.com/Trustworthy-ML-Lab/when2tool"
  variableMeasured: ["accuracy", "total tool calls"]
---

When2Tool is a benchmark for the tool-call decision in LLM agents: rather than assuming every task
needs a tool, it asks whether a model can tell when a tool is needed and when it can answer directly.
It was introduced by researchers at the University of California, San Diego in
[[ScholarlyArticle/llm-agents-already-know-when-to-call-tools-even-without-reasoning]], which
describes it as the first benchmark for studying tool-call decisions.

## Contents

The benchmark has 18 environments — 15 single-hop and 3 multi-hop — split evenly across three
categories of tool necessity: "Can I compute this?" (computational scale, such as arithmetic,
statistics, combinatorics, matrices and primes), "Do I know this?" (knowledge boundaries, such as
fact retrieval, historical years, game rules, hashing and decoding) and "Can I execute this
reliably?" (execution tracking, such as list manipulation, date arithmetic, code execution,
scheduling and regular expressions). Each environment provides tools the model must call with
correctly formatted arguments and whose responses must be parsed.

Every environment has three difficulty levels: easy tasks most models can solve without tools, medium
tasks sit at the decision boundary, and hard tasks are almost impossible without a tool — for the
knowledge category, hard tasks use fictional entities, invented events and custom algorithms that
cannot appear in any training data. The multi-hop environments chain three dependent tool calls,
each hop's output feeding the next. In total the benchmark has 1,080 training and 2,700 test tasks.
Answers are exact numbers, strings or lists checked by a deterministic evaluator, and each setting
reports accuracy and total tool calls per difficulty level.

## Provenance

All tasks are generated with fixed random seeds, and all tool responses are simulated locally and
deterministically, so the benchmark runs offline on a single machine with no API keys, network access
or API cost. New environments are added by writing a self-contained task generator. The paper states
that its code is available at <https://github.com/Trustworthy-ML-Lab/when2tool>.

## Use

[[ScholarlyArticle/llm-agents-already-know-when-to-call-tools-even-without-reasoning]] uses the
benchmark to evaluate prompt-only and reason-then-act baselines on six open models, to train and test
a linear probe that predicts tool necessity from hidden states, and to evaluate its Probe&Prefill
method. Run in a no-tool setting, the six models averaged 69.4% accuracy on easy test tasks, 54.4% on
medium and 15.5% on hard, which the authors use to confirm that the difficulty levels behave as
intended.
