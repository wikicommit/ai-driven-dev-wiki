---
title: "Outdated Rate"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, metrics, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2501.15134'
    hash: sha256:8cee9ceb37a21ce19689362c1d5ee9b3bbfa63f9f4f85fa4b4dcd878c06ad074
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A code review metric, introduced with ByteDance's BitsAI-CR, giving the percentage of review comments whose flagged code is modified in later commits, as an automated signal of whether developers act on the comments."
---

The Outdated Rate is a metric introduced in
[[ScholarlyArticle/bitsai-cr-automated-code-review-via-llm-in-practice]] for evaluating automated
code review comments. It is the percentage of comments seen by code committers within a one-week
measurement window that became outdated, where a comment counts as outdated if any line within the
code range it flagged is modified in a subsequent commit. It was proposed to complement precision,
which the paper argues cannot show whether developers actually accept and act on review comments
and which requires manual assessment too costly for large-scale or sustained evaluation; the Outdated
Rate, by contrast, can be computed automatically.

## Usage

In [[SoftwareApplication/bitsai-cr]] the Outdated Rate is tracked weekly for each review rule and
used together with precision to decide which rules to keep, a combination the paper presents as
what drives its data flywheel. A rule with high precision but a consistently low Outdated Rate is
read as producing comments that are technically correct but practically superfluous — its example is
a magic-number warning that follows Go coding standards but that a user disliked — and may be
decommissioned. The same measure can be applied to human reviewers: the paper reports a human
Outdated Rate at ByteDance of 35–46%, which it uses as a baseline for effective review impact.

The paper is explicit about the metric's limit: an outdated comment does not definitively prove the
code was changed in direct response to it. It is offered as a signal that helps a system improve
continuously in large-scale deployment rather than as proof of causation.

## Related Terms

- [[DefinedTerm/code-review-agent]] — the kind of automated reviewer whose comments the metric evaluates
