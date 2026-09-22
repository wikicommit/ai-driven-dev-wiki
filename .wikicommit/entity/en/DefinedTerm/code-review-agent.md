---
title: "Code Review Agent"
type: "schema:DefinedTerm"
lang: en
tags: [agents, code-review, coding-tools]
sources:
  - type: url
    url: https://arxiv.org/pdf/2604.03196
    hash: sha256:d341905668ac335fd8b65234aab88d9e6141be72f0b9ffda8fc58381845ae5e6
    license: CC-BY-4.0
  - type: url
    url: 'https://zenn.dev/globis/articles/d0c73d2b176ba5'
    hash: sha256:d007e48e9860eef6953063dd12b23e8be1cf1576ddabcc4574d8a292c21d4357
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An automated bot that posts review feedback on pull requests, as distinct from a bot performing CI/CD or workflow automation. Abbreviated CRA."
---

A code review agent (CRA) is an automated participant in a pull request that posts review
feedback on the code under review. The category is defined by function rather than by
implementation: what separates a CRA from the other bots that comment on pull requests is that it
produces feedback about the code, where bots such as `github-actions[bot]` perform
continuous-integration and workflow automation instead. That distinction has to be drawn by hand
— in GitHub's own pull request data every bot is recorded under the same `Bot` user type, with
nothing to separate a reviewer from a build runner.
[[ScholarlyArticle/from-industry-claims-to-empirical-reality]] handled this by extracting the
distinct bot names from its data and classifying each one manually by what it does, excluding the
CI/CD and workflow-automation accounts.

## Usage

CRAs became a routine part of pull request workflows alongside the rise in pull requests opened
by autonomous coding agents. The argument for adopting them is one of volume: when code arrives
faster than human reviewers can read it, review becomes the bottleneck, and an automated reviewer
is one place to look for relief.

A CRA occupies a structurally weaker position in the review process than a human reviewer does.
In the pull request data examined by
[[ScholarlyArticle/from-industry-claims-to-empirical-reality]], pull requests reviewed solely by
CRAs appeared only in the Commented review state — never Approved, Changes Requested, or
Dismissed. That study reads this as showing a lone CRA cannot make an explicit merge decision: it
can say something about the code, but it cannot by itself approve the change or formally demand
that it be revised.

That study also measured how well CRAs do the job. It found pull requests
reviewed only by CRAs merging at 45.20% against 68.37% for human-only review, and traced the
difference to the quality of the feedback rather than its quantity — 60.2% of the 98 abandoned
CRA-only pull requests it examined scored in the lowest 0–30% band of the
[[DefinedTerm/signal-to-noise-ratio]]. Its recommendation is that CRAs be configured for narrow,
specific checks such as security vulnerabilities or style violations, on the argument that
specialised checks produce fewer false positives, and that a human approval step be kept in place
before merging.

Individual CRAs vary widely in the quality of what they produce. That study identified 13
distinct CRAs across the abandoned pull requests it examined, and reported that 12 of them
averaged below 60% signal. It notes that the number of pull requests an agent reviews is no guide
to how useful its comments are.

A practitioner account arrives at the same narrowing independently, and reports what it was for. It
was published before that study and does not cite it, so what the two share is a conclusion rather
than a lineage. [[BlogPosting/growing-ai-code-review-with-single-responsibility]] records a team whose
general-purpose reviewer produced enough off-target comments that colleagues began ignoring its
output, and whose response was to split the one reviewer into many — one per review concern, each
carrying only the context that concern needs, which the post frames as the single responsibility
principle applied to the reviewer. Its examples are narrow in the way that study recommends: one agent
looks for test patterns that make a suite flaky, another for pagination queries whose ordering is not
unique.

Two details of that account bear on the category rather than on the team. The first is the failure
mode it names: low-signal output does not merely waste a reader's time, it costs the reviewer its
audience, which is a different kind of loss from the merge-rate gap measured above. The second is
where the narrowness came from — the team reports feeding its own past failures back in as detection
patterns, so that fixing a defect and extending the reviewer became one act, and reports reaching for
an LLM reviewer specifically on a class of defect a static-analysis rule had proved too awkward to
express.

## Related Terms

- [[DefinedTerm/signal-to-noise-ratio]] — the measure used to judge how much of a CRA's feedback
  is actionable
