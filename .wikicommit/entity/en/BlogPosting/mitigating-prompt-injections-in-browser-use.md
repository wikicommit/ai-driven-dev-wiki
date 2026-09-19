---
title: "Mitigating the risk of prompt injections in browser use"
type: "schema:BlogPosting"
lang: en
tags: [prompt-injection, agent-safety, security]
sources:
  - type: url
    url: 'https://www.anthropic.com/research/prompt-injection-defenses'
    hash: sha256:a0696c23a0c6a65b1581eb7fa746dbecd592b1177f016f52481cf3d09d18ab4f
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Anthropic's account of why browser use amplifies prompt injection risk and what it has done about it: reinforcement learning against injections in simulated web content, classifiers scanning untrusted content entering the context window, and continuous human red teaming. It reports a 1% attack success rate against an internal adaptive attacker and states plainly that this is not a solved problem."
  datePublished: "2025-11-24"
  publisher: "[[Organization/anthropic]]"
---

This post sets out why [[DefinedTerm/indirect-prompt-injection]] is a sharper problem for a browser
agent than for an agent generally, and what Anthropic has done to reduce it. Its framing of the risk is
that for an agent to be useful it must act on the user's behalf — browsing, completing tasks, working
with the user's own data — and that this makes every webpage it visits a potential attack vector.

Two properties are named as what amplifies the risk in a browser specifically. The attack surface is
vast: every webpage, embedded document, advertisement and dynamically loaded script is a possible
carrier of malicious instructions. And the action space is wide: a browser agent can navigate to URLs,
fill forms, click buttons and download files, all of which an attacker can turn to their purpose once
they have influence over its behaviour.

The post reports measured progress and refuses to present it as resolution. Its own summary of the
number is that a 1% attack success rate, while a significant improvement, still represents meaningful
risk — and that the findings are shared to demonstrate progress rather than to claim the problem solved.

## Key Points

- The worked example given is an agent asked to read recent emails and draft replies to meeting
  requests, where one email carries instructions hidden in white text — invisible to the user, processed
  by the agent — directing it to forward any email containing the word "confidential" to an external
  address before drafting the replies.
- Robustness is measured against an internal adaptive "Best-of-N" attacker that tries and combines many
  prompt injection techniques known to be effective, given 100 attempts per environment, with attack
  success rate computed as a percentage of attacks encountered by each model.
- The comparison reported is between the browser extension configuration launched with the post and the
  original research-preview launch configuration; Claude Opus 4.5 is stated to show stronger prompt
  injection robustness in browser use than previous models, with new safeguards since the preview
  improving safety across all Claude models.
- The first defence described is training: reinforcement learning is used to build robustness into the
  model itself, exposing it during training to prompt injections embedded in simulated web content and
  rewarding it for identifying and refusing malicious instructions — including instructions designed to
  appear authoritative or urgent.
- The second is classifiers. All untrusted content entering the model's context window is scanned, with
  classifiers flagging potential injections across several carriers — hidden text, manipulated images,
  deceptive UI elements — and adjusting the model's behaviour when an attack is identified. The post
  reports improving both the classifiers and the intervention that guides behaviour after detection.
- The third is human red teaming, on the stated grounds that human security researchers consistently
  outperform automated systems at discovering creative attack vectors. An internal red team probes the
  browser agent continuously, and Anthropic also takes part in external arena-style challenges that
  benchmark robustness across the industry.
- These results are given as the basis for expanding the Claude for Chrome extension from research
  preview to beta, available to users on the Max plan.
- The post states that no browser agent is immune to prompt injection, describes the web as an
  adversarial environment requiring ongoing vigilance, and commits to continued investment as attack
  techniques evolve.

## Context

The evaluation is Anthropic's own, against its own internal attacker, and the post reports the attack
success rate without publishing the benchmark, the environments, or the attack corpus — so the figure
establishes a direction of travel within one vendor's methodology rather than a comparable measure. The
post's participation in external arena-style challenges is mentioned as a complement to this, but no
external result is reported here.

What distinguishes the post from a defence-in-depth checklist is where it places the residual risk. Its
three layers are all on the provider's side — model training, classifiers in the serving path, and red
teaming — and the post's closing position is not that they suffice but that they do not. That framing
is consistent with the same company's later writing on agent trust, which extends the responsibility to
the tools, permissions and environments a customer grants an agent.
