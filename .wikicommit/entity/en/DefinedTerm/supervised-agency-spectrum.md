---
title: "Supervised Agency Spectrum"
type: "schema:DefinedTerm"
lang: en
tags: [agents, governance, autonomy-levels]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.28791'
    hash: sha256:0de559cacdfe9078d48a08a5f2b05d76219a579abd307e3a72ca17d1894464d0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A framing of agent autonomy as a graduated spectrum rather than a binary — assist, shadow, human-in-the-loop gate, bounded, full — along which human authority falls, agent initiative rises, and the governance burden grows."
---

The supervised agency spectrum is the framing
[[ScholarlyArticle/from-determinism-to-delegation]] uses to make the point that autonomy is not binary.
It places five positions on one axis — assist, shadow, human-in-the-loop gate, bounded, and full — and
notes three quantities that move together along it: human authority falls, agent initiative rises, and
the governance burden grows.

The paper's practical observation about where systems actually sit is that most enterprise deployments
in regulated domains operate to the left of "bounded", reserving destructive actions behind
human-in-the-loop gates.

## Usage

The paper describes deployment as progressing through graduated trust rather than being switched on:
**shadow mode**, where the agent proposes and a human disposes; **human-in-the-loop checkpoints** for
consequential actions; and **bounded autonomy** within scoped permissions. Its diagram of the canonical
agentic loop places the HITL gate as the thing mediating consequential or irreversible actions before
they reach the environment, with a blocked action routed back for revision.

It grounds the framing in the CMU SEI human-centred pillar, which holds that AI systems are
socio-technical artifacts that must align with human needs and establish explicit boundaries where
decision authority remains with human operators, particularly in high-stakes domains.

The paper also describes the collaboration as bidirectional rather than as pure supervision: agents act
as first-pass implementers across planning, implementation, testing, review, documentation and
operational triage, compressing coordination cycles, while humans retain architecture, product intent
and final quality judgment. The deeper gain it names, where it materialises, is cognitive leverage —
fewer handoffs and less rediscovery of system knowledge.

## When It Applies

The spectrum applies wherever the question is not whether to delegate but how far, which the paper
treats as the normal case. Its own evidence gives two reasons to place any given deployment
deliberately rather than by default.

The first is that benefit is heterogeneous. The paper sets a lab experiment reporting 55.8% faster
completion and three field experiments reporting 26.1% more completed tasks against a randomized
controlled trial of 16 experienced open-source developers on their own mature repositories that found a
19% *increase* in completion time — and reads this as gains concentrating on well-scoped tasks and
lower-context cohorts while high-context expert work can incur net costs.

The second is [[DefinedTerm/compositional-reliability]]: because an agent's end-to-end success decays
multiplicatively across dependent steps, human checkpoints placed along a long task are what make
autonomy usable at all, rather than a concession to caution.

The failure mode the spectrum is arranged against is the one the paper treats throughout: that an
agentic system may do the wrong thing even when its code is syntactically correct, because it
misinterprets intent, selects the wrong tool, loses context, or acts with excessive autonomy — and that
the risk is amplified by agency itself, since under indirect prompt injection a poisoned document can
induce an agent to misuse a legitimate tool.

As a scheme it is one paper's presentation, given as a figure and a paragraph rather than derived from
a survey of deployments, and its positions are not defined with operational thresholds. The paper is a
position paper that says so, and treats its forward-looking claims as falsifiable hypotheses; the
"most enterprise deployments" observation is stated without a supporting measurement.

## Related Terms

- [[ScholarlyArticle/from-determinism-to-delegation]] — the paper this framing comes from
- [[DefinedTerm/human-in-the-loop]] — the gate this spectrum places in the middle of its range
- [[DefinedTerm/agentic-autonomy-levels]] — a separate scheme over similar ground
- [[DefinedTerm/se-autonomy-levels]] — another such scheme
- [[DefinedTerm/compositional-reliability]] — the structural reason checkpoints are load-bearing
- [[DefinedTerm/indirect-prompt-injection]] — the attack class that makes unsupervised tool access risky
