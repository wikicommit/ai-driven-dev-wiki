---
title: "Methodological Harness"
type: "schema:DefinedTerm"
lang: en
tags: [spec-driven-development, agentic-software-engineering, human-agent-collaboration]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.00252'
    hash: sha256:5331d1eb219124b67deabb6640416e4b3ac07d3f4ede62ff19407f403d7d576d
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The team-level counterpart of an agent's technical harness, as proposed by Díaz et al.: the practices and artifacts a team owns — centred on specifications — through which it governs agent behaviour across sessions, agents and people, as opposed to the software around the model that governs one agent in one session."
---

The methodological harness is a construct proposed in
[[ScholarlyArticle/spec-driven-development-for-agentic-software-engineering]] for the set of team-owned
practices and artifacts through which a software team governs the behaviour of coding agents. That paper
distinguishes it from the technical harness — the software around a model (orchestration loop, tools,
context management, memory, guardrails and verification loops) that governs one agent in one session —
and argues that the team-level properties this cannot supply on its own, namely reproducibility,
auditability, transferability, review capacity and coordination, need a second harness whose central
artifact is the specification.

## Usage

The paper organizes the methodological harness into eight mechanisms grouped under three functions —
knowledge, production and governance — and states for each the commitment a team takes on:

- **Context engineering**: the information environment agents work in is built and maintained as a
  shared, versioned team asset rather than as private per-developer configuration.
- **Persistent shared knowledge**: a store of decisions, rationale, session summaries and discoveries is
  read at the start of every agent session and written at its end, holding summaries and decisions rather
  than raw transcripts, retrieved selectively, and neutral to which agent or tool reads it.
- **Executable specifications**: specifications are written to be consumed by agents and validated by
  automated checks — testable acceptance criteria, checkable constraints and explicit decisions.
- **The N-version mindset and parallel agents**: dispatching one specification to several agents and
  comparing the candidates is treated as a normal mode of work, with each agent isolated in its own
  [[DefinedTerm/git-worktrees]] working tree.
- **Normative specifications**: the team's standing conventions and prohibitions are written into the
  always-loaded system specification rather than left tacit, and added by reviewed pull request.
- **Structured consultation**: the agent suspends on a decision it cannot or should not resolve and
  raises a scoped request citing the specification clause at issue, with the answer recorded against that
  specification.
- **Evidence-backed acceptance**: the unit of completion is an evidence bundle showing conformance to the
  specification rather than a merged pull request.
- **Graduated autonomy**: the autonomy granted to agents is calibrated per class of task as an explicit,
  versioned and revisable team decision.

The paper presents these as mutually reinforcing rather than independent, with persistent shared
knowledge described as the mechanism that closes the loop by letting the products of the others survive
to the next session, agent and teammate. It also argues that one artifact, the rule file an agent loads
at the start of every session, serves at once as the system specification, as feedforward guidance to
the agent and as the carrier of the team's norms.

## When It Applies

The construct is argued to matter once agents are delegated goal-level work at team scale, where
individual gains otherwise run into review, verification and coordination bottlenecks. It assumes the
team has committed to specifications as the authoritative contract between humans and agents, since each
mechanism is defined relative to one. Its central claim is an asymmetry in durability: the technical
harness is described as transient, depreciating as models improve and as capabilities become native to
them, whereas the methodological harness encodes the team's intent, norms and accumulated decisions and
so appreciates over time — from which the authors conclude that teams should invest preferentially in the
methodological harness and treat tool selection as secondary. The paper warns that adopting it in
fragments, for example writing feature specifications without encoding norms or persisting decisions,
yields a fraction of the benefit while paying most of the discipline cost, and lists specification drift
and cost growth among its risks.

It is one research group's proposal, derived from a multivocal literature review that relies largely on
gray literature, and the authors state that several of the individual mechanisms had appeared separately
in practitioner writing, with their contribution being to organize them around specifications. They
describe the framework as falsifiable hypotheses rather than a validated model, and its predicted
benefits as untested.

## Related Terms

[[DefinedTerm/agent-harness]], [[DefinedTerm/harness-engineering]], [[DefinedTerm/spec-driven-development]],
[[DefinedTerm/context-engineering]], [[DefinedTerm/consultation-request-pack]],
[[DefinedTerm/merge-readiness-pack]]
