---
title: "A Survey of Code Review Benchmarks and Evaluation Practices in Pre-LLM and LLM Era"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, evaluation, llm, surveys]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.13377'
    hash: sha256:48fbc4dbbc6846bdc40bcf267ddc54c5cb37a33b889a76dc5b54960ec064e90a
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A survey of 99 code review research papers from 2015 to 2025, proposing a taxonomy of five high-level code review domains and 18 sub-tasks, and comparing the datasets and evaluation metrics used before and after the arrival of large language models."
  author: ["Taufiqul Islamkhan", "Shaowei Wang", "Haoxiang Zhang", "Tse-Hsun Chen"]
  datePublished: "2026-02-13"
  keywords: ["Survey", "Benchmark", "Evaluation Strategies", "Code Review", "LLM"]
---

This survey addresses what its authors describe as a gap in the study of automated code review: the
datasets used to evaluate it are scattered, vary widely in design, and give limited insight into
which review capabilities are actually being assessed. Where surveys of benchmarks exist for
adjacent areas such as code generation, the authors report that no systematic benchmark study yet
exists for code review, leaving evaluation inconsistent and incomplete.

The authors searched several academic databases with twenty predefined search terms, restricted to
publications from 2015 onward, and expanded the result by backward and forward snowballing. They
report retrieving 160 publications, of which 77 met their inclusion criteria — the study must address
code review or a review-related task, priority given to leading software engineering and AI venues,
arXiv preprints admitted only with at least one citation, and dataset or evaluation details
disclosed — with a further 25 studies added by snowballing, for a final set of 99 papers, 58 from the
Pre-LLM era and 41 from the LLM era. From each paper they extract the datasets, evaluation metrics,
data sources and target tasks, and they built the taxonomy by open coding, the first two authors
labelling independently and then reconciling, with a reported inter-rater Cohen's Kappa of 0.81.

The resulting comparison is organized around three research questions covering the Pre-LLM era, the
LLM era, and the change between them. The authors present per-task tables recording, for each
dataset, its task, whether it draws on open-source or private projects, the number of projects, the
programming languages covered, the granularity at which the task is posed — chunk, file, method,
commit or pull-request level — the number of data points, and the evaluation metrics used.

## Key Points

- Proposes a multi-level taxonomy of code review research organized into five high-level domains —
  Review Prioritization/Selection, Change Understanding and Analysis, Peer Review, Review Assessment
  and Analysis, and Code Refinement — subdivided into 18 sub-tasks, and aligns those domains with the
  stages of the code review process. See [[DefinedTerm/code-review-task-taxonomy]].
- Reports that Peer Review tasks have come to dominate the LLM era, accounting for nearly 60% of all
  datasets in that era, against a more balanced distribution across tasks in the Pre-LLM era.
- Reports that Change Understanding and Analysis has gone from a research cornerstone with 14 datasets
  in the Pre-LLM era to nearly absent as a standalone topic with one dataset in the LLM era, with
  Change Decomposition and Impact Analysis disappearing entirely. The authors read this as
  consolidation rather than abandonment: understanding is treated as a prerequisite bundled into
  comment generation rather than a separate research goal.
- Reports a shift from language-specific to cross-language benchmarks: single-language datasets fall
  from 59% of the Pre-LLM era to 24% of the LLM era, while datasets covering nine or more languages
  rise from 2% to 34%. Java's share falls from about 61% to about 34% while Python becomes the most
  used language at about 41%.
- Argues that current benchmarks overlook macro-level review responsibilities such as impact analysis
  and commit decomposition, and that where datasets for these do exist they are often confined to a
  few languages such as Java, C and C#.
- Argues that evaluation relies on static metrics — text-matching and classification measures — that
  capture alignment with a ground truth rather than functional correctness, so that a suggested fix
  which is grammatically perfect but introduces a deadlock or fails to compile can still score well.
  The authors call for runtime measures such as build success rate and regression testing, suggesting
  sandboxed verification in containers as one route.
- Argues for granular benchmarking guided by the task taxonomy, so that a model's code-revision
  ability is measured per sub-task — refactoring, documentation and readability, correctness,
  performance — rather than as a single aggregate score.

## Notes

The authors state two threats to validity of their own. For internal validity they acknowledge that
relevant studies may have been omitted, noting that the rapid growth of AI-driven code review means
new datasets appear weekly and absolute exhaustiveness is a moving target; they report mitigating
this with multiple iterations of forward and backward snowballing and cross-referencing against
known repositories and earlier surveys. For construct validity they note that task categorization is
subject to human interpretation, and report a dual-reviewer protocol in which each paper was labelled
independently by at least two authors with a third senior researcher arbitrating disagreements.

The survey also observes what its authors call a shift in publication culture: they report a sharp
rise in 2025 driven substantially by arXiv preprints, which they attribute to rapid experimentation
with LLM-based methods and read as benchmark datasets and evaluation studies being disseminated
faster and at larger scale, often before formal peer review.
They further record that one LLM-era review-comment-generation dataset is reused by several later
studies, and that another group of works employs closely related or overlapping datasets originating
from the same CodeReviewer-style corpus.
