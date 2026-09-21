---
title: "AACR-Bench"
type: "schema:Dataset"
lang: en
tags: [code-review, benchmark, evaluation]
sources:
  - type: url
    url: 'https://github.com/alibaba/open-code-review'
    hash: sha256:b9e25b582bd7eea6db72fdab8f395f2c2a3a3d52275e5bb2239736035a7c6c88
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A code review benchmark built from 200 real pull requests across 50 popular open-source repositories and 10 programming languages, with 1,505 ground-truth issues annotated and cross-validated by more than 80 senior engineers. It is hosted on Hugging Face and is the benchmark Open Code Review reports its own results against."
  url: "https://huggingface.co/datasets/Alibaba-Aone/aacr-bench"
---

AACR-Bench is a code review benchmark assembled from real pull requests rather than synthetic
cases. Its stated composition is 50 popular open-source repositories, 200 real pull requests and
10 programming languages, with 1,505 annotated ground-truth issues. It is hosted on Hugging Face
under the `Alibaba-Aone` namespace, and this wiki's account of it comes entirely from the README of
[[SoftwareApplication/open-code-review]], which presents and links the benchmark and reports its
own results against it.

## Contents

The source gives the scale at two levels and says nothing about the record layout: 200 pull
requests drawn from 50 repositories, and 1,505 individual annotated issues across them, which works
out to several ground-truth findings per pull request rather than a single verdict. The
ten-language spread is stated but not broken down, and the source names none of the repositories.

## Provenance

The annotations were cross-validated by more than 80 senior engineers — the source's phrasing for
how the ground truth was established. Nothing further is said about how the 200 pull requests were
selected from the 50 repositories, how disagreements between annotators were resolved, or what
counts as a defect for annotation purposes. The source does not state who assembled the benchmark;
that it sits under a Hugging Face namespace beginning `Alibaba-` is hosting rather than a statement
of authorship, and no source this wiki holds settles the question.

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
