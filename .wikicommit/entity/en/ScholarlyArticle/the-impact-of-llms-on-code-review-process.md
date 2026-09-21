---
title: "The Impact of Large Language Models (LLMs) on Code Review Process"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, llm, developer-productivity, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.11034'
    hash: sha256:c26f6ca15b993bdf14c53dafbec5cbf2e9a282f3e856b081f914ba60fb3dbd0b
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An observational study of 25,473 GitHub pull requests testing whether those whose contributors mention using GPT resolve faster, reporting a median merge time of about nine hours against twenty-three, a 66.7% shorter review phase and an 87.5% shorter wait before a change is made, with the assistance concentrated on improving existing code rather than writing new features."
  author: ["Antonio Collante", "Samuel Abedu", "SayedHassan Khatoonabadi", "Ahmad Abdellatif", "Ebube Alor", "Emad Shihab"]
  datePublished: "2025-11-13"
  keywords: ["LLMs", "GPT", "pull requests", "code review process", "developer productivity"]
  citation: "arXiv:2508.11034"
---

This paper asks a question about phases rather than about models: not whether an LLM can review code,
but where in the life of a pull request developers actually reach for one and whether the request
then closes faster. The authors take as their gap that prior work has studied task-specific
applications of LLMs to code review while the phase-specific effects on the efficiency of the process
remain underexplored.

The dataset is 25,473 pull requests drawn from 9,254 GitHub projects. Pull requests count as
GPT-assisted when contributors say so: the authors detect them with keyword matching and regular
expression filtering, then verify manually until labelling reaches 95% accuracy, reporting
substantial inter-rater agreement with disagreements settled by consensus among the authors. For the
overall resolution question they keep only merged pull requests, leaving 1,367 GPT-assisted ones, and
compare them against a matched set of non-assisted requests. The analysis is a multiple linear
regression of time to merge on a GPT-assisted indicator with controls for number of commits, change
size, files changed and project age, together with Mann-Whitney U tests for the per-phase
comparisons.

The headline results are timing differences. GPT-assisted pull requests merge in a median of about
nine hours against about twenty-three for non-assisted ones, a 61% reduction, with the GPT indicator
significant in the regression. Broken out by phase, the review phase falls from a median of three
hours to one and the wait before a change is made from twenty-four hours to three, while the change
phase itself shows no significant difference and no evidence of GPT use appears at submission or after acceptance.
A labelled sample of 310 GPT-assisted pull requests shows what the assistance is for: in the review
phase, enhancement of existing code accounts for about 60% of requests, bug fixing about 26% and
documentation about 12%, with new implementation and testing comparatively rare.

## Key Points

- Identifies GPT-assisted pull requests by contributors' own explicit mentions, detected with
  keywords and regular expressions and verified manually to 95% labelling accuracy — so what is
  measured is disclosed use, not use.
- Reports GPT-assisted pull requests merging in a median of about nine hours against about
  twenty-three for non-assisted ones, a 61% reduction over the whole lifecycle.
- Finds the GPT-assisted indicator statistically significant in a multiple linear regression of time
  to merge that also controls for number of commits, pull request size, files changed and project
  age, with a negative coefficient.
- Finds the review phase 66.7% shorter — a median of one hour against three — and the phase the
  paper's table calls waiting for change 87.5% shorter, three hours against twenty-four, both
  significant under Mann-Whitney U. The paper's abstract and conclusion describe this same reduction
  as the waiting time before acceptance.
- Finds no significant difference in the change phase, where both groups have a median of one hour.
- Finds no evidence of GPT being used at submission or while waiting after acceptance, and concludes
  that its use concentrates in the iterative middle of the review process.
- Reports from a labelled sample of 310 GPT-assisted pull requests that, in the review phase,
  enhancement accounts for about 60%, bug fixing about 26% and documentation about 12%, while
  implementation and testing are comparatively rare; the categories overlap and can exceed 100%
  because one pull request may carry several.
- Characterises GPT in this material as a support tool for improving code that already exists rather
  than for creating new components.
- Names over-reliance on GPT in review as an open research question, and suggests tooling that
  reports on the quality, confidence or relevance of a suggestion so that developers can judge it
  rather than adopt it passively.

## Notes

The study is observational and the authors say plainly what that costs. Attributing the reductions
to GPT alone remains difficult, since task simplicity, developer experience and team dynamics could
produce the same pattern; the regression controls for some of these and the authors state that
residual confounding may persist, suggesting matching or propensity score analysis as a stronger
design. They also raise the possibility that the time savings reflect more efficient developers or
inherently simpler tasks rather than GPT's contribution.

The detection method bounds what the finding can mean. Because a pull request is labelled
GPT-assisted only when someone mentions GPT, undisclosed use falls into the comparison group and
unrelated occurrences of the word can be picked up, both of which the authors name as threats. The
phase measurements rest on GitHub timestamps and events, which they describe as an objective
foundation that nonetheless misses qualitative aspects such as interaction complexity. Generalisation
is limited to GitHub and to repositories with at least ten stars, a selection the authors note may
exclude less popular or private repositories with different review practices.

One internal discrepancy is worth noting for a reader checking figures: the abstract describes the
task-purpose sample as 300 pull requests while the method section gives 310, and the abstract
presents the task percentages without the phase qualification that the paper's own table attaches to
them.
