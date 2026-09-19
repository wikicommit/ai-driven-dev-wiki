---
title: "Action-Selector Pattern"
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
  description: "A design pattern for prompt-injection resistance in which an agent may trigger external actions but is never exposed to their results, so that nothing an action returns can influence what the agent does next. Described in the paper reviewed by Simon Willison as an LLM-modulated switch statement."
---

The action-selector pattern is a way of building an LLM agent so that it can take external actions
while remaining immune to [[DefinedTerm/prompt-injection]]: the agent may trigger tools, but no
feedback from those tools is allowed back into it. Because the agent never reads what an action
returns, adversarial text sitting in a web page or an email cannot reach the agent at all, and so
cannot redirect it.

As summarized in [[BlogPosting/design-patterns-for-securing-llm-agents]], the paper that proposes
it describes this as a relatively simple pattern that makes agents immune to prompt injections while
still allowing them to take external actions, achieved by preventing any feedback from those actions
back into the agent. The paper summarizes the pattern as an "LLM-modulated switch
statement", a description the post says feels accurate to it.

## Usage

The cost of the pattern is what the agent may no longer do. Actions whose whole purpose is to
retrieve something — reading an email, fetching a web page — are unavailable, because their value
lies precisely in the response the agent is forbidden to see. What remains are actions that are
complete in themselves: the examples given are sending the user to a web page, or displaying a
message to the user.

## When It Applies

The pattern applies where the useful work can be expressed as a choice among known actions rather
than as a process that reacts to what those actions return. It assumes such a set of actions can be
enumerated in advance, and that none of them needs to feed a result back for the agent to decide
what to do next. It is misapplied wherever a tool's output must inform a later step, and its
protection disappears the moment any return value is routed back into the agent's context.

It is one of six patterns presented together, all resting on a single premise: that once an agent
has ingested untrusted input it must be constrained so that input cannot trigger consequential
actions. The account available here is a review of that paper rather than the paper itself, and the
paper frames its patterns as offering a valuable trade-off between agent utility and security.

## Related Terms

- [[DefinedTerm/plan-then-execute-pattern]] — the more permissive neighbour, which does allow tool
  output back into the agent while protecting the choice of actions
- [[DefinedTerm/dual-llm-pattern]] — another of the six, which isolates untrusted content behind a
  second model instead of refusing feedback outright
- [[DefinedTerm/prompt-injection]] — the attack the pattern is designed to make structurally
  impossible
- [[BlogPosting/design-patterns-for-securing-llm-agents]] — the source of this account
