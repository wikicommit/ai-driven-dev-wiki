---
title: "BitsAI-CR: Automated Code Review via LLM in Practice"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, industry-case-study, llm, data-flywheel]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2501.15134'
    hash: sha256:8cee9ceb37a21ce19689362c1d5ee9b3bbfa63f9f4f85fa4b4dcd878c06ad074
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A paper from ByteDance presenting BitsAI-CR, an LLM-based automated code review framework that pairs a two-stage comment generation pipeline with a data flywheel, and introducing the Outdated Rate metric for whether developers act on review comments."
  author: ["Tao Sun", "Jian Xu", "Yuanpeng Li", "Zhao Yan", "Ge Zhang", "Lintao Xie", "Lu Geng", "Zheng Wang", "Yueyan Chen", "Qin Lin", "Wenbo Duan", "Kaixin Sui"]
  keywords: ["Code Review", "Large Language Model", "Data Flywheel"]
---

This paper presents [[SoftwareApplication/bitsai-cr]], an automated code review framework built and
deployed at ByteDance, and reports what its authors learned from running it at enterprise scale. It
starts from ByteDance's internal data on review practice — reviewers spend an average of 15 minutes
per review in over half of cases, only 30% of reviews receive immediate attention, and over 67% of
engineers want more effective tools — and from three challenges it identifies in existing LLM-based
code review: insufficient precision, comments that are technically correct but of low practical
value, and a lack of systematic mechanisms for targeted improvement.

Its answer has two parts. A review comment generation pipeline runs a fine-tuned LLM called
RuleChecker over a taxonomy of 219 review rules to detect potential issues, then a second fine-tuned
LLM called ReviewFilter to verify them, before similar comments are aggregated. A data flywheel then
improves the system continuously from annotation feedback, precision measurements and a new metric,
the [[DefinedTerm/outdated-rate]], which measures the share of flagged code that developers go on to
modify.

## Key Points

- A three-tier taxonomy of review rules — review dimensions, review categories and detailed review
  rules — is presented as the foundation of the system, organising data collection, model training,
  evaluation and targeted optimisation; its four dimensions are code defects, security
  vulnerabilities, maintainability and readability, and performance issues.
- In offline evaluation on 1,397 cases sampled from the production codebase, the taxonomy-guided
  version reached 57.03% overall precision against 16.83% for a base version trained on the same
  volume of randomly sampled human review data without the taxonomy, and outperformed the baseline
  models it was compared with.
- An ablation study found that adding ReviewFilter consistently improved precision, because even
  extensively fine-tuned LLMs produced hallucinated comments — for example flagging a variable name
  for an underscore it did not contain.
- Of three reasoning patterns tested for ReviewFilter, Conclusion-First — a decision token followed
  by its rationale — gave the highest precision (77.09%) at an inference time of 1.7 seconds per
  sample, against 31 seconds for Reasoning-First, and was adopted.
- The authors prioritise precision over recall, arguing that developers ignore review comments when
  faced with too many and that inaccurate comments early on damage user trust.
- Over an 18-week period online, RuleChecker's precision rose from 27.9% to 62.6% and ReviewFilter's
  from 35.6% to a peak of 75%.
- For Go, the Outdated Rate reached 26.7% by week 18 after underperforming rules were removed, which
  the authors describe as converging toward ByteDance's human Outdated Rate of 35–46%.
- The system is deployed across ByteDance's development teams with over 12,000 weekly active users
  and a second-week retention rate of 61.64%, holding at around 48% over eight weeks; in a survey of
  137 users, 74.5% affirmed the value of its reviews.

## Notes

The lessons the authors draw are that a well-defined rule taxonomy is the cornerstone of an effective
automated review system, that a dedicated verification stage is necessary for production-grade
reliability, and that precision alone is not enough to evaluate review rules without a measure of
user acceptance such as the Outdated Rate. They acknowledge that the Outdated Rate does not prove a
change was made in direct response to a comment. Future work named in the paper is expanding language
coverage beyond the five languages currently supported and developing cross-file review, since the
current rules focus mainly on function-level understanding with limited context.
