---
title: "meta-harness"
type: "schema:DefinedTerm"
lang: en
tags: [agent-harness, architecture, terminology]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/managed-agents'
    hash: sha256:0e4e8bf6d9cb724da07f95297d00f7077a224890c85346851d0d455eba93d529
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A system that is deliberately unopinionated about which specific agent harness runs inside it, providing instead a set of general interfaces — for state and for computation — that many different harnesses can be built against."
  termCode: ""
  inDefinedTermSet: ""
---

A meta-harness is a system that supplies general interfaces around a model rather than a particular loop, so that many different harnesses can run inside it. The term is used in [[TechArticle/scaling-managed-agents]] to describe [[SoftwareApplication/claude-managed-agents]]: "a meta-harness in the same spirit, unopinionated about the *specific* harness that Claude will need in the future," but opinionated about the interfaces around it.

## Usage

The problem it answers is stated as an old one in computing: how to design a system for "programs as yet unthought of." Operating systems solved it by virtualising hardware into abstractions — process, file — general enough for programs that did not yet exist, so that a `read()` call is agnostic between a 1970s disk pack and a modern SSD, and the abstractions outlast the hardware underneath.

The motivating problem in the agent case is that a harness encodes assumptions about what the model cannot do on its own, and those assumptions expire. The example that account gives is a behaviour it calls **context anxiety** — a model wrapping up tasks prematurely as it sensed its context limit approaching — which was addressed by adding context resets to the harness, only for the behaviour to be absent on a later model, leaving the resets as dead weight.

What a meta-harness commits to, on that account, is a minimal set of expectations: that the model will need to manipulate state (a session) and perform computation (a sandbox), and that it will need to scale to many brains and many hands. What it declines to assume is the number or location of those brains and hands, or the shape of the loop between them. Its stated test is accommodating harnesses that already exist and differ — a general-purpose coding harness used widely across tasks, and task-specific harnesses that excel in narrow domains — without privileging any of them.

## Related Terms

A meta-harness is one layer above the [[DefinedTerm/agent-harness]] it hosts, and its durability argument is the reason [[DefinedTerm/agent-scaffolding]] decisions are worth separating from interface decisions. Its treatment of stored state as interrogable rather than summarised is a different answer to the same problem [[DefinedTerm/compaction]] and [[DefinedTerm/agentic-memory]] address.
