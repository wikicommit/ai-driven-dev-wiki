---
title: "Data Contamination"
type: "schema:DefinedTerm"
lang: en
tags: [benchmark, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2403.07974'
    hash: sha256:67c28aaadc21ea0b54adf573ed254a4ee0e73c81cd2972017fa0c8f6974ef524
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The presence of benchmark problems in a language model's training data, which lets the model score well on problems it has effectively already seen and so makes the benchmark overstate its capability on unseen problems."
---

Data contamination is the situation in which the problems of an evaluation benchmark are included in the massive training corpora of a large language model, so that the model may have encountered the exact problems it is later tested on. Because the model's score then partly reflects memorised material rather than its ability on new problems, contamination can paint a skewed or misleading picture of its capabilities; [[ScholarlyArticle/livecodebench-holistic-and-contamination-free-evaluation-of-large-language-models-for-code]] names it, alongside overfitting, as a shortcoming of code benchmarks such as HumanEval, MBPP and APPS.

## Usage

The term is used in LLM evaluation, including evaluation of code models. The LiveCodeBench paper notes that earlier work tried to decontaminate training data with exact and fuzzy matching, that this can be non-trivial, and that it can be evaded by simple strategies such as rephrasing. Its alternative is time-segmented evaluation: [[Dataset/livecodebench]] tags each problem with its release date so a model can be scored only on problems released after its training cutoff. The same dates make contamination visible — the paper reports stark drops in DeepSeek, GPT-4-O and Codestral performance on LeetCode problems released after each model's cutoff or release, which it reads as evidence that the earlier problems were likely in their training data. It also cites related work on detecting contamination, such as methods based on edit distance and AST-based semantic similarity for code.
