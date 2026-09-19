---
title: "Source-Sink Analysis"
type: "schema:DefinedTerm"
lang: en
tags: [security, prompt-injection, agent-safety]
sources:
  - type: url
    url: 'https://openai.com/index/designing-agents-to-resist-prompt-injection/'
    hash: sha256:a6abdf1b681484a9400a9cdf6ae01a404d4dba8657ede15473b45bfd66d74271
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A traditional security-engineering framing applied to AI agents, in which an attack requires both a source — a way to influence the system — and a sink, a capability that becomes dangerous in the wrong context. Breaking either half prevents the attack, which shifts attention from classifying inputs to constraining capabilities."
---

Source-sink analysis is a security-engineering framing in which an attacker is understood to need
two things rather than one: a **source**, meaning a way to influence the system, and a **sink**,
meaning a capability that becomes dangerous in the wrong context. As applied to agents in
[[BlogPosting/designing-ai-agents-to-resist-prompt-injection]], that combination typically means
untrusted external content paired with an action such as transmitting information to a third party,
following a link, or interacting with a tool.

Its usefulness in this setting is that it gives a second place to intervene. Where a defence built
only around detecting malicious input must win every time at the source, this framing treats the
sink as equally available to defend — which matters given the same post's argument that classifying
manipulative content is close to the problem of detecting a lie, and that fully developed attacks
are not usually caught that way.

## Usage

The post describes combining this framing with its social-engineering model of how agent attacks
actually work. The security expectation it derives is stated in terms of sinks: potentially
dangerous actions, or transmissions of potentially sensitive information, should not happen silently
or without appropriate safeguards. [[DefinedTerm/safe-url]] is the concrete mechanism it reports
building on that basis, operating on the transmission rather than on the incoming content.

## When It Applies

The framing applies wherever an agent combines exposure to outside content with capabilities that
have consequences, and it assumes that the dangerous capabilities can be enumerated — a sink nobody
identified is not defended. It is a way of organizing where controls go rather than a control
itself, so it produces no protection until something is actually done at one end or the other.

How well-established it is: the post presents it not as a new proposal but as one of the more
traditional security engineering approaches, brought across to agentic systems and combined with its
own social-engineering model. The account available here is a single vendor's description of how it
reasons about its own products.

## Related Terms

- [[DefinedTerm/prompt-injection]] — the attack the framing is applied to
- [[DefinedTerm/safe-url]] — the sink-side mitigation built on this framing in the same source
- [[DefinedTerm/control-data-plane-confusion]] — a different structural account of why this attack
  class resists elimination
- [[DefinedTerm/guardrails]] — the controls placed at the sink end
- [[BlogPosting/designing-ai-agents-to-resist-prompt-injection]] — the source of this account
