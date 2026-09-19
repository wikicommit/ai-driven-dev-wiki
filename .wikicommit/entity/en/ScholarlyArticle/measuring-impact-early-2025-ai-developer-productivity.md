---
title: "Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity"
type: "schema:ScholarlyArticle"
lang: en
tags: [ai-assisted-programming, coding-tools, evaluation]
sources:
  - type: url
    url: 'https://metr.org/Early_2025_AI_Experienced_OS_Devs_Study-paper.pdf'
    hash: sha256:e66dae0841ce1d0555249838c9ef705372ee5153a16710f0cb447edc8f6892bf
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A randomized controlled trial by METR in which 16 experienced open-source developers completed 246 real issues on repositories they knew well, with each issue randomly allowing or disallowing early-2025 AI tools. Allowing AI increased completion time by 19%, while the developers had forecast a 24% reduction and, after the fact, still estimated a 20% reduction."
  author: ["Joel Becker", "Nate Rush", "Beth Barnes", "David Rein"]
  keywords: ["randomized controlled trial", "developer productivity", "AI coding tools", "field experiment", "open source"]
---

This paper reports a randomized controlled trial measuring what AI tools at the February–June 2025
frontier did to the productivity of experienced open-source developers working on their own
repositories. Sixteen developers with moderate AI experience completed 246 real issues — 136 with
AI allowed, 110 with it disallowed — with each issue defined before randomization and assigned to
a condition by a simulated coin flip. Where AI was allowed, developers could use any tools they
chose and mostly used Cursor Pro with Claude 3.5 or 3.7 Sonnet; where it was not, no generative AI
tooling was permitted. The outcome measure was the time taken to implement each issue.

The design deliberately sits away from the settings the authors say most prior measurements use.
They argue that laboratory studies of AI's effect on developers trade realism for scale, using
self-contained tasks that need little prior context, and that field studies often measure outcomes
such as lines of code, commits or pull requests, which AI can move without productivity actually
rising — code can be more verbose but functionally equivalent, and work can be split into more
pieces without the total changing. This study's five stated contributions are testing
February–June 2025 frontier models, using live repository issues rather than synthetic or
cherry-picked ones, fixing the outcome measure before randomization, recruiting engineers with
years of expertise in the target repositories, and collecting screen recordings and qualitative
data alongside the timings.

## Key Points

- Allowing AI increased implementation time by 19% on average, and AI-allowed issues took longer at nearly every quantile of the observed distribution. The paper notes the raw percentage difference between the two groups is 34%, larger than the 19% its regression estimates, because the AI-allowed issues happened to come out slightly harder after randomization; the regression accounts for that and the simple ratio does not.
- The gap between expectation and outcome runs in one direction for everybody asked. Developers forecast a 24% reduction in completion time before starting, and after the study still estimated they had been sped up by 20%. Thirty-four economics experts and fifty-four machine-learning experts forecast reductions of 39% and 38%.
- Developers were nonetheless well calibrated about *relative* difficulty: the correlation between forecast and actual time was 0.64 for AI-allowed issues and 0.59 for AI-disallowed ones. What was reversed was their expectation about whether AI would help.
- On the 74 issues with valid screen recordings, hand-labelling showed where the time went: with AI allowed, developers spent a smaller share of their time actively coding and reading or searching for information, and more of it prompting the AI, waiting for generations, reviewing outputs, and idle.
- The paper identifies 20 properties of the setting that could a priori explain the slowdown, grouped as direct productivity loss, experimental artifact, factors raising human performance and factors limiting AI performance. It finds evidence that 5 contribute, mixed or no evidence for 9, and evidence against 6 — while cautioning that the analysis is not powered for statistically significant multiple comparisons and is intended as suggestive rather than conclusive.
- The five with supporting evidence are over-optimism about AI's usefulness; high developer familiarity with the repositories (developers slowed down more on issues they knew better); large and complex repositories; low AI reliability, with developers accepting under 44% of AI generations, a majority reporting major cleanup of AI code, and 9% of time spent reviewing or cleaning it; and implicit repository context the AI does not have access to.
- Factors the paper finds evidence *against* include an unfamiliar development environment, developers cheating or under-using AI, issue dropout, and non-robustness of the outcome measure or estimator — alternative measures and estimators yielded similar slowdown, and developers who stayed in comparable IDEs across conditions still showed a 24% slowdown.

## Notes

The developers and repositories are at one end of the experience range on purpose. Participants
were typically engineers with over a decade of experience, averaging five years and 1,500 commits
on the repository they worked in — about 59% of that repository's lifetime — and were paid $150 an
hour to take part. The repositories averaged 23,000 stars, 1,100,000 lines of code, 4,900 forks,
20,000 commits and 710 committers, with high quality bars for contributions. While 93% of the
developers had used LLMs before, only 44% had used the Cursor IDE.

The authors are explicit that the result is about this setting. They caution against
overgeneralising, note that the two factors they find contribute most — repository familiarity and
repository size and maturity — do not apply in many development settings, and say their results
are consistent with small greenfield projects or work in unfamiliar codebases seeing substantial
speedup. They also expect that AI systems with higher reliability, lower latency or better
elicitation could speed up developers even in this setting, and report preliminary evidence, not
included in the paper, that fully autonomous agents using Claude 3.7 Sonnet can often implement
the core functionality of issues from these repositories while failing to satisfy all requirements
— typically omitting documentation, failing lint or style rules, and leaving out tests.

What the paper draws from the expectation gap is methodological: that it underscores the
importance of field experiments with outcome measures fixed in advance, rather than relying on
expert forecasts or developer surveys. It also offers the slowdown as some evidence that AI
capabilities in the wild may be lower than benchmark results suggest.
