---
title: "Solution Leakage"
type: "schema:DefinedTerm"
lang: en
tags: [benchmarks, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2410.06992'
    hash: sha256:fe195596f421247a319f0f69aac6b6ee2f3a71dd78fb639db9df2b33dbb063e7
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A defect of an issue-resolution benchmark instance in which the solution to the issue is already outlined in the issue report or its comments, so that a model given that text can copy the fix rather than work it out."
---

Solution leakage is the name the authors of
[[ScholarlyArticle/swe-bench-plus-enhanced-coding-benchmark-for-llms]] give to benchmark instances
in which the solution to the issue is clearly outlined in the issue description or in the comments
on it. Because issue-resolution benchmarks such as [[Dataset/swe-bench]] provide both the issue
description and its comments (called `hints_text` in SWE-bench) to the model as input, a model can
extract the solution directly from that text instead of generating it independently; the paper
describes patches produced this way as "cheating" and as replicating what is provided rather than
demonstrating problem-solving ability. It is also referred to in the paper as "solution leak" or
"answer leak".

## Usage

The term is used when assessing whether a benchmark's reported resolution rates measure genuine
problem solving. The paper cites an issue from the sympy project whose description contained the
exact code patch needed, and reports that 32.67% of the 251 SWE-bench patches it studied from
SWE-Agent with GPT-4 were solution leaks, making this the most common pattern among resolved
instances; it also found such instances in SWE-bench Lite and SWE-bench Verified. The authors'
response was to build [[Dataset/swe-bench-plus]], manually removing instances whose issue reports
contain clear solution details.

The paper treats solution leakage as distinct from two neighboring problems: weak tests, where an
incorrect or incomplete patch passes because the tests cannot detect it, and potential data leakage,
where the issues and their fixes may have appeared in a model's training data because they predate
its cut-off date.

## Related Terms

- [[DefinedTerm/data-contamination]]
- [[DefinedTerm/software-issue-resolution]]
