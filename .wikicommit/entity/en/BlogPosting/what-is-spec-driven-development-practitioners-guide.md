---
title: "What Is Spec-Driven Development? A Practitioner's Guide (and When to Skip It)"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, agentic-coding]
sources:
  - type: url
    url: 'https://felipefontoura.com/articles/what-is-spec-driven-development'
    hash: sha256:df2dca52352dcf718f101f98063eb1e945bc10156a4d147c303ee689675185ea
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A practitioner's guide that defines spec-driven development as approving a structured specification before any code is generated, presents the specification as the external memory an AI agent lacks, and sets out a four-phase gated workflow, the EARS requirements format and the cases where a spec is not worth writing."
  author: ["Felipe Fontoura"]
  datePublished: "2026-05-12"
---

A guide to [[DefinedTerm/spec-driven-development]] published on Felipe Fontoura's personal site on
May 12, 2026. The author, who describes himself as having shipped production code for 25 years,
presents it as the method he used in late 2025 to build a crypto fintech of 13 apps, 3 APIs and 3
databases, running on Kubernetes, in 70 days and working alone with AI agents; the detailed numbers
are left to a separate case-study article, and this piece is the method.

Its central argument is that the problem spec-driven development solves is memory, not intelligence.
An AI agent, on the author's account, is extraordinarily capable but has no persistent memory between
sessions, so anything not written down is reinvented on the next run and not the same way twice; the
specification is the external memory that carries a project's decisions forward. From that follow a
workflow of four gated phases, a worked specification, a set of writing techniques, and an explicit
account of when the method is not worth using.

## Key Points

- Spec-driven development is defined as writing and approving a structured specification —
  requirements, design, acceptance criteria, constraints and edge cases — before any code is
  generated, with that specification remaining the source of truth the agent builds from; the post
  summarises the flip as the code becoming a byproduct of the spec rather than the docs a byproduct
  of the code.
- The author points to Anthropic's published Claude Code guidance, which he reports recommends
  planning before implementing and provides a dedicated plan mode, as the model maker itself
  recommending the practice.
- It separates a specification from the artefacts it is confused with: a prompt is an instruction for
  one agent turn, a PRD tells a business what to build, a design doc explains a decision to human
  reviewers, and only a specification is written to be executed by the agent and lives with the
  feature.
- The workflow has four phases — requirements (what, in business language and technology
  independent), design (how, with every requirement mapped to a decision and each technology choice
  given a reason), tasks (units of two to four hours, each independently testable), and
  implementation — with a human approval gate between each.
- In the author's own kit, the gate is a one-line per-feature `.status` file holding tokens such as
  `requirements:approved`, which the agent reads before acting; a `design.md` sitting on disk does
  not count as approval, only the status token does. This is the author's own tooling, not a general
  convention.
- The post's worked example is a specification for creating a payment charge in which a retry must
  never double-bill: it lists in- and out-of-scope items, writes functional requirements in EARS,
  gives concrete acceptance examples, pins money to integer cents, enforces exactly-once billing with
  a database uniqueness constraint, and ends by telling the agent to restate the requirements before
  writing code.
- It recommends writing functional requirements in [[DefinedTerm/easy-approach-to-requirements-syntax]],
  calling it the highest-leverage technique almost no guide teaches, and stating negative scope
  explicitly as the best defence against an agent building something nobody asked for.
- It presents three levels of rigor — spec-first, spec-anchored and spec-as-source — which it
  attributes to Birgitta Böckeler's work at Thoughtworks; the author reports running spec-first for
  MVP features and spec-anchored for anything touching money, and calls spec-as-source still a
  research bet.
- It places the practice on a line after TDD and BDD, calling TDD spec-driven development at the unit
  level, and contrasts where each method keeps its truth: vibe coding in the last prompt, TDD in unit
  tests, BDD in behaviour examples, and spec-driven development in the approved specification.
- It argues that a very large context window does not make a specification unnecessary, because
  context length and context precision are different problems: a whole codebase in context tells the
  agent what the system currently is, not what it should become.
- It says a specification is not worth writing for one-off scripts, throwaway prototypes or
  exploratory spikes, and is worth it when the work outlives a single sitting, spans multiple
  sessions, or involves real architecture and correctness requirements.
- It rejects the charge that this is waterfall — whose problem it identifies as frozen, long-loop
  planning — because its specifications are living documents revised per phase, while warning,
  again citing Böckeler, that the failure modes that ended model-driven development in the 2000s
  remain risks.

## Context

The post is one practitioner's method, written on his own site and backed by his own project rather
than by an independent evaluation; its headline figures come from that single solo build, which it
credits to the specifications rather than to the AI. It cites a randomized controlled trial in which,
by the author's account, experienced open-source developers were slower with AI assistance while
believing it had sped them up, as evidence that a more capable model carries a vague instruction
further in the wrong direction. It also names [[SoftwareApplication/github-spec-kit]], AWS [[SoftwareApplication/kiro]] and the author's own
pi-sdd-kit as toolkits that codify the workflow, while holding that the method needs no tool beyond
Markdown files and a capable coding agent.
