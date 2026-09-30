---
title: "AACR-Bench"
type: "schema:Dataset"
lang: en
tags: [code-review, benchmark, evaluation]
sources:
  - type: url
    url: 'https://github.com/alibaba/open-code-review'
    hash: sha256:b9e25b582bd7eea6db72fdab8f395f2c2a3a3d52275e5bb2239736035a7c6c88
  - type: url
    url: 'https://www.infoq.cn/article/owxMsObP9h1wFcRqW000'
    hash: sha256:60a6ed99d642c704fc28a825c63800527d10a8ac99ef3134464f957853cfb593
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A code review benchmark built from 200 real pull requests across 50 popular open-source repositories and 10 programming languages, with 1,505 ground-truth issues annotated and cross-validated by more than 80 senior engineers. It is hosted on Hugging Face and is the benchmark Open Code Review reports its own results against."
  url: "https://huggingface.co/datasets/Alibaba-Aone/aacr-bench"
---

AACR-Bench is a code review benchmark assembled from real pull requests rather than synthetic
cases. Its stated composition is 50 popular open-source repositories, 200 real pull requests and
10 programming languages, with 1,505 annotated ground-truth issues. It is hosted on Hugging Face
under the `Alibaba-Aone` namespace. Most of this wiki's account of it comes from the README of
[[SoftwareApplication/open-code-review]], which presents and links the benchmark and reports its
own results against it; a conference talk outline by that project's author adds who led its release
and what it costs to maintain.

## Contents

The source gives the scale at two levels and says nothing about the record layout: 200 pull
requests drawn from 50 repositories, and 1,505 individual annotated issues across them, which works
out to several ground-truth findings per pull request rather than a single verdict. The
ten-language spread is stated but not broken down, and the source names none of the repositories.

## Provenance

The annotations were cross-validated by more than 80 senior engineers — the source's phrasing for
how the ground truth was established. Nothing further is said about how the 200 pull requests were
selected from the 50 repositories, how disagreements between annotators were resolved, or what
counts as a defect for annotation purposes. The README does not state who assembled the benchmark,
and that it sits under a Hugging Face namespace beginning `Alibaba-` is hosting rather than a
statement of authorship. The speaker biography in
[[NewsArticle/open-code-review-deterministic-engineering-and-agent-collaboration]] adds that
Open Code Review's author, an Alibaba engineer, led the open-sourcing of AACR-Bench, and describes it
as the industry's first multi-language code review benchmark with awareness of repository context —
the first-of-its-kind claim is his own.

The same talk outline names a limitation of the benchmark as one of the project's pain points: its ground truth is a human annotation
taken at one point in time, while code patterns, frameworks and the defect profile of AI-generated
code keep shifting, so it drifts away from production reality unless it is continuously updated —
and each update is costly to annotate, which keeps it from being a loop that can iterate often.

## Use

The one use this wiki has a record of is Open Code Review's own. Its README reports evaluating
itself against a general-purpose agent — it names Claude Code — on the same underlying model, and
states significantly higher precision and F1 for its own tool, at roughly one ninth of the tokens
and a shorter wall-clock time, with lower recall presented as a deliberate trade-off favouring
precision over noise. The README's text carries no numbers for those metrics — it links an image
where they would be — so what this wiki records from it is the direction of the claim rather than
the figures.

The five metrics the benchmark is scored on are named and explained there: F1 as the harmonic mean
of precision and recall, offered as the best single number for overall review quality; precision as
the proportion of reported issues that are real defects; recall as the proportion of real defects
found; average time per review, which matters for CI pipeline latency; and average tokens consumed
per review, which drives API cost.

The standing caveat on any figure drawn from this pairing is that the only reported result comes
from the tool being measured, presented in the same document that introduces the benchmark.
