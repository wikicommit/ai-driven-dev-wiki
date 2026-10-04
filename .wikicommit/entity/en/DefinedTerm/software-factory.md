---
title: "Software Factory"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, agents, code-review, verification, software-process]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Feb/7/software-factory/'
    hash: sha256:f037b61ef74329e98d22e3f5e86498585708d651d71581e420890095020b0ad3
  - type: url
    url: 'https://addyosmani.com/blog/human-judgment-doesnt-leave-the-software/'
    hash: sha256:c4cc398bbcb3b786b12103edd73235c1799a0c14110e69dfb8a172809051a0b4
  - type: url
    url: 'https://addyosmani.com/blog/software-factories/'
    hash: sha256:eb552a385a5d999797ee2b99bf1f369144b5c1e7e2d6b16e30ee78f7654314d1
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A name for organizing software development around coding agents running repeatable loops of work. This wiki's sources use it two ways: StrongDM's AI team for their own non-interactive practice in which agents write code that no human writes or reviews, and Addy Osmani for a repeatable, event-driven loop around software work in which human judgment is relocated rather than removed."
---

A software factory is a way of organizing software development around coding agents that run
repeatable loops of work — taking tasks, writing code, running checks — at a scale beyond what a
developer supervises session by session — a framing this page uses to hold together two quite
different usages, which differ sharply on where people sit in it. For [[Organization/strongdm]]'s AI team, who described their
working arrangement publicly under this name, it is non-interactive development in which
specifications plus scenarios drive agents that write code, run harnesses and converge without human
review. For Addy Osmani it is "a repeatable loop around software work" in which human judgment does
not leave but is relocated — upstream to product intent, system design and the quality bar, and
downstream to evidence, risk and ownership of what ships.

## Usage

### StrongDM's AI team

StrongDM's team use the term for their own practice rather than as a general industry category, but it
is not presented as their coinage: the source introduces them as a team implementing what it says Dan
Shapiro called the Dark Factory level of AI adoption. What is theirs is the definition above and the
two prohibitions they state with it — code must not be written by humans, and code must not be
reviewed by humans. A third, practical statement accompanies them — that if a team has not spent at
least $1,000 on tokens per human engineer per day, its software factory has room for improvement.

The prohibition on review is what the rest of the practice exists to make survivable. The relaying
author frames the problem the team ran into as the obvious one — if nothing is written by hand, how
do you ensure the code works? — and notes that having the agents write tests only helps if they do
not cheat. Their answer has three
named parts. **Scenarios**, a word they say they repurposed — the source
describes their answer as inspired by scenario testing — are end-to-end user stories they say are
often held *outside* the codebase — the comparison they draw is to a holdout set in model training. The
relaying author reads this as keeping them where the coding agents cannot see them; that reading is
his gloss rather than the team's stated rationale. Each scenario is meant to be intuitively
understandable and flexibly validated by an LLM.
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

### Addy Osmani

In [[BlogPosting/human-judgment-doesnt-leave-the-software-factory]], Osmani defines a software
factory as "a repeatable loop around software work" and distinguishes it from simply using a coding
harness. A stock harness such as Claude Code or Codex, run across multiple sessions with good specs
that build in verification and constraints, gets "surprisingly far" on his account; a factory is worth
adding when the work needs to be repeatable and event-driven — an event-driven queue of work such as
Slack triggers, GitHub issues, Linear or a backlog, run in an isolated cloud environment to handle
triage, implementation and testing with some explicit human babysitting. Some, he notes, end the loop
with a monitor agent watching production and filing issues that are triaged again.

What makes a factory useful, in his telling, is coordination rather than code generation: making
runs behave consistently, handing work between agents, keeping two sessions from claiming the same
issue, preserving evidence, and stopping production when human review falls behind. The people in it
can shape work early, steer it during implementation, take it through a handoff, or stop it from
shipping, rather than only approving a final diff. Much of a responsible factory's time, he says, goes
to verification, which he proposes allocating through a [[DefinedTerm/verification-budget]].

In an earlier post, [[BlogPosting/software-factories-light-and-dark]], Osmani builds the term up from
three layered concepts. A loop is one agent doing a single job on repeat — gather context, take an
action, check the result, go again until a condition is met. A harness is "the walls around a loop":
its sandbox, the tools it can reach, the memory that survives between runs and the gates that decide
what done means. A software factory is "many harnessed loops running at once, fed by a queue of work
and drained through a review gate into production, with humans owning the whole thing from above" —
"not a bigger agent" but "an org chart made of loops." In that telling every stage but one runs at
close to zero cost; the review gate, where judgment lives, is the one that resists scaling. He
distinguishes a [[DefinedTerm/dark-software-factory]], in which code ships that no human has read, from
a lit one that keeps human judgment upstream on the product, design and architecture and at the review
gate, and argues that which loops may run dark should be decided one loop at a time.

## When It Applies

On StrongDM's own account the practice became viable at a specific point: they date their catalyst to
a transition observed in late 2024, stating that with the second revision of Claude 3.5 long-horizon
agentic coding workflows began to compound correctness rather than error. The team formed in July
2025 on the rule of no hand-coded software. What it assumes is therefore a model generation reliable
enough to be left alone over long horizons, plus two things the team built alongside the
prohibitions — validation held outside the codebase, and an environment those validations can be run
against at volume.

The stated cost is the clearest limit. At least $1,000 of tokens per engineer per day is the team's
own benchmark, and [[BlogPosting/how-strongdms-ai-team-build-serious-software-without-even-looking-at-the-code]]
puts that figure at roughly $20,000 per engineer per month, saying that at that level the patterns are
far less interesting to him and become more of a business-model exercise, while hoping they can be put
into play with a much lower spend. The failure mode the practice is designed against is agents that satisfy
their own tests without satisfying the user — the relaying author's point that having agents write
tests only helps if they do not cheat.

Osmani's version assumes the opposite of StrongDM's prohibition on review: someone still chooses the
problem and the architecture, sets the quality bar, decides which verification signals deserve trust
and decides when the evidence is sufficient to ship, so that code review is concentrated where
automated back-pressure breaks down or maintainability trade-offs must be made. The failures he warns
of are a factory that shows green when it is not — an agent changing a test or the code to pass it
without following the intent behind it — untrusted input such as an issue or Slack message carrying
adversarial content, and a volume of parallel work that outruns the reviewer's understanding. He
advises asking first whether a factory is needed at all.

How well established it is: both versions are practitioners' own accounts rather than measured
results. StrongDM's is one team's self-description, published by them and relayed with its provenance
flagged; the claim about what it achieves is theirs, and that the software in question managed user
permissions across connected services, and that security software is the last thing one would expect
to be built from unreviewed agent code, is the relaying author's report of a demo he attended.
Osmani's draws on his own sample factory and day-to-day practice. The broader idea of treating a
development organisation as a factory is not either party's alone — the StrongDM source itself credits
Dan Shapiro with naming the level of adoption that team is implementing — and is covered under
[[DefinedTerm/factory-model]].

## Related Terms

[[DefinedTerm/factory-model]], [[DefinedTerm/digital-twin-universe]], [[DefinedTerm/review-bottleneck]], [[DefinedTerm/agentic-code-review]], [[DefinedTerm/spec-driven-development]], [[DefinedTerm/output-verifiability]], [[DefinedTerm/verification-budget]], [[DefinedTerm/dark-software-factory]]
