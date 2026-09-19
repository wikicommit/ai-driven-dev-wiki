---
title: "Sequoia Ascent 2026 summary"
type: "schema:BlogPosting"
lang: en
tags: [agents, ai-assisted-programming, terminology, human-oversight]
sources:
  - type: url
    url: 'https://karpathy.bearblog.dev/sequoia-ascent-2026/'
    hash: sha256:5f0fc28c7d2ce3663820af50aba485b5ec93384a47528a92d2935967dd678dc4
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Andrej Karpathy's write-up of a fireside chat at Sequoia Ascent 2026, arguing that agentic coding crossed a threshold in December 2025 and setting out the framings he uses for it: the context window as a programmable layer, verifiability plus lab attention as the explanation for jagged model capability, and vibe coding as raising the floor while agentic engineering raises the ceiling."
  author: "Andrej Karpathy"
  datePublished: "2026-04-30"
---

This post is Andrej Karpathy's write-up of a fireside chat he gave with Stephanie Zhan at Sequoia
Ascent 2026. It carries two documents: a summary of the conversation's intellectual content, and a
cleaned-up transcript of the event. Both were produced by feeding a model his recent blog posts and
tweets and then the video's transcript; he names the model used, says he read the output and that
it "reads ok without glaring mistakes", and states that he is publishing it so the content is
legible to readers and to other LLMs. So the wording throughout is a model's rendering of what was
said, checked but not written by the speaker.

Its organising claim is that large language models have stopped being chatbots or autocomplete and
have become a new programmable layer for digital work — and that the change became noticeable at a
particular moment. Karpathy dates a step change to around December 2025: where agentic tools had
been useful but needed frequent correction, the generated chunks became larger, more coherent and
reliable enough that he stopped correcting them, which he describes as sending him "down the rabbit
hole of infinite side projects". The unit of programming, on his account, moved from typing lines
to delegating macro actions — implement this feature, refactor this subsystem, research this
library, write tests and fix the failures — so that the programmer becomes an orchestrator of
agents.

## Background

Several of the post's framings are named ideas he has written about elsewhere and restates here.
[[DefinedTerm/software-3-0]] places prompting alongside hand-written code and learned weights as a
third way of programming, with the context window as the lever and the model as the interpreter.
[[DefinedTerm/jagged-intelligence]] explains why capability spikes in some places and collapses in
others, and he offers verifiability plus how much attention the labs paid a domain as the two axes
behind it. An "animals versus ghosts" framing argues that these systems are not animal minds with
drives and curiosity but statistical simulations shaped by pretraining, reinforcement learning and
economic incentive — which he presents as a way to avoid anthropomorphic expectations rather than
as advice with direct practical consequences.

The distinction the post draws between [[DefinedTerm/vibe-coding]] and
[[DefinedTerm/agentic-engineering]] is its most quotable: vibe coding raises the floor, letting
almost anyone create software by describing what they want, while agentic engineering raises the
ceiling and is the professional discipline of coordinating fallible agents without giving up
correctness, security, taste and maintainability. He argues the old "10x engineer" idea understates
how far that ceiling now goes.

Two consequences follow in the post. Hiring, he argues, should test the new skill directly — build
a substantial project with agents, deploy it, secure it, then have adversarial agents try to break
it — rather than set small coding puzzles. And infrastructure should be rewritten for agents rather
than humans: Markdown docs, CLIs, APIs, MCP servers, structured logs, machine-readable schemas,
copy-pasteable agent instructions, safe permissioning, auditable actions and headless setup flows,
which he frames as giving agents sensors and actuators over the world. His recurring test for
whether that has arrived is deployment: building an app was the easy part, while wiring hosting,
auth, payments, DNS, secrets and production settings was not.

The post closes on education, around a line he says he keeps returning to: you can outsource your
thinking, but you cannot outsource your understanding. Even where agents do the work, a person
needs understanding to direct them — to know what is worth building, which result is suspicious and
which tradeoff is acceptable — and he presents LLM-maintained knowledge bases, in which an agent
incrementally compiles messy sources into a persistent wiki of summaries, entity pages, concept
pages, contradictions and cross-links, as a tool for producing that understanding rather than
merely answering questions. He offers this as an example of the broader point that the interesting
question is not only which existing workflow AI can speed up, but which information transformation
was not previously possible at all.

Where he judges the scarce thing to be heading is stated plainly: less scarce are code generation,
API recall, boilerplate, first drafts and repetitive setup; more scarce are understanding, taste,
evaluation design, security, system boundaries, agent orchestration, domain-specific feedback loops
and knowing when the model is off the rails.
