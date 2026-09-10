---
title: "First Principles Framework"
type: "schema:DefinedTerm"
lang: en
aliases: ["FPF"]
tags: [agents, llm, decision-making]
sources:
  - type: url
    url: https://github.com/NeoLabHQ/context-engineering-kit
    hash: sha256:3a00d5fa6029f48343ba32101feda4acd0f31870b7ff74ef954be99d4e04a584
    license: GPL-3.0
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "A methodology by Anatoly Levenchuk for rigorous, auditable reasoning, in which competing hypotheses are generated, checked logically, tested against evidence, and left for a human to decide between, leaving an audit trail from hypothesis to decision."
---

The First Principles Framework is a methodology for rigorous, auditable reasoning, which
[[SoftwareApplication/context-engineering-kit]] identifies as Anatoly Levenchuk's. Rather than letting a reasoner move to a
solution, it requires generating competing hypotheses, checking them logically, testing them against
evidence, and then leaving the choice to a person. Applied to an AI agent, the point of the
constraint is what it leaves behind: the kit describes its effect as turning the black box of an
agent's reasoning into a transparent, evidence-backed audit trail.

## Usage
The core cycle runs three modes of inference in order — abduction, generating competing hypotheses
so that the first idea is not anchored on; deduction, verifying each against logic and constraints;
and induction, gathering evidence through tests or research to see whether it holds in reality. The
cycle closes with an audit for bias, a decision, and a durable record of the rationale.

Four principles govern how that cycle is run: reasoning is transparent, with a full audit trail from
hypothesis to decision; it is hypothesis-driven, generating three to five competing alternatives
before any is evaluated; it is evidence-based, with trust scores computed rather than estimated; and
it keeps a human in the loop, the AI generating options and the human deciding — a division the
framework calls the Transformer Mandate. In the kit's implementation the cycle is run as a workflow
that initialises a working directory, generates hypotheses, invites the user to add their own,
then verifies, validates and scores them in parallel before presenting the comparison for a decision.

## When It Applies
The framework suits decisions whose rationale has to survive scrutiny later — where being able to
show what was considered and rejected matters as much as the answer. It assumes there are genuinely
competing alternatives to generate, and that a person is available and willing to make the final
call; the Transformer Mandate is not an optional step, so the framework has nothing to offer a fully
autonomous loop.

Its cost is unusual enough that the kit warns about it directly: the core specification is large,
which is why the plugin loads it into a sub-agent on a long-context model, and the kit cautions that
such an agent can consume a token limit quickly. As for standing, this is one author's published
methodology rather than a consensus practice, and the kit is a packaging of it — the source
describes how the framework is applied, not an independent assessment of whether it works.

## Related Terms
- [[DefinedTerm/llm-as-a-judge]] — a different answer to the same problem of not trusting a model's
  first output, evaluating a result rather than structuring the reasoning that produced it
