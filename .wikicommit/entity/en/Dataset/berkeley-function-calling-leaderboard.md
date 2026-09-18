---
title: "Berkeley Function Calling Leaderboard (BFCL)"
type: "schema:Dataset"
lang: en
tags: [agents, tool-use]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2504.15546'
    hash: sha256:39549788a2452ec0fb8ea5da808b3e0e1e78cd4676d00b50ff2c06f8b85de2cd
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A benchmark dataset for evaluating large language models on function-calling (tool-calling) tasks, pairing a natural-language query and a desired function specification as input with a structured JSON object naming the correct function, parameters, and values as the expected output."
  variableMeasured: ["natural language query", "function specification", "correct function name", "correct parameters", "correct values"]
---

The Berkeley Function Calling Leaderboard (BFCL), introduced by Yan et al. (2024), is a benchmark dataset for evaluating how well large language models perform function-calling (tool-calling) tasks. [[ScholarlyArticle/testing-rest-apis-as-llm-tools]] uses BFCL's V3 release as part of the training data for fine-tuning its own natural-language test-case generation model.

## Contents

Each BFCL example pairs a natural-language user query with a desired function specification (comparable in structure to an API specification) as input, and a structured JSON object naming the correct function, its parameters, and their values as the expected output.

## Provenance

BFCL was introduced by Yan et al. (2024) as a benchmark for function-calling in large language models. [[ScholarlyArticle/testing-rest-apis-as-llm-tools]] draws specifically on its V3 release.

## Use

[[ScholarlyArticle/testing-rest-apis-as-llm-tools]] combines 400 of BFCL's simpler API examples (each with a maximum of 10 parameters) with 120 additional human-curated, domain-specific API examples of its own, and uses 70% of that combined pool — with 15% each held out for validation and test — to fine-tune a Granite-3B-Code-Base model (via LoRA) to generate natural-language test-case utterances.
