---
title: "Backpressure"
type: "schema:DefinedTerm"
lang: en
aliases: ["Back pressure", "Back-pressure"]
tags: [agentic-coding, verification]
sources:
  - type: url
    url: 'https://ghuntley.com/ralph/'
    hash: sha256:9836ee3ee0773613f370a27796b1e456199be38681f73a47b974e210dd356317
  - type: url
    url: 'https://addyosmani.com/blog/agentic-code-quality/'
    hash: sha256:56349ced5b7fdba7ce2fa4ec5b60235f5fff08ae8eda38b2493c358817cec69f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "In AI-driven software delivery, the checks wired into the loop around an agent that reject invalid or low-quality generated code — type systems and compilers, tests, static analysers, security scanners or policies, CI deployment gates."
---

In the autonomous coding loop described by Geoffrey Huntley, backpressure is whatever is wired into
the loop to reject invalid code generation. His premise is that generating code is now cheap and what
is hard is ensuring the agent has generated the right thing, so the checks that push back against bad
output become where the engineering effort goes. Some programming languages supply it inherently
through their type systems; beyond that, anything can serve — tests, static analysers, security
scanners — so long as it rejects invalid output and, collectively, lets the loop turn fast.

## Usage

The usage described here is from [[BlogPosting/ralph-wiggum-as-a-software-engineer]], where backpressure is the
second phase of the [[DefinedTerm/ralph-loop]] after generation. There the author's standing
instruction is that after implementing functionality or fixing a problem, the agent runs the tests for
the unit of code it changed. He treats the choice of language as a trade-off along the same axis:
Rust's type system gives the extreme correctness he wanted for a compiler, but its slow compilation
and the model's difficulty producing correct Rust in one attempt mean more attempts per change — "the
speed of the wheel turning", in his phrase, balanced against correctness. The same post uses the term
for a failure: fanning build and test out to hundreds of parallel subagents produces bad backpressure,
which is why its prompt allows many subagents for searching and writing files but only one for build
and test.

Addy Osmani uses the term at the scale of a whole delivery pipeline in [[BlogPosting/agentic-code-quality]].
There back-pressure can be implemented through many tools — compilers rejecting invalid code, tests
failing, security policies blocking bad practices, CI declining to deploy — and all the constraints
that keep production flowing to a quality standard create back-pressure in the pipeline. He argues
it should ideally exist throughout the loop rather than as a single review at the very end, so that
the signals are used as early as possible rather than waiting for CI to refuse a deployment.

## When It Applies

It applies to agents that generate code in unattended loops, where no human reviews each iteration
and the checks are what keep a bad change from being built upon. It assumes such checks exist and run
quickly enough not to stall the loop. The author says that in a dynamically typed language, running a
loop without a static analyser or type checker leads to "a bonfire of outcomes", and he pairs it with
a second practice: because each loop starts with a fresh context, the agent is asked to record why
each test matters, so later loops can judge whether a failing test should be fixed, changed or
deleted. The framing is one practitioner's, argued from his own experience building a compiler rather
than from a measured comparison.

Osmani names the case where it breaks down at pipeline scale: when the volume of changes exceeds what
the checks can consume, work queues up behind verification that moves at human speed. His options are
to scale the verification system, reduce the rate at which agents generate changes, or lower the
quality bar, and he recommends applying strong constraints where they matter most while relaxing
those that serve no purpose. This too is presented as one author's argument rather than a measured
result.
