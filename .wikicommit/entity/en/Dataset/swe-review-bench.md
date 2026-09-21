---
title: "SWE-Review-Bench"
type: "schema:Dataset"
lang: en
tags: [code-review, benchmarks, agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.06065'
    hash: sha256:cb4fdaa0aecd873bb17c7946eae064e6fc7d82ab88b72e25a69a45f06154657d
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A benchmark for agentic code review built on SWE-bench Verified, pairing each real-world issue with AI-generated candidate pull requests of deliberately varied quality so that a reviewer's decision and its downstream usefulness can both be measured against executable tests."
  variableMeasured: ["repository checkout at the relevant commit", "natural-language issue", "candidate pull request diff", "pull request title", "pull request body"]
---

SWE-Review-Bench is the evaluation benchmark introduced in [[ScholarlyArticle/swe-review]] to measure [[DefinedTerm/agentic-code-review]] end-to-end. Where earlier review benchmarks score a review against reference comments or judge open-ended text with a prompt-sensitive evaluator, this one is built so that both halves of a review — the accept/request-changes decision and the written diagnosis — can be checked against executable verification of whether the patch actually resolves the issue.

## Contents

A record is one review instance: a repository checked out at the relevant commit, the natural-language issue, and one candidate pull request with its proposed diff, title and body. The reviewer is deliberately not given the golden patch or the hidden test results, so the benchmark measures review conducted from repository evidence rather than from the answer.

The benchmark totals 1,384 candidate pull requests after pull requests with empty patches were filtered out. It is organized into three splits, one per generating model, chosen to span high-, medium- and low-quality candidate distributions: GLM-5 (72.2% resolve rate, n=500), Qwen3-Coder-30B-A3B (50.9%, n=462) and Qwen3-30B-A3B (27.5%). The paper additionally stratifies the 1,384 instances into easy, medium and hard tertiles using a post-hoc difficulty criterion.

## Provenance

The instances derive from the 500 real-world software issues of [[Dataset/swe-bench-verified]], which supplies the executable test suites the benchmark's metrics depend on. For those same 500 issues the authors used the OpenHands-SDK agent scaffold with three models of differing capability to generate candidate pull requests, producing the three quality distributions above. That the candidate distribution is a property of those three specific generators, rather than of AI-authored pull requests in general, is a limit the benchmark carries by construction.

## Use

[[ScholarlyArticle/swe-review]] uses the benchmark to compare agentic review against single-turn fixed-context review baselines, and reports that agentic review wins on both Decision Accuracy and Resolve Rate after Revision across all three generator splits, with the largest margins on the harder tertiles that require non-local repository reasoning. The paper states the benchmark will be released.
