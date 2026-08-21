---
title: "Beyond Code-Centric"
type: "schema:Report"
lang: en
tags: [spec-driven-development, agentic-coding, specification, software-development-process]
sources:
  - type: url
    url: 'https://specstory.com/whitepapers/beyond-code-centric-specstory-2025.pdf'
    hash: sha256:4dc1c2f09b2ea2dff0c8bfb3cc6e5eb177c4c5134a96a0025cf03ad6841972e8
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A SpecStory whitepaper arguing that AI coding agents have moved the software bottleneck from development speed to specification clarity, and that Waterfall, Agile and GitFlow each fail in a multi-voice agent environment because all three assume human interpretation."
  author: ["[[Person/greg-ceccarelli]]"]
  publisher: "[[Organization/specstory]]"
  datePublished: "2025-06-15"
  abstract: "AI coding agents can now generate code on demand, moving the primary software bottleneck from development speed to specification clarity. Structured workflows coupled with trunk-based development unify intent, code and tests, forcing teams to make domain knowledge explicit."
---

"Beyond Code-Centric: Agents Code but the Problem of Clear Specification Remains" is a whitepaper published on 15 June 2025 by [[Person/greg-ceccarelli]], co-founder of [[Organization/specstory]]. Its thesis is that software's bottleneck has moved — "it's no longer about how fast we type but how clearly we think" — and that the established ways of organising software work were all built on an assumption agents break.

## Key Findings

The paper calls the move the **abstraction shift**: because agents can produce code on demand from high-level prompts, progress now hinges on the clarity of thought behind the specification of what should be built. It grounds this in Robert C. Martin's argument in *Clean Code* that "specifying requirements in such detail that a machine can execute them is programming. Such a specification is code" — reading Martin's point as newly literal rather than as a refutation of the shift.

The central mechanism it identifies is that humans fill gaps agents blast past. A human developer given "make it more user-friendly" books a call and asks questions; an agent given the same line invents solutions, with no middle ground. The paper argues this cannot be engineered away because it is baked into how agents execute prompts, and that the consequence lands hardest on teamwork: where a specification must carry product vision, business realities, design constraints, user limitations and technical architecture at once, any ambiguity becomes a bug, an assumption, or a blocker.

From there it argues each established paradigm fails for its own reason. **Waterfall** produces book-length documents that "choke LLMs" — lengthy, imprecise in AI terms, oriented toward a final product rather than iterative building blocks, and assuming a single authority owns the specification. **Agile**'s preference for working software over documentation keeps design intent in hallway chat, stand-ups and tacit knowledge, which the paper calls a paradox because agents "can't attend retros or read between the lines". **GitFlow**'s long-lived branches multiply the contexts an agent must reconcile: asked to implement a feature across `main`, `dev`, a feature branch and a hotfix branch, a human infers the right one from conversation and tacit knowledge while "the AI agent sees four conflicting realities with no way to reconcile them".

Its answer is trunk-based development with each role contributing specifications to one shared repository — product managers writing testable user behaviours as functional intent, designers coding constraints such as spacing, components and interactions as design intent, and architects declaring interfaces, contracts and dependencies as technical intent. The stated reason is enforcement rather than preference: "unfinished work cannot hide in branches. One branch enforces one truth." The workflow it layers on top is [[DefinedTerm/specflow]].

The paper is unusually direct about where the approach still hurts, cataloguing pain points it says redistribute rather than remove complexity — the context loading problem, model choice micro-decisions, precision overhead, intervention and versioning trade-offs, and a maintenance burden it summarises as agents generating "house of cards code" that appears complete but fails under real-world pressure. Its own conclusion from that list is a qualified one: until better intent-centric tools reduce these micro-decisions, "spec-driven development with agents remains powerful in theory but insufficient in practice".

On testing it states a rule it calls sacred, quoting Diwank Singh — "Never. Let. AI. Write. Your. Tests." — while shifting the emphasis: the paper's own position is that it is *specification* that matters, and that if AI specifies the tests then control is ceded. Its reasoning is that tests are executable specs capturing shared understanding of correct behaviour, which must reflect business rules, user needs and insights from people who know the domain.

## Context

The paper's framing throughout is that it is not proposing to replace *Clean Code*'s principles but to evolve them for a world where implementation is cheap and coordination expensive. Where Clean Code made code the primary specification, the paper proposes a three-layer stack: **declared intent** as the first-class spec reflecting product, design and architecture voices; **code** as one valid execution of that intent rather than the only source of truth; and **tests** verifying both the intent and its implementation. In its concluding section it states that "the specification is still code, just a different kind", and explicitly rejects a no-code or low-code future in favour of what it calls high-leverage code.

As a vendor whitepaper its claims about its own method are the author's own. Its reported result — three people delivering a complete end-to-end macOS alpha of SpecStory's Studio product in four weeks — is stated by the company about its own practice, with no independent verification, and the paper's account of Specflow is likewise the account of the workflow's own publisher.
