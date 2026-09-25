---
title: "Backpressure"
type: "schema:DefinedTerm"
lang: en
aliases: ["Back pressure"]
tags: [agentic-coding, verification]
sources:
  - type: url
    url: 'https://ghuntley.com/ralph/'
    hash: sha256:9836ee3ee0773613f370a27796b1e456199be38681f73a47b974e210dd356317
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "In an autonomous AI coding loop, whatever is wired into the loop to reject invalid generated code — a language's type system, tests, static analysers, security scanners."
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

## When It Applies

It applies to agents that generate code in unattended loops, where no human reviews each iteration
and the checks are what keep a bad change from being built upon. It assumes such checks exist and run
quickly enough not to stall the loop. The author says that in a dynamically typed language, running a
loop without a static analyser or type checker leads to "a bonfire of outcomes", and he pairs it with
a second practice: because each loop starts with a fresh context, the agent is asked to record why
each test matters, so later loops can judge whether a failing test should be fixed, changed or
deleted. The framing is one practitioner's, argued from his own experience building a compiler rather
than from a measured comparison.
