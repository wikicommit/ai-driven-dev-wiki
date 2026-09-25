---
title: "LGTM Smell"
type: "schema:DefinedTerm"
lang: en
tags: [code-review]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.17548'
    hash: sha256:becc2ac1a59aad4f9155e8968fd738e02ecb7dbf2e77a818df204daa4dfd3310
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A code review smell in which reviewers submit \"Looks Good To Me\" (LGTM) reviews in place of substantive feedback, associated with missing pull-request context, reviewer overload and time pressure."
---

The LGTM smell is a code review smell in which reviewers submit "LGTM" ("Looks Good To Me")
reviews in place of substantive feedback — for instance when a pull request gives them too little
context to understand the change, or when they are too busy to review it properly. It is counted
among the practices that undermine the effectiveness of code review.

## Usage

[[ScholarlyArticle/rethinking-code-review-in-the-age-of-ai-a-vision-for-agentic-code-review]] uses
the term, drawing on earlier code review research it cites, to connect several challenges of
traditional pull-request review to LGTM reviews. It links them to a number of situations: when a pull request lacks a descriptive title and description,
which confuses reviewers; when missing documentation leaves reviewers
unable to tell intended behavior from defects; when a missing issue link deprives them of the
requirement being implemented; and when time pressure pushes them to inspect changes hastily. It
also reports that prior work names reviewer availability as a direct root cause — a reviewer who is
too busy with other tasks but cannot decline the review request — and that one cited study found
64.7% of pull requests across five large-scale projects reviewed without any comment, with such
comment-free reviews exhibiting the LGTM smell 3.5 times more often than commented ones.

The same paper returns to the term when discussing how AI-assisted review should be evaluated,
arguing that speed-centric metrics such as time-to-merge can mislead once code generation is
accelerated, and that evaluation should instead account for how thoroughly review is conducted,
moving beyond LGTM smells.

## Related Terms

[[DefinedTerm/modern-code-review]], [[DefinedTerm/pr-issue-alignment]],
[[DefinedTerm/automation-bias]]
