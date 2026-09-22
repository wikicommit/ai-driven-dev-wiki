---
title: "Software Factory"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, agents, code-review, verification, software-process]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Feb/7/software-factory/'
    hash: sha256:f037b61ef74329e98d22e3f5e86498585708d651d71581e420890095020b0ad3
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "StrongDM's AI team's name for their own way of working: non-interactive development in which specifications and scenarios drive agents that write code, run harnesses and converge without human review, held together by scenarios they say are often kept outside the codebase and a probabilistic measure of whether they are satisfied."
---

A software factory, in the sense [[Organization/strongdm]]'s AI team gave the term when they first
described their working arrangement publicly, is non-interactive development in which specifications
plus scenarios drive agents that write code, run harnesses and converge without human review. They use the term for their own practice rather than as a
general industry category, but it is not presented as their coinage: the source introduces them as a
team implementing what it says Dan Shapiro called the Dark Factory level of AI adoption. What is
theirs is this definition and the two prohibitions they state with it — code must not be written by
humans, and code must not be reviewed by humans.
A third, practical statement accompanies them — that if a team has not spent at least $1,000 on
tokens per human engineer per day, its software factory has room for improvement.

## Usage

The prohibition on review is what the rest of the practice exists to make survivable. The relaying
author frames the problem the team ran into as the obvious one — if nothing is written by hand, how
do you ensure the code works? — and notes that having the agents write tests only helps if they do
not cheat. Their answer has three
named parts. **Scenarios**, a word they say they repurposed — the source
describes their answer as inspired by scenario testing — are end-to-end user stories they say are
often held *outside* the codebase — the comparison they draw is to a holdout set in model training — so that
the agents writing the code cannot read the thing that judges it; each is meant to be intuitively
understandable and flexibly validated by an LLM rather than asserted exactly.
**Satisfaction** is the measure that replaces a green test suite: because much of the software they
grow itself has an agentic component, they state success probabilistically as the fraction of all
observed trajectories through all the scenarios that likely satisfy the user. And a
[[DefinedTerm/digital-twin-universe]] of agent-built clones of their third-party dependencies
supplies somewhere those scenarios can be run at volume.

The team also names three techniques on their own techniques pages as part of the same practice —
gene transfusion, semports and pyramid summaries. The relaying author paraphrases them
respectively as having agents extract
patterns from existing systems and reuse them elsewhere, porting code directly from one language to
another, and providing summaries at several levels of detail so an agent can enumerate the short ones
and zoom in as needed. Those pages are theirs and only their existence and one-line glosses are
established here.

## When It Applies

On the team's own account the practice became viable at a specific point: they date their catalyst to
a transition observed in late 2024, stating that with the second revision of Claude 3.5 long-horizon
agentic coding workflows began to compound correctness rather than error. The team formed in July
2025 on the rule of no hand-coded software. What it assumes is therefore a model generation reliable
enough to be left alone over long horizons, plus the two things the team had to build before the
prohibitions were safe — validation the agents cannot see, and an environment those validations can
be run against cheaply and destructively.

The stated cost is the clearest limit. At least $1,000 of tokens per engineer per day is the team's
own benchmark, and [[BlogPosting/how-strongdms-ai-team-build-serious-software-without-even-looking-at-the-code]]
treats that figure as the term deciding whether the arrangement generalises at all, putting it at
roughly $20,000 per engineer per month and arguing that at that level the patterns become a
business-model question. The failure mode the practice is designed against is agents that satisfy
their own tests without satisfying the user, which is why the validating artefact is deliberately
placed where the implementing agents cannot reach it.

How well established it is: this is one team's self-description, published by them and relayed with
its provenance flagged, not a measured result or a convention with multiple independent
practitioners. The claim about what it achieves is theirs; that the software in
question managed user permissions across connected services, and that security software is the last
thing one would expect to be built from unreviewed agent code, is the relaying author's report of a
demo he attended. The broader idea of treating a development organisation
as a factory is not this team's alone — the source itself credits Dan Shapiro with
naming the level of adoption they are implementing — and is covered under
[[DefinedTerm/factory-model]]; this term is the narrower, named practice of one team.

## Related Terms

[[DefinedTerm/factory-model]], [[DefinedTerm/digital-twin-universe]], [[DefinedTerm/review-bottleneck]], [[DefinedTerm/agentic-code-review]], [[DefinedTerm/spec-driven-development]], [[DefinedTerm/output-verifiability]]
