---
title: "SWE-Bench Verified"
type: "schema:Dataset"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A human-validated, 500-task subset of SWE-Bench released by OpenAI in collaboration with the SWE-Bench authors to address concerns that some original SWE-Bench tasks were ambiguous or underspecified."
  creator: "OpenAI"
  url: "https://openai.com/index/introducing-swe-bench-verified/"
---

SWE-Bench Verified is a human-validated, 500-task subset of [[Dataset/swe-bench]], discussed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]]. It was released by OpenAI to address concerns that some of the original SWE-Bench's tasks were ambiguous or underspecified, with OpenAI working directly with SWE-Bench's own authors on the curation.

## Contents

The subset holds 500 tasks drawn from SWE-Bench and validated by humans as well-specified and solvable.

## Provenance

SWE-Bench Verified was introduced by OpenAI in collaboration with the authors of SWE-Bench. [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] reports that OpenAI later warned the benchmark was increasingly exposed to data contamination and recommended [[Dataset/swe-bench-pro]] as a more reliable evaluation instead.

## Use

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] cites results on this subset as illustrating rapid progress on agentic coding benchmarks: GPT-4o solved 33% of tasks at its August 2024 launch, while leading agentic solutions exceeded 70% of tasks by mid-2025.
