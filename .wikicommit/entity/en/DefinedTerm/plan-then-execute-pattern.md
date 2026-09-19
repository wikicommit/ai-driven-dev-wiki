---
title: "Plan-Then-Execute Pattern"
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
  description: "A design pattern for prompt-injection resistance in which the agent commits to its sequence of tool calls before any untrusted content is read, so that tool output can shape the content of later steps but never which steps are taken."
---

The plan-then-execute pattern constrains an LLM agent by fixing the plan first. The agent decides
which tool calls it will make before it has been exposed to any untrusted content, and then carries
that plan out; tool output is allowed back into the agent, but it arrives too late to change what
the agent has already committed to doing. As summarized in
[[BlogPosting/design-patterns-for-securing-llm-agents]], the paper describes this as a more
permissive approach than refusing feedback altogether: it allows feedback from tool outputs back to
the agent while preventing those outputs from influencing the choice of actions the agent takes.

## Usage

The worked example given is a request to send today's schedule to a named recipient, planned in
advance as a calendar read followed by an email write addressed to that recipient. The protection is
partial and the boundary is precise: text returned by the calendar read might corrupt the body of
the email that goes out, but it cannot change who the email is sent to, because the recipient was
fixed before anything untrusted was read.

That division — content is at risk, control flow is not — is what the pattern buys. It permits
more sophisticated sequences of actions than a pattern that admits no feedback at all, without the
risk that one action introduces instructions that trigger unplanned harmful actions later on.

## When It Applies

The pattern applies where a useful plan can be formed from the user's request alone, before any
external data is consulted. It assumes the consequential decisions — which tools run, and with
what irreversible parameters — can all be settled at planning time. It fails where the right next
step genuinely depends on what was retrieved, since an agent that re-plans after reading untrusted
content has given up the property the pattern rests on. It also leaves the content of later steps
exposed, so it is misapplied if the damage an attacker could do lies in what a message says rather
than in where it goes.

It is one of six patterns presented together in the reviewed paper as trade-offs between an
agent's utility and its resistance to [[DefinedTerm/prompt-injection]], rather than as a ranked
list. The account available here is that paper's reviewer rather than the paper itself.

## Related Terms

- [[DefinedTerm/action-selector-pattern]] — the stricter neighbour, which admits no tool output at all
- [[DefinedTerm/llm-map-reduce-pattern]] — addresses the exposure this pattern leaves open, by
  routing untrusted content through sub-agents
- [[DefinedTerm/prompt-injection]] — the attack being constrained
- [[BlogPosting/design-patterns-for-securing-llm-agents]] — the source of this account
