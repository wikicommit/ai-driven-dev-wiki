---
title: "Software Factories, Light and Dark"
type: "schema:BlogPosting"
lang: en
tags: [software-factory, verification, human-oversight, harness-engineering]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/software-factories/'
    hash: sha256:eb552a385a5d999797ee2b99bf1f369144b5c1e7e2d6b16e30ee78f7654314d1
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "Addy Osmani's account of the software factory as harnessed agent loops run at scale, contrasting a dark factory — code shipped that no human has read — with a lit one that keeps human judgment upstream and at the review gate, and arguing that verification rather than generation is the factory's real constraint."
  author: "Addy Osmani"
  datePublished: "2026-07-20"
---

This post describes a [[DefinedTerm/software-factory]] as "harnessing loops at scale" and builds it up
from three layered concepts. A loop is one agent doing a single job on repeat — gather context, take
an action, check the result, go again until a condition is met. A harness is "the walls around a
loop": the sandbox it runs in, the tools it can reach, the memory that survives between runs and the
gates that decide what done means. A factory is "many harnessed loops running at once, fed by a queue
of work and drained through a review gate into production, with humans owning the whole thing from
above" — "not a bigger agent" but "an org chart made of loops."

Against that structure it contrasts two ways of running a factory. In a
[[DefinedTerm/dark-software-factory]], agents scope, build and ship code without anyone really reading
it; in a lit one, a human reads what comes out before it ships, and human judgment moves upstream to
the product, the design and the architecture. The author's warning is that "if people stop reading,
they'll stop understanding your software," and that the hardest job now is deciding which checks to
build and how much autonomy to delegate.

## Key Points

- The author presents the software factory as an old idea: for half a century many have dreamed of software as a repeatable, instrumentable production process rather than an individual craft, a dream he says has generally fallen flat, partly because of the difficulty of stamping out ideas — and which changes in the last two years make worth a fresh look.
- The point of loop engineering, the author writes, is to stop prompting an agent turn by turn and instead design the small system that prompts it; see [[DefinedTerm/loop-engineering]].
- Drawn as a closed loop, a factory runs from intent and production signals into a queue, through the harness, automated checks and a review gate, to deployment and monitoring that feed back into signals. Every box but one is close to zero cost; the review gate — judgment — is the one that resists scaling.
- The "dark" metaphor is borrowed from lights-out manufacturing, where only machines are on the floor; in software, the author says, "the floor is the diff," and a dark factory ships diffs verified only by the machines that built them.
- A dark factory takes on [[DefinedTerm/comprehension-debt]] — which the post defines as "the widening gap between how much code exists and how much any human still understands" — as fast as it can, with the tests green the whole way, and its reckoning will be "quiet and late."
- "The bottleneck was never generation": the post defines back pressure as the rule that a loop can be handed only as much autonomy as can be cheaply and reliably verified, and argues that improving models will not automatically close the gap, because architectural quality is measured over months and years rather than in fast, crisp evaluations; see [[DefinedTerm/backpressure]].
- The safety net of a lit factory is ordinary architecture — good types and signatures, test seams, legible layout, short call stacks, well-defined component boundaries and dependency injection — which now does "a second job" as a cheap, hard-to-fake check on agent mistakes, and which the author says has to live outside the model.
- A loop earns full automation only if its check is cheap, runs at high frequency, cannot be easily faked, answers immediately and does not drift; short loops are easier to verify than long ones. A loop should stay lit where a wrong answer is expensive and only a person can catch it — subtle production bugs, large blast radii, and decisions that will shape a year or more of work.
- The danger is setting every switch the same way: all dark leads to tearing everything down months later, all lit to an unmanageable review bottleneck.
- Structuring agent work as a predefined directed graph of steps and conditional edges, rather than a free loop in which the model picks each path, is described as "back pressure drawn as a diagram" — giving up some agent freedom for mandatory checks and legible failure points. The author clarifies that "graph" here means a workflow graph, not a knowledge graph.
- The human never left the factory but moved: engineers should own the [[DefinedTerm/outer-loop]] — deciding whether a fix is the right approach, verifying the diagnosis and implementation, approving the change and carrying the consequences — with evidence (diffs, tests, logs and a brief explanation connecting them) as the boundary between the inner and outer loops.

## Context

The post builds on a conference talk by a co-founder of HumanLayer on why software factories fail, and offers the author's own take on that talk's central diagram. Several of its claims are relayed from that speaker: his report of running a fully automated code factory for about four months without any human looking at the code, a rule of thumb that an agent holds up for three to ten steps and loses the thread past twenty, and a nightly automated job that fixes one anti-pattern and opens one small pull request.

It names Claude Code and Codex as agents reinforcement-trained against their own harness and tools, fluent with the idioms of the trade but not with long-term maintainability. It links to other writing by the author on the [[DefinedTerm/factory-model]], on owning the outer loop, on comprehension debt, on loop engineering and on human judgment in the software factory. The post notes that Pangram scored it as 100% human-written.
