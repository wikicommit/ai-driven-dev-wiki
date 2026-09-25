---
title: "CodeContests"
type: "schema:Dataset"
lang: en
tags: [code-generation, competitive-programming, benchmark]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2401.08500'
    hash: sha256:0b04951cf53383d9b58bed9fa05b768a2e74972e65c4ff2168ff413ff3d8ecd1
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A code generation dataset introduced by Google's DeepMind, made up of problems curated from competitive programming platforms such as Codeforces, with long, detailed problem descriptions, public tests, and a private test set of about 200 input-output tests per problem used to judge submitted solutions."
  creator: ["DeepMind"]
---

CodeContests is a challenging code generation dataset introduced by Google's DeepMind, consisting of problems curated from competitive programming platforms such as Codeforces. It contains about 10,000 code problems that can be used to train LLMs, together with a validation set and a test set for assessing their ability to solve challenging code problems; the account here comes from [[ScholarlyArticle/code-generation-with-alphacodium]], which uses it as its evaluation benchmark.

## Contents

Each problem consists of a description and public tests, which are available as inputs to the model, and the goal is to generate a solution that produces the correct output for any legal input. A private test set, not available to the model or to contestants, is used to evaluate submitted solutions; each problem has about 200 private input-output tests, which the AlphaCodium authors say keeps false positives to a minimum. The validation and test sets contain 107 and 165 problems respectively. By design the problem descriptions are long and complicated, with small details and nuances.

## Provenance

The dataset was introduced by Google's DeepMind and is curated from competitive programming platforms such as Codeforces. The AlphaCodium paper describes AlphaCode, a DeepMind code generation system that uses a network fine-tuned specifically for competitive programming tasks, as the primary work addressing the dataset.

## Use

The AlphaCodium authors argue that CodeContests is a good dataset for evaluating LLMs on code generation because, unlike many other competitive programming datasets, it has a comprehensive private test set that avoids false positives, and because its lengthy, detailed descriptions simulate real-life problems — in contrast to datasets such as HumanEval, whose problems are easier and concisely presented. They ignore the training set and evaluate on the validation and test sets, reporting that GPT-4 pass@5 on the validation set rose from 19% with a direct prompt to 44% with their flow. They also note that AlphaCode 2 reported results on an updated variant of the CodeContests benchmark that was not released to the public.
