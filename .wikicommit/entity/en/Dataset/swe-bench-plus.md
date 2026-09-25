---
title: "SWE-Bench+"
type: "schema:Dataset"
lang: en
tags: [benchmarks, evaluation, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2410.06992'
    hash: sha256:fe195596f421247a319f0f69aac6b6ee2f3a71dd78fb639db9df2b33dbb063e7
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A refined variant of SWE-bench consisting of 548 GitHub issue-resolution tasks created after the evaluated LLMs' training cut-off dates and screened so that no issue report or comment contains its solution."
  url: "https://zenodo.org/records/13879453"
  temporalCoverage: "2023-11-01/2024-08-22"
---

SWE-Bench+ is a dataset of real-world GitHub issue-resolution tasks built by the authors of
[[ScholarlyArticle/swe-bench-plus-enhanced-coding-benchmark-for-llms]] as a more rigorous
alternative to [[Dataset/swe-bench]]. It is designed to remove two problems the authors found in
the original benchmark: issues that the evaluated models may have seen during training, and issues
whose report or comments already contain the solution.

## Contents

The dataset contains 548 task instances drawn from the same projects as SWE-bench except Django.
Each instance follows the SWE-bench format: an issue, the codebase at the corresponding version,
and a pull request whose tests are used to check a generated patch. The paper shows the distribution
of instances across projects in a figure.

## Provenance

The authors followed SWE-bench's data collection methodology using its open-source scripts. They
took the same 12 projects, excluding Django because its issues are tracked outside GitHub, and
collected issues created from 2023-11-01 to 2024-08-22 — starting a month after the most recent
training cut-off among the models they used (GPT-3.5, GPT-4 and GPT-4o). They then applied
SWE-bench's attribute filter, keeping issues that resolve a problem and contribute tests, and its
execution filter, keeping issues that install successfully and whose pull requests pass all tests,
and finally checked every instance manually to remove those with clear solution details in the
issue report. The paper states that the dataset is released on Zenodo while it is being merged
into the SWE-bench project repository.

## Use

The introducing paper ran SWE-RAG with GPT-4 and GPT-3.5, SWE-Agent with GPT-4 and
[[SoftwareApplication/autocoderover]] with GPT-4o on SWE-Bench+ and manually validated the patches
marked as resolved. It reports that [[DefinedTerm/solution-leakage]] no longer appears in the
dataset but that weak tests persist, with most patches that passed not truly resolving their issue,
and that the systems' validated resolution rates are far below their reported SWE-bench figures.
