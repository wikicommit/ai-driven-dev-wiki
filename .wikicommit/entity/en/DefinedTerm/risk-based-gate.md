---
title: "Risk-Based Gate"
type: "schema:DefinedTerm"
lang: en
tags: [agents, human-oversight, guardrails, governance]
sources:
  - type: url
    url: 'https://www.port.io/blog/human-in-the-loop-for-ai-coding-agents'
    hash: sha256:766abcbeb6946c92580399d54cd8330c0edeb8fda6e8e61aefb36579d744524c
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A non-deterministic guardrail in which an agent scores a specific action against its current context and a human is pulled in only when that score crosses a set threshold."
---

A risk-based gate is a non-deterministic guardrail on an agent's actions: instead of checking a
condition written in advance, it has an agent assess the specific action in its actual context and
decide how risky it is right now, producing a risk score, and a human is pulled in only if that
score crosses a threshold the organisation sets. The answer is calculated fresh each time. The term
is one half of a pair proposed in [[BlogPosting/do-you-really-need-a-human-in-every-loop]], the
other being a [[DefinedTerm/rule-based-gate]].

## Usage

The worked example is an agent proposing a change that looks small but sits on a service half an
organisation's tier-1 systems depend on: nobody wrote a rule for that exact change, and the gate
works it out from context. The scoring described traces how far a change reaches through a
connected graph of an organisation's systems — which services depend on it, what deployed recently,
what it touches downstream — and uses that to judge how risky the action actually is, letting a
small contained change run while a change that ripples across tier-1 services pulls in a human.

Because the decision is a judgment rather than a fixed rule, the post sets three requirements for
running one. It needs a threshold set for when a human gets pulled in, and the post expects that
threshold to be tuned over time. It needs tracing on every decision, including what the model
scored and what context it used, because a call that changes with context is only trustworthy if
it can be reconstructed. And it needs a fallback to a blocking human review when the model is
unsure or the context is thin, so that thin context produces a review rather than a silent pass.
The post's warning is that skipping these leaves an unaudited judgment call in a system that cannot
be questioned later.

## When It Applies

The dividing line the post draws is lookup versus judgment, not whether context matters — rules
handle plenty of context such as time and environment. A risk-based gate is for decisions that
cannot be reduced to a clean condition: its examples are a change whose blast radius reaches across
a dependency graph, where the risky combinations cannot be enumerated; classifying how severe or
risky an incident really is, where severity is not always a clean field; and a deploy that looks
normal but is anomalous for that particular service, where catching "off" requires weighing many
signals rather than checking one.

Its dependency on context is stated as sharper than a rule's, because scoring a blast radius or
classifying an incident means reading the whole connected picture — what depends on what, what
changed recently, who owns it — and a risk score computed over thin context just hides a bad guess
behind a number. This formulation is one vendor's, advanced in a post that concludes by
recommending that vendor's own platform, and the post expects most teams to run both kinds of gate
rather than choosing one.

## Related Terms

[[DefinedTerm/rule-based-gate]], [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/guardrails]],
[[DefinedTerm/llm-as-a-judge]]
