---
title: "Automated Code Review In Practice"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, industry-case-study, llm]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2412.18531'
    hash: sha256:ac124a39ba7a6dcd791eadca078770724a87d60055b9a6b95b3a0ffa48769833
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An industrial case study at the software division of Beko of an LLM-based automated code review tool built on Qodo's open-source PR-Agent, combining pull request data with developer surveys to assess its usefulness, its effect on pull request closure time, and its effect on human review activity."
  author: ["Umut Cihan", "Vahid Haratian", "Arda İçöz", "Mert Kaan Gül", "Ömercan Devran", "Emircan Furkan Bayendur", "Baykal Mehmet Uçar", "Eray Tüzün"]
  keywords: ["code review", "large language models", "pull requests", "AI-assisted code review", "industry case study", "code review automation"]
---

This paper, by researchers from Bilkent University and practitioners from Beko, examines the impact
of LLM-based automated code review tools in an industrial setting, a question the authors say had
not yet been examined empirically. The study object is the software development division of Beko, a
multinational company in the consumer durables and electronics sectors, which adopted an automated
code review tool based on [[SoftwareApplication/pr-agent]] from [[Organization/qodo]] (formerly
CodiumAI), customised to its needs and named "CodeReviewBot" internally. The tool posts automatic
review comments on each pull request using a GPT-4 model, while developers can still add their own
reviews.

Beko rolled the tool out from a first pilot in November 2023 to 10 projects and 22 repositories by
June 2024, with 238 practitioners having access to it. The analysis focuses on the three projects
that adopted it earliest, covering 4,335 pull requests of which 1,568 underwent automated review. It
draws on three data sources: pull request data from Azure DevOps, including labels developers were
required to put on each review comment under a mandatory comment resolution policy; a short survey
sent with individual pull requests; and a broader survey of 22 practitioners about their general
opinion of automated code review.

## Key Points

- 73.8% of the tool's review comments on merged pull requests were labelled "Resolved" and 21.3%
  "Won't Fix", with the resolved share varying widely by project — 55% in one project against 90% in
  another.
- Pull requests received 88 commits after the bot's comments but before any human reviewer had
  commented, which the authors read as developers acting proactively on the bot's suggestions.
- Average pull request closure time rose from 5 hours 52 minutes before the tool to 8 hours 20
  minutes after it, a statistically significant increase; the trend differed by project, and one
  project's closure time fell from 6 hours 6 minutes to 3 hours 7 minutes.
- The average number of human review comments per pull request fell from 0.31 to 0.28, a decrease
  that was not statistically significant, so the tool did not replace the need for human review; the
  bot itself left an average of 3.65 comments per pull request.
- In the general survey, 68.8% of respondents perceived a minor improvement in code quality, and
  most perceived no effect on knowledge sharing, with none reporting a negative one.
- Practitioners valued faster bug detection, catching code smells, typos and forgotten test code,
  greater awareness of code quality, and the promotion of best practices.
- The drawbacks reported were faulty reviews, unnecessary corrections, out-of-scope or irrelevant
  suggestions, redundant comments generated again after each fix, and a concern that reviewers
  might over-rely on the bot and let severe bugs go unnoticed.
- The authors conclude that LLM-based automated code review can moderately improve software
  development activity, but found no conclusive evidence of consistent time or effort savings, and
  advise examining such tools extensively before widespread adoption.

## Notes

The authors frame the work against [[DefinedTerm/modern-code-review]] and against earlier automation
efforts, which they describe as focused mostly on reviewer assignment. They acknowledge several
threats to validity: some authors belong to Beko's software organisation, one in a managerial role,
so the results and discussion were written by the non-practitioner authors; data collection
centred on summer, making conclusions subject to seasonality; comment resolution labels depend on
developers following the policy; and the findings rest on one tool built on one LLM at one company,
so they aim to replicate the study at other companies rather than to generalise statistically.
