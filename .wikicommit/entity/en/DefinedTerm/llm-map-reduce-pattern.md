---
title: "LLM Map-Reduce Pattern"
type: "schema:DefinedTerm"
lang: en
tags: [security, prompt-injection, agent-architecture, agent-safety]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Jun/13/prompt-injection-design-patterns/'
    hash: sha256:bd74a0ffe03b1f53850aa0b16d091950d2f2544de525ebb6dade120e2b8ab4c4
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A design pattern for prompt-injection resistance in which a coordinating agent dispatches sub-agents to read untrusted content and returns only their constrained results for safe aggregation, so that no untrusted text reaches the coordinator directly."
---

The LLM map-reduce pattern isolates untrusted content inside sub-agents. A coordinating agent
directs sub-agents that are each exposed to some piece of untrusted material; their results are then
aggregated, and it is the aggregate rather than the raw content that informs what happens next. As
summarized in [[BlogPosting/design-patterns-for-securing-llm-agents]], this answers a limitation of
the pattern before it in the same paper — where malicious instructions could still affect the
*content* passed to a later step — by keeping the untrusted text inside a component whose output
shape is constrained.

The name is borrowed from the classic map-reduce framework for distributed computation, which the
post says is what the structure reflects.

## Usage

The example given is an agent asked to find the files containing a month's invoices and send them to
an accounting department. Each file is handed to its own sub-agent, which responds with a boolean
indicating only whether that file is relevant. Files judged relevant are then aggregated and sent.

What does the protective work is the narrowness of what a sub-agent may return. A sub-agent that has
read attacker-controlled text can still be subverted, but a boolean is a very small channel: the
worst it can express is a wrong answer about one file, not a new instruction for the coordinator.

## When It Applies

The pattern applies where a task over untrusted material decomposes into independent per-item
judgements that can each be reduced to a constrained answer. It assumes such a reduction exists and
that the coordinator never needs the underlying text. It is misapplied where the sub-agent's result
must be rich enough to carry attacker-controlled prose back — at that point the untrusted content
has simply been relayed rather than contained — and it offers nothing against a sub-agent being
wrong about the items it was given.

It is one of six patterns presented together in the reviewed paper as trade-offs between utility
and resistance to [[DefinedTerm/prompt-injection]]. The account available here is the paper's
reviewer rather than the paper itself.

## Related Terms

- [[DefinedTerm/plan-then-execute-pattern]] — the pattern whose remaining content-level exposure this
  one addresses
- [[DefinedTerm/dual-llm-pattern]] — the neighbouring pattern that also quarantines untrusted reading
  behind another model, returning symbolic variables rather than aggregated judgements
- [[DefinedTerm/sub-agent-architecture]] — the general structure this pattern puts to a security use
- [[BlogPosting/design-patterns-for-securing-llm-agents]] — the source of this account
