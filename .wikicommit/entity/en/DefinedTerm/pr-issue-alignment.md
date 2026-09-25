---
title: "PR-Issue Alignment"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, traceability]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.17548'
    hash: sha256:becc2ac1a59aad4f9155e8968fd738e02ecb7dbf2e77a818df204daa4dfd3310
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "As formalized by Isik et al., whether a pull request completely and accurately implements the requirements of the issue it is linked to, classified into four categories: Exact, Tangling, Missing, and Missing and Tangling."
---

PR-issue alignment, as formalized by Isik et al. and described in
[[ScholarlyArticle/rethinking-code-review-in-the-age-of-ai-a-vision-for-agentic-code-review]], is
whether a pull request completely and accurately implements the requirements specified in its
associated issue. That formalization defines four alignment categories: **Exact**,
where the pull request fully addresses the requirements without unrelated changes; **Tangling**,
where it includes changes unrelated to the issue; **Missing**, where it fails to fully address the
issue; and **Missing and Tangling**, which combines both deviations.

## Usage

The vision paper attributes the formalization of the concept and its four categories to that
earlier study, which it cites, and describes judging PR-issue alignment as a critical challenge for pull-request reviewers. It traces
the concept's roots to research on tangled commits, which had focused on binary classification at
the commit level, and presents PR-issue alignment as extending that idea to the broader relationship
between a pull request and its issue. According to the paper, Missing pull requests are indicative
signs of technical debt, while Tangling pull requests hinder review and defect detection by adding
noise in which critical changes can be missed, and can delay approval of an otherwise correct
change when an unrelated part is controversial. It cites prior studies reporting that 7–20% of
changesets contain tangled changes and that 16.5% of pull requests were labeled Missing.

In the review framework that paper proposes, an Alignment Analysis Agent automates the check: it
retrieves the issue's title, description and acceptance criteria along with the pull request's
details and code diff, classifies the pull request into one of the four categories, highlights the
tangling lines and irrelevant additions in the review interface, and reports line numbers of
tangling modifications and details of any missing implementation so that reviewers can request
revisions. The paper lists PR-issue alignment among its keywords and treats it as one of four
analyses in its PR Augmentation stage.

## Related Terms

[[DefinedTerm/lgtm-smell]], [[DefinedTerm/agentic-code-review]], [[DefinedTerm/modern-code-review]]
