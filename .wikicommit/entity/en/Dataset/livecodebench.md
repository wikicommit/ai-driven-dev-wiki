---
title: "LiveCodeBench"
type: "schema:Dataset"
lang: en
tags: [benchmark, code-generation, evaluation, data-contamination]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2403.07974'
    hash: sha256:67c28aaadc21ea0b54adf573ed254a4ee0e73c81cd2972017fa0c8f6974ef524
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A continuously updated benchmark for evaluating LLMs on code, built from problems collected over time from LeetCode, AtCoder and CodeForces contests and tagged with their release dates, with scenarios for code generation, self-repair, code execution and test output prediction."
  url: "https://livecodebench.github.io/"
  temporalCoverage: "2023-05/2024-05"
---

LiveCodeBench is a benchmark for evaluating large language models on code-related tasks, introduced in [[ScholarlyArticle/livecodebench-holistic-and-contamination-free-evaluation-of-large-language-models-for-code]] by researchers from UC Berkeley, MIT and Cornell. It collects new problems over time from programming contests and marks each with its release date, so that a model can be evaluated only on problems released after its training cutoff; its authors present it as a live, holistic and contamination-free alternative to benchmarks such as HumanEval and MBPP.

## Contents

Each problem pairs a natural-language problem statement with test cases and, where available, a ground-truth solution, plus the contest date used as its release date. At the time of the paper it contained 511 problems released between May 2023 and May 2024 — 267 from AtCoder, 235 from LeetCode and 9 from CodeForces — split into 182 easy, 206 medium and 123 hard problems, with about 17 tests per problem on average. The problems are organised into four scenarios: code generation and self-repair (511 problem instances), code execution (479 samples drawn from 85 LeetCode problems, filtered for short programs with a limited number of execution steps) and test output prediction (442 instances from 181 LeetCode problems). Results are measured with Pass@1.

## Provenance

Problems are scraped from weekly and biweekly LeetCode contests, AtCoder beginner contests and CodeForces Division 3 and 4 contests, taken from publicly visible pages only, with problems containing images or admitting multiple correct answers excluded. Difficulty labels come from each platform's own ratings, and problems rated above a threshold are excluded as too hard. Tests are taken from the platforms where available; otherwise they are produced by input generators that GPT-4-Turbo writes from the problem specification, validated against correct programs. The authors describe it as an extensible framework to which new problems, scenarios and models will be added, and state that they use the collected problems for academic purposes only and do not train on them.

## Use

The introducing paper evaluates 52 models on LiveCodeBench and uses its release dates to detect likely [[DefinedTerm/data-contamination]] — for example a sharp drop in DeepSeek models' performance on LeetCode problems released after August 2023 — and to compare models only on problems released after their cutoff. It also reports that some fine-tuned open-access models that score well on HumanEval+ perform much worse on LiveCodeBench, which the authors interpret as overfitting to HumanEval.
