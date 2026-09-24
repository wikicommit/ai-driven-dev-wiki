---
title: "Mise en Place (Agentic Coding Methodology)"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, context-engineering, spec-driven-development, multi-agent]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.05400'
    hash: sha256:1f126c8e3d5e00a7ac0db71cd27186c357be2d109f14c9979f133b56b18b3303
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A preparation-first methodology for agentic coding proposed by Andrew Zigler, named after the culinary practice of putting everything in its place before cooking: contextual grounding, collaborative specification and task decomposition are all completed before agents begin implementation."
---

Mise en place (MEP), as proposed in [[ScholarlyArticle/mise-en-place-for-agentic-coding]], is a
structured preparation methodology for agentic coding that borrows the French culinary term for
"everything in its place". Its premise, in the author's words, is that the alignment problem in
agentic coding is fundamentally a preparation problem: when domain expertise, design intent and task
boundaries are externalized into structured artifacts before agents begin writing code, the resulting
implementation is argued to be more aligned, more coherent and less costly to verify. MEP formalizes
that preparation into three sequential, phase-gated steps — contextual grounding, collaborative
specification and task decomposition — each producing artifacts that feed the next, all completed
before implementation begins, after which parallel agents execute the decomposed work and their
outputs converge in integration verification.

## Usage

In **contextual grounding**, the practitioner externalizes domain expertise and tacit knowledge into
briefing documents — markdown files encoding domain knowledge, competitive analysis and design
philosophy — that form a persistent context layer agents consult throughout implementation; following
backward design, this starts from outcomes rather than features. In **collaborative specification**,
structured human-agent dialogue (the practitioner describes intent, the agent proposes details, the
practitioner accepts, rejects or modifies) produces a design document; its key mechanism is encoding
value judgments as specification constraints, including what to exclude, and recording the why as
well as the what so that agents can make aligned micro-decisions without escalating. In **task
decomposition**, the specification becomes dependency-aware task records with priorities and
acceptance criteria — the author used [[DefinedTerm/beads]] — so that multiple agents can work
simultaneously; the coordination burden shifts from runtime to preparation time.

The paper positions MEP relative to [[DefinedTerm/spec-driven-development]], which it extends with a
phase for tacit, value-laden knowledge, and to [[DefinedTerm/prompt-engineering]], from which it
differs in scope: prompt engineering tunes individual model invocations, whereas MEP structures the
workflow-level artifacts that precede and constrain them. It presents MEP as the opposite end of the
spectrum from [[DefinedTerm/vibe-coding]], front-loading alignment work that iterative flows pay
incrementally as rework.

## When It Applies

The author argues that agentic workflows need this kind of preparation because agents lack the tacit
context human collaborators carry and cannot iterate cheaply without expensive regeneration. MEP
assumes a practitioner able to articulate the relevant domain knowledge and to decompose work into
independently executable units with explicit dependencies, and it is aimed at setups where several
agents implement in parallel. The paper does not name misapplication modes; among its open questions
are what counts as "sufficient" context and when preparation should stop, and whether the method
scales from prototyping to multi-month development.

Its evidential basis is thin by the author's own account: a single five-hour hackathon with one
practitioner and no control group, in which about two hours of preparation preceded parallel
implementation by four agents with no structural refactoring needed afterward. The author
acknowledges that this cannot establish causation and that their own dual background in education and
software engineering confounds the result, and describes MEP as a starting framework that formalizes
practices experienced practitioners converge on independently rather than a validated method.

## Related Terms

- [[DefinedTerm/context-fluency]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/ralph-loop]]
- [[DefinedTerm/vibe-coding]]
