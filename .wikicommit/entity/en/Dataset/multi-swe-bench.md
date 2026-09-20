---
title: "Multi-SWE-bench"
type: "schema:Dataset"
lang: en
tags: [evaluation, coding-agents, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2504.02605'
    hash: sha256:efffadb8771463b26f920f9ded479e505f88487063add19a6bfb5eafcc304e4e
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A multilingual issue-resolving benchmark of 1,632 annotated instances covering Java, TypeScript, JavaScript, Go, Rust, C and C++, built to evaluate large language models on modifying a codebase to produce a patch that addresses a given issue across ecosystems other than Python."
---

Multi-SWE-bench is a benchmark for issue resolving — the task of modifying a codebase to generate a
patch that addresses a given issue — built to cover programming languages beyond Python. It is
introduced in [[ScholarlyArticle/multi-swe-bench-a-multilingual-benchmark-for-issue-resolving]],
whose motivation for it is that existing benchmarks, of which that paper names
[[Dataset/swe-bench]] as an example, focus almost exclusively on Python and are therefore
insufficient for evaluating large language models across diverse software ecosystems.

## Contents

The benchmark spans seven languages: Java, TypeScript, JavaScript, Go, Rust, C and C++. It holds a
total of 1,632 instances, which the introducing paper describes as high-quality. One instance poses
the issue-resolving task the benchmark is built around — a codebase to be modified, and an issue the
resulting patch must address.

## Provenance

The 1,632 instances were selected rather than collected wholesale: the introducing paper states they
were carefully annotated from 2,456 candidates by 68 expert annotators, and offers that annotation
effort as the reason the benchmark can provide an accurate and reliable evaluation.

The authors also open-source the entire data production pipeline behind it, along with detailed
tutorials, with the stated aim of encouraging the open-source community to continuously contribute
and expand the dataset.

## Use

The introducing paper evaluates a series of state-of-the-art models on Multi-SWE-bench using three
representative methods — [[DefinedTerm/agentless]], [[SoftwareApplication/swe-agent]] and
[[SoftwareApplication/openhands]] — and reports a comprehensive analysis with key empirical
insights.
