---
title: "Code Review Task Taxonomy"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, evaluation, llm]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.13377'
    hash: sha256:48fbc4dbbc6846bdc40bcf267ddc54c5cb37a33b889a76dc5b54960ec064e90a
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A multi-level classification of code review research into five high-level domains — review prioritization, change understanding, peer review, review assessment, and code refinement — each subdivided into named sub-tasks, used to organize which review capabilities a benchmark actually measures."
---

The code review task taxonomy is a multi-level classification proposed in
[[ScholarlyArticle/a-survey-of-code-review-benchmarks-and-evaluation-practices]] for organizing what
code review research measures. It sorts studies into five high-level domains — Review
Prioritization/Selection, Change Understanding and Analysis, Peer Review, Review Assessment and
Analysis, and Code Refinement — and subdivides those into 18 named sub-tasks. The five domains are
aligned with the stages of the code review process itself, from deciding which changes are worth
reviewing through to revising the code after feedback, so that a benchmark's position in the taxonomy
indicates which part of a reviewer's job it exercises.

## Usage

The taxonomy is used first to ask what a given dataset actually assesses, and to make visible which
parts of the review process no dataset covers.

The five domains are defined by the inputs they consume and the outputs they produce. **Review
Prioritization/Selection** decides which changes should be reviewed and in what order, formulated as
prediction or ranking over patch content, developer and reviewer history and test signals; its
sub-tasks are review prioritization and change quality prediction. **Change Understanding and
Analysis** supports a reviewer in interpreting a change's intent, impact and structure, covering
relevant change identification, impact analysis, change decomposition and visualization. **Peer
Review** covers tasks that support or emulate the human reviewer's own judgment — issue localization,
review comment generation, issue labeling and classification, refactoring identification, defective
change prediction and security detection. **Review Assessment and Analysis** turns the examination on
the review itself, covering review quality evaluation, comment-code compliance, review summarization
and sentiment or toxicity analysis. **Code Refinement** covers the revision stage after review, split
into code revision and code refactoring.

Applied across the surveyed literature, the instrument's main use in that study is comparative: the
same sub-task labels are applied to datasets from before and after the arrival of large language
models, so that shifts in what the field measures become countable. On that reading the source reports
that Peer Review grew to account for nearly 60% of LLM-era datasets, while Change Understanding and
Analysis fell from 14 datasets to one, with change decomposition and impact analysis disappearing
altogether.

That study also proposes using the taxonomy in the other direction — as a specification for
benchmarks that do not yet exist. Rather than measuring a model's code-revision ability as a single
aggregate, it suggests curating datasets per sub-task so that capabilities such as refactoring,
improving documentation and readability, ensuring correctness, and optimizing performance can be
scored separately.

## Related Terms

- [[ScholarlyArticle/a-survey-of-code-review-benchmarks-and-evaluation-practices]] — the survey that
  proposes this taxonomy and applies it to 99 papers
- [[DefinedTerm/agentic-code-review]] — a different axis on the same subject, dividing review practice
  into eras by who participates rather than into tasks by what is measured
- [[DefinedTerm/six-dimension-process-taxonomy]] — a comparable instrument in an adjacent area, scoring
  agent process frameworks rather than classifying review tasks
