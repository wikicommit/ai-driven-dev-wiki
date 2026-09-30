---
title: "IFEval-FC"
type: "schema:Dataset"
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
  description: "A benchmark of 750 function-calling test cases, each a function whose parameter description embeds a verifiable format instruction plus a user query, used to measure whether LLMs follow such instructions when calling functions."
  url: "https://github.com/Skripkon/IFEval-FC"
---

IFEval-FC is a benchmark for precise instruction following in [[DefinedTerm/function-calling]]. It was
introduced in
[[ScholarlyArticle/instruction-following-evaluation-in-function-calling-for-large-language-models]]
and adapts the "verifiable instructions" of the IFEval benchmark to the function-calling setting: each
instruction is embedded in the description field of a parameter in a JSON schema, and whether the
model's call follows it is checked algorithmically.

## Contents

The benchmark offers 750 test cases, each consisting of a function with an embedded format instruction
for one of its input parameters and a corresponding user query. Its instructions are drawn from 19
distinct types of verifiable instruction, which the author organizes into seven major categories
according to the nature of the constraint — for example requiring a Python list format, restricting
text to Cyrillic or Greek script, or controlling word or comma counts. Some instruction types were adapted from IFEval
and others, such as Cyrillic/Greek and Python list format, were introduced for this benchmark. Each
response is scored 1 if the instruction is followed and 0 otherwise.

## Provenance

Part of the functions were taken from the [[Dataset/berkeley-function-calling-leaderboard]] and
enhanced with format constraints; the rest were generated with GPT-5 across 80 curated domains, each
required to include one free-form natural-language string parameter with no enum or format field so
that any format constraint could be applied to it. Five conversational user queries were generated per
function from the original, constraint-free functions, so that it is the model's job during the call to
transform a value into the required format. Tasks that an ensemble of LLMs failed on all five queries,
or answered correctly on all five with ease, were omitted, and trivially easy instruction types such as
all-uppercase or all-lowercase were excluded from the final evaluation. The code and data are publicly
available on GitHub.

## Use

The introducing paper evaluates GigaChat, Anthropic and OpenAI models on the benchmark and reports that
no evaluated model surpassed 80% accuracy.
