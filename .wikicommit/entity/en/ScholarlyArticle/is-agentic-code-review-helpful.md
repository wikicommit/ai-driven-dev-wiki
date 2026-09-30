---
title: "Is Agentic Code Review Helpful? Mining Developers' Feedback to CodeRabbit Reviews in the Wild"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, agentic-code-review, empirical-study, mining-software-repositories]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2607.03316'
    hash: sha256:956e9dca5a4b96ebca5f05ddc9d52438ab5d8dcd654d5abfbfa8a2270ba8b20e
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An empirical study of 31,073 CodeRabbit review comments and the developer feedback they received across 10,191 pull requests in 239 GitHub repositories, measuring how often agentic reviews are accepted or rejected, why they are rejected, and whether rejection can be predicted."
  author: ["Hong Yi Lin", "Mingzhao Liang", "Patanamon Thongtanunam", "Kla Tantithamthavorn"]
  datePublished: "2026-07-03"
  keywords: ["agentic code review", "CodeRabbit", "developer feedback", "pull requests", "empirical study"]
---

This paper examines [[DefinedTerm/agentic-code-review]] — autonomous agents posting review comments on pull requests — from the side of the developers who receive it. Noting that such tools are increasingly integrated into development workflows but that there is limited evidence of how developers respond to their comments in practice, it uses [[SoftwareApplication/coderabbit]] as a case study.

The authors mine 31,073 pairs of code reviews and developer feedback from 10,191 pull requests across 239 GitHub repositories, classify how developers responded, analyse the reasons behind rejections and the kinds of concern the reviews raised, and then explore LLM-based and learning-based approaches for predicting whether a review will be rejected.

## Key Points

- Agentic reviews received a mixed reception: 36.4% were accepted, 7.3% triggered discussion and 56.3% were rejected.
- Rejections were primarily associated with invalid suggestions — false positives, redundant comments or out-of-scope comments — and with misalignment with developer intent and coding practices.
- The agentic reviews focused more on functional concerns than on evolvability-related ones, yet functional comments were more likely to be invalid.
- Lightweight learning-based methods predicted review rejection with up to 76% F1, which the authors take as evidence of learnable patterns between reviews and the feedback they receive.

## Notes

The study covers a single tool, so its figures describe CodeRabbit's reviews rather than agentic code review in general; the authors present the results as showing both opportunity gaps for improvement and shortcomings that limit CodeRabbit's effectiveness. The arXiv record lists a first version on 3 July 2026 and a revised version on 23 July 2026.
