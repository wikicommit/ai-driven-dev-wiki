---
title: "Dark Software Factory"
type: "schema:DefinedTerm"
lang: en
aliases: [dark factory]
tags: [software-factory, human-oversight, verification]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/software-factories/'
    hash: sha256:eb552a385a5d999797ee2b99bf1f369144b5c1e7e2d6b16e30ee78f7654314d1
  - type: url
    url: 'https://simonwillison.net/2026/Sep/27/2026-in-llms-so-far/'
    hash: sha256:385452beca91e7fc01c6dedad958d7ec1fa6f8605175db68befe2a8961aec188
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A software factory run so that code ships without any human having read it, verified only by other machines — named after lights-out manufacturing — as contrasted with a lit factory that keeps human judgment at the review gate and upstream on design and architecture."
---

A dark software factory, in Addy Osmani's description, is a [[DefinedTerm/software-factory]] in which
"code ships that no human has read, verified only by other machines." The image is borrowed from
manufacturing: a dark factory runs with the lights physically off because the only things on the
floor are machines, which do not need light to see. Osmani stresses that the word is used as a
literal physical claim rather than an insult — in software "the floor is the diff," and what makes a
factory dark is that the act of a human reading that diff has been removed. Its counterpart is a lit
factory: the same pipeline with the lights left on where judgment lives, in which agents still do
most of the building but a human reads what comes out before it ships, and human judgment is moved
upstream to the product, the design and the architecture before an agent starts a loop.

## Usage

Osmani presents the dark/lit distinction in [[BlogPosting/software-factories-light-and-dark]] as a
setting chosen loop by loop rather than for a whole factory. Going dark is, he says, surprisingly easy
at first, because removing review makes a team's throughput suddenly seem far higher; the cost is
[[DefinedTerm/comprehension-debt]], which a dark factory "doesn't pay … down; it takes it on as fast
as it can, with the tests green the whole way." He relays a report from a speaker who ran a fully
automated code factory for about four months with no human looking at the code, and found the
resulting failure required painstaking manual debugging to pinpoint.

The name is not Osmani's alone. Recounting [[Organization/strongdm]]'s software factory in
[[BlogPosting/2026-in-llms-so-far]], Simon Willison says Dan Shapiro called that approach the Dark
Factory, after the idea that a sufficiently automated factory can turn the lights out because nobody
needs to see what is going on. The approach he applies it to is defined by two rules StrongDM stated —
code must not be written by humans, and code must not be reviewed by humans — and Willison describes
the team as exploring how to build software without reading the code while still being confident it is
of high quality, and what agents can do to help verify their own work.

## When It Applies

On Osmani's account, a loop can earn fully automated, lights-out status only when its check is cheap,
runs at high frequency, relies on something that cannot easily be faked — green-or-red oracles, type
gates, property tests, a review agent with a real rubric — answers immediately and does not drift over
time. Short loops qualify more easily than long ones. He relays an example described by another
practitioner: a nightly job that fixes exactly one anti-pattern and opens one small pull request. A
loop should stay lit when a wrong answer is expensive and only a person can catch it: subtle
production bugs tests cannot catch, large blast radii, and decisions that will shape a year or more of
work. For loops with high enough stakes, he writes, you do not want to risk waking up to a broken
authentication system, billing engine or public API contract.

The failure he warns of is setting every switch the same way. An all-dark factory leaves a team
"stuck tearing everything down four months later"; an all-lit one leaves nobody able to finish reviews
in time. He argues that better models will not by themselves make dark operation safe, because the
coding agents that feel most capable are trained against their own harness and tools rather than for
long-term maintainability, so the safety net — deliberate architecture with good types, test seams and
well-defined boundaries — has to live outside the model.

How well established it is: the term is a borrowed metaphor and this framing is one practitioner's
argument, supported by reports relayed from others' experience rather than by measured results.

## Related Terms

[[DefinedTerm/software-factory]], [[DefinedTerm/backpressure]], [[DefinedTerm/comprehension-debt]],
[[DefinedTerm/human-in-the-loop]], [[DefinedTerm/humans-on-the-loop]], [[DefinedTerm/review-bottleneck]],
[[DefinedTerm/outer-loop]]
