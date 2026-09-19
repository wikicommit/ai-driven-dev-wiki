---
title: "Safe Url"
type: "schema:DefinedTerm"
lang: en
tags: [security, prompt-injection, agent-safety, exfiltration]
sources:
  - type: url
    url: 'https://openai.com/index/designing-agents-to-resist-prompt-injection/'
    hash: sha256:a6abdf1b681484a9400a9cdf6ae01a404d4dba8657ede15473b45bfd66d74271
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "OpenAI's named mitigation against data exfiltration by a manipulated assistant: a mechanism that detects when information the assistant learned during a conversation would be transmitted to a third party, and either shows the user what would be sent and asks for confirmation, or blocks it and tells the agent to find another way."
---

Safe Url is a mitigation described by OpenAI in
[[BlogPosting/designing-ai-agents-to-resist-prompt-injection]], aimed at the case where an
assistant has already been convinced by an attacker. It is designed to detect when information the
assistant learned in the conversation would be transmitted to a third party. On detection, the
system either shows the user the information that would be transmitted and asks them to confirm, or
blocks the transmission and tells the agent to try another way of moving forward with the user's
request.

Its place in the defence is deliberately last. The post states that the attacks most commonly seen
against its assistant attempt to convince it to take secret information from a conversation and send
it to a malicious third party, and that in most known cases those attacks fail because safety
training causes the agent to refuse. Safe Url is presented as what handles the rare remainder — the
cases where the agent is convinced — rather than as the primary barrier.

## Usage

The mechanism follows from the [[DefinedTerm/source-sink-analysis]] framing set out in the same
post: an attacker needs both a source and a sink, and for agentic systems the sink is often an
action that transmits information to a third party, follows a link, or interacts with a tool. Safe
Url operates on that sink, and the security expectation it is meant to uphold is that potentially
dangerous actions or transmissions of sensitive information should not happen silently or without
appropriate safeguards.

The same mechanism is reported as applying beyond chat: to navigations and bookmarks in the
vendor's browser product, and to searches and navigations in its deep research product. Its canvas
and apps features are described as taking a similar approach, running in a sandbox able to detect
unexpected communications and ask the user for consent.

## When It Applies

The mitigation applies where an agent holds information from a conversation and has some capability
that could move it outward. It assumes that such transmissions can be recognized before they happen
and that a user is present to confirm when the system chooses to ask rather than block — so it is a
[[DefinedTerm/human-in-the-loop]] control in the confirming case, with the limits that implies for
an unattended agent. It is aimed at exfiltration specifically, not at manipulation whose damage is
done through some other consequential action.

How well-established it is: this is one vendor's description of its own deployed defence, published
on its own site. The post states that a paper about the mechanism's structure exists at a separate
dedicated post, but gives no effectiveness figures here, and no independent evaluation is present in
this source.

## Related Terms

- [[DefinedTerm/prompt-injection]] — the attack class this mitigates the consequences of
- [[DefinedTerm/source-sink-analysis]] — the framing that identifies the transmission as the sink to
  defend
- [[DefinedTerm/human-in-the-loop]] — the confirmation step the mechanism falls back on
- [[DefinedTerm/guardrails]] — the broader family of controls placed around an agent's actions
- [[BlogPosting/designing-ai-agents-to-resist-prompt-injection]] — the source of this account
