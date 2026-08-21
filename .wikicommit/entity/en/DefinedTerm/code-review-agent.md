---
title: "code review agent"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, agentic-coding, verification, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.03196'
    hash: sha256:d341905668ac335fd8b65234aab88d9e6141be72f0b9ffda8fc58381845ae5e6
  - type: url
    url: 'https://arxiv.org/pdf/2605.17548'
    hash: sha256:becc2ac1a59aad4f9155e8968fd738e02ecb7dbf2e77a818df204daa4dfd3310
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An automated agent that posts review feedback on pull requests, acting as a gatekeeper in development workflows. Abbreviated CRA. Distinguished from CI/CD automation bots by producing code review feedback rather than performing workflow tasks."
  termCode: "CRA"
  inDefinedTermSet: ""
---

A code review agent — abbreviated **CRA** — is an automated reviewer that posts feedback on pull requests, occupying the gatekeeper position a human reviewer would otherwise hold. [[ScholarlyArticle/code-review-agents-in-pull-requests]] describes them as having become routine parts of development workflows as agentic pull-request volumes rose, and gives `coderabbitai` as an example. Its operational definition is a distinction rather than a capability list: when the authors extracted GitHub bot accounts from review comments, they manually classified each by function and excluded bots that perform CI/CD and workflow automation, such as `github-actions[bot]`, keeping only those that produce code review feedback.

## Usage

**What they can and cannot do procedurally.** In the dataset that study analysed, pull requests reviewed solely by CRAs appear exclusively in GitHub's Commented review state. The authors' stated reading is that a single CRA reviewer cannot independently approve, dismiss, or request changes — an agent supplies feedback without making the merge decision.

**The gap between claimed and observed effectiveness.** The paper is organised around that gap. On the claim side it cites vendor and industry material reporting that 81% of CRA users see quality improvements and 69% see speed improvements, that 80% of PRs receive no human comments when CRAs are enabled, and that 82% of developers use CRAs daily or weekly. On the observed side it reports that CRA-only reviewed pull requests merged at 45.20% against 68.37% for human-only ones, and were abandoned at 34.88% against 21.60%. It also cites earlier work finding human review comments addressed far more often (60%) than CRA comments (0.9% to 19.2%).

**Signal and noise.** The paper's explanation for the outcome gap is feedback quality, which it measures as a signal-to-noise ratio: the share of a PR's review comments that flag either critical signal (runtime errors, crashes, compilation failures, API-breaking changes, security vulnerabilities) or important signal (architectural problems, performance issues, maintainability concerns), out of total comments. The framework is adopted from an outside blog post on measuring signal versus noise in AI code review rather than devised by the authors. Applied to 98 closed CRA-only PRs, 60.2% scored in the 0–30% band and 12 of 13 distinct agents averaged below 60%. Named per-agent averages in that closed set include `github-advanced-security[bot]` at 27.62% over 36 PRs and Copilot at 19.79% over 24 PRs, with `entelligence-ai-pr-reviews[bot]` highest among agents with substantial counts at 52.29%; several figures rest on a handful of PRs each.

**Where they are argued to fit.** That paper's recommendation is narrow configuration over general-purpose review — specific checks such as security vulnerabilities or style violations, on the reasoning that specialised checks reduce false positives — combined with mandatory human approval before merge and workflows in which a CRA comment triggers human review rather than a direct developer response. It also raises a structural concern from prior work that CRAs often review code produced by the same provider, which it frames as a closed-loop bias risk.

### From single-stage tools to a whole-lifecycle architecture

[[ScholarlyArticle/rethinking-code-review-in-the-age-of-ai]] characterises current review tooling as fragmented — addressing isolated tasks such as reviewer recommendation, PR description generation, or comment suggestion — and argues those stage-level advances do not compose on their own, because a helpful review comment depends on a PR whose rationale was written down and reviewer matching depends on behavioural context reaching the reviewer.

Its proposed alternative, [[DefinedTerm/agentic-code-review]], decomposes review into a set of narrowly specialised agents distributed across the whole pull-request lifecycle rather than one general-purpose reviewer, with a different orchestrator and a different human at each end. At PR creation, agents for PR detail generation, issue linking, an initial automated review pass and fix suggestion sit under a PR Creation Agent that the PR *author* directs in natural language before submitting. At review time, agents for explanation, automated review, fix suggestion and comment measurement sit under a PR Review Agent that the *reviewer* addresses, and which also draws on the PR Augmentation Agent's own subagents for requirement-alignment classification, bug-proneness scoring, sandboxed runtime analysis and cross-module impact analysis. Two of the review-stage agents evaluate the human's own output rather than the code — measuring the toxicity and the usefulness of review comments as they are composed.

That paper's stated evidence for why single-pass automated review underperforms overlaps with the survey findings above: it cites empirical work reporting that 54% of reviews fail to detect bugs because of change-understanding barriers and that roughly 44.47% of review feedback is non-useful, and separately that AI-assisted reviewers surface more low-severity issues but not additional high-severity defects — which it reads as automated support pulling attention toward the easier problems.

## Related Terms

Code review agents are one automated answer to the [[DefinedTerm/verification-bottleneck]], and the evidence above is what qualifies how much of that bottleneck they actually remove. The general technique of using a model to evaluate another model's output is [[DefinedTerm/llm-as-judge]]; a CRA is that technique deployed as a persistent workflow participant. The pull requests they review are increasingly produced by [[DefinedTerm/coding-agent]] runs, which is the volume pressure the paper opens with.
