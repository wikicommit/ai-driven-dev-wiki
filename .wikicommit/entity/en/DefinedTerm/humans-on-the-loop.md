---
title: "Humans on the loop"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, harness-engineering, human-oversight]
aliases: ["On the loop"]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html'
    hash: sha256:767b9a865639b9476811d14704d9d23901875bda1ac1263f9794e9aa70ba663c
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A position for humans in agentic software development, proposed by Kief Morris, in which people build and improve the harness that controls how agents produce software, rather than leaving agents unsupervised or inspecting each artefact they produce."
---

Humans on the loop is a position for people in agent-driven software development, named by Kief
Morris in [[BlogPosting/humans-and-agents-in-software-engineering-loops]], in which humans build and
manage the working loop instead of either leaving agents to it or micromanaging what they produce.
It is defined against two alternatives within the author's model of a **why loop** (turning ideas
into working software, run by humans) and a **how loop** (building the software through intermediate
artefacts such as specs, code and tests): humans *outside* the loop, who leave the how loop to agents,
and humans *in* the loop, who act as gatekeepers inside its innermost level, for instance by inspecting
each line of generated code. On the loop, humans shape the how loop itself through the agent's
harness — the specifications, quality checks and workflow guidance that control its levels.

## Usage

The article identifies the practice of building and maintaining those harnesses,
[[DefinedTerm/harness-engineering]], as how humans work on the loop. Its clearest test is what happens
when an agent's output, including an intermediate artefact, is not satisfactory: the in-the-loop
response is to fix the artefact, by editing it or telling the agent what to correct; the on-the-loop
response is to change the harness that produced it so that it produces the wanted results. Outcomes
then improve by continuously improving the harness. The article notes that something like this
concept has also been described as the "middle loop" — moving human attention to a loop above the
coding loop.

## When It Applies

The proposal assumes agents that can be given guidance and quality checks to judge their own work,
on the "shift left" reasoning that agents, like developers, do better when they can gauge quality
themselves than when they rely on someone to check for them. It is offered against the bottleneck
created when humans inspect everything agents generate, and against the loss of the internal quality
that affects the time and cost of agent work when humans stay out entirely. It is one author's
framing, not a measured result; he extends it to the [[DefinedTerm/agentic-flywheel]], in which agents
themselves recommend and apply harness improvements.

## Related Terms

- [[DefinedTerm/human-in-the-loop]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/agentic-flywheel]]
- [[DefinedTerm/vibe-coding]]
