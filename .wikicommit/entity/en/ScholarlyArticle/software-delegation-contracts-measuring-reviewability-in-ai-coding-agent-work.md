---
title: "Software Delegation Contracts: Measuring Reviewability in AI Coding-Agent Work"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, empirical-study, code-review, agentic-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2606.17099'
    hash: sha256:287a1f7f2965de4360676a41fe7236b0036d0a2d603c9d92125d58e53a5d3612
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "A controlled pilot study, posted to arXiv in June 2026, that measures what explicit software delegation contracts change in AI coding-agent work, finding that on small tasks they left objective outcomes unchanged but made the returned work easier to review, at a cost in tokens and time."
  author: ["Vincent Schmalbach"]
  datePublished: "2026-06-14"
---

The paper starts from the [[DefinedTerm/software-delegation-contract]], a unit of analysis for
delegated coding work that, according to the paper, prior work had proposed without measuring its
effects. It sets out to measure them: AI coding agents increasingly accept assigned software tasks,
modify repositories under bounded authority and return work packages for review, and the study asks
whether stating the delegation explicitly changes what comes back.

The authors built a dependency-free TypeScript API task environment with seeded defects and
documentation gaps, wrote ten tasks in five families, and ran 64 agent executions across two model
tiers under three conditions: a realistic issue-style prompt, an explicit delegation contract, and a
contract with a required evidence bundle. Each run was scored with hidden acceptance tests, mutation
checks and scope analysis, and then reviewed by three independent, condition-blinded model-based
reviewers using a fixed rubric, for 192 reviews in all. The paper's conclusion is that, on these
small tasks, delegation contracts bought reviewability rather than correctness.

## Key Points

- Explicit contracts did not improve objective task outcomes: all 64 runs passed the hidden
  acceptance checks, with zero scope violations.
- Contracts improved reviewability: evidence sufficiency improved in 22 of 30 paired comparisons and
  worsened in none (+0.83 on a 5-point scale, p < 0.0001, Cliff's delta = 0.66), and reviewer
  ambiguity decreased (p = 0.035).
- Changed-file lists, known-limitations sections, residual-risk sections and reviewer checklists
  appeared in the returned work mostly or only when the contract demanded them.
- Contracts cost 13% more agent tokens and 38% more wall-clock time, with larger effects for the
  weaker model tier.
- All of these results come from a pilot of small tasks in one purpose-built TypeScript environment,
  and the reviews were made by model-based reviewers rather than people.

## Notes

The paper is an 11-page empirical pilot study, classified under Software Engineering (cs.SE) and
Artificial Intelligence (cs.AI) on arXiv. Its subject is the work an [[DefinedTerm/ai-coding-agent]]
returns for review under an assigned task.
