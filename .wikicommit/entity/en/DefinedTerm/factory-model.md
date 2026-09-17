---
title: "Factory Model"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/factory-model/'
    hash: sha256:5c88d875dc4b49c7cdcb8bc777758f860985d09734d623a7d4b1817af75e9a35
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Addy Osmani's mental model for agentic software development: rather than writing code directly, a developer builds and runs a factory — a fleet of parallel AI coding agents, each with its own task, toolbelt, context, and feedback loop — whose output quality depends on the specification and testing discipline behind it rather than on typing speed."
---

The factory model is Addy Osmani's mental model for agentic software development: rather than writing code directly, a developer builds and runs a factory — a fleet of AI coding agents working in parallel, each with its own task, toolbelt (repositories, test runners, deployment scripts, documentation), context (specs, architecture decisions, prior constraints), and feedback loop. Instead of hand-holding one agent through one task, a developer spins up several agents at once — one on a backend refactor, another on a feature, another on integration tests, another on documentation — and reviews outputs, gives feedback, refines specs, and redeploys.

## Usage

Osmani extends the factory analogy on several points he treats as holding directly: a factory has quality control, has process documentation, has inputs that must be precisely specified or the output comes out wrong, and stalls when its environment is unreliable. He reports that inside teams that have adopted the model aggressively, a substantial portion of merged pull requests now originate from agents running autonomously in cloud environments, presenting this as production reality rather than theory. He connects the model to public remarks from Cursor, quoting it as saying "the developer's job is becoming building the system that builds the software, the factory, not just the product" and "reviewing ideas is a lot more fun than reviewing code."

## When It Applies

Osmani presents the factory model as the appropriate approach once a developer is directing autonomous agents that can run largely unsupervised for extended periods, rather than a single synchronous agent handled step by step. It assumes a developer can write and maintain a specification precise enough to survive being run against by many agents at once, plus a comprehensive, test-first suite to check the results — without those, he argues, ambiguous requirements and poor architectural decisions propagate across the whole fleet rather than staying contained to one implementation. He presents it as his own mental model for this shift, while reporting it as already production reality inside some engineering organizations.

## Related Terms

[[BlogPosting/code-agent-orchestra]], [[DefinedTerm/conductor-and-orchestrator-modes]], [[DefinedTerm/red-green-tdd]]
