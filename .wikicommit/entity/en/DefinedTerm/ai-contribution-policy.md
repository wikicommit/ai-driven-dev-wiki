---
title: "AI contribution policy"
type: "schema:DefinedTerm"
lang: en
aliases: ["AI contribution rules"]
tags: [open-source, ai-governance, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.26819'
    hash: sha256:1eacfc0f1ecc9c6417e146a4780acd58380742a08adb36aaed687c0c20270840
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A written rule an open-source community adopts to govern AI-generated contributions, ranging from an outright ban to mandatory disclosure, required verification before submission, and handing critical steps to a human."
---

An AI contribution policy is the set of written rules an open-source community adopts to regulate
contributions produced with AI assistance, including contributions made by coding agents. As
described in
[[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]],
communities wrote such rules in response to a flood of AI-generated contributions that are cheap to
produce but costly to review, and the rules range from a total ban through mandatory disclosure to
verification gates and human sign-offs.

## Usage

The same paper groups the provisions into four types, a classification it adopts, inspired by earlier
work by the same authors:

- **Refuse** — banning AI-generated contributions outright.
- **Disclose** — requiring contributors to disclose how AI assisted the work.
- **Verify** — mandating verification, such as running required checks or a manual review, before
  a contribution is submitted.
- **Handoff** — reserving critical steps, such as implementing the fix or opening the pull request,
  for a human.

Following open-source conventions, these rules are documented in several places rather than one:
contributing guidelines such as `CONTRIBUTING.md`, pull-request templates, agent instruction files
such as [[DefinedTerm/agents-md]], and separate policy files such as `AI_POLICY.md`; some sit
outside the repository entirely, on project websites or in `.github` repositories. The paper's
corpus hand-codes 455 such norms from 102 communities.

Two properties make these rules hard to apply to agents. A rule takes effect only if the
contributor is aware of it, and an agent may not check governance files that a human developer
would. And violations leave little trace: the paper observes that the only evidence a reviewer
typically sees is a checkbox, backed by community trust and reputation. Measured on
[[Dataset/repocompliancebench]], four frontier coding agents opened the relevant policy file in 3.5%
of unaided runs; disclosure and verification rules largely recovered once the rule reached the
agent or one round of feedback named the violation, while refusal and handoff rules did not. The
authors conclude that bans and human-approval rules need enforcement outside the agent, such as a
CI check that blocks the merge, required human review, or a bot that closes AI-authored pull
requests.

## Related Terms

- [[DefinedTerm/agents-md]]
