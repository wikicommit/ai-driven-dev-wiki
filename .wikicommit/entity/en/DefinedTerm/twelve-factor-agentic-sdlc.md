---
title: "Twelve-Factor Agentic SDLC"
type: "schema:DefinedTerm"
lang: en
aliases: ["Agentic SDLC 12 Factors", "12-Factor Agentic SDLC"]
tags: [agentic-engineering, sdlc, methodology, spec-driven-development]
sources:
  - type: url
    url: 'https://github.com/tikalk/agentic-sdlc-12-factors'
    hash: sha256:888e9d2521e7757a502ad5480f485f5e6b06b50fe2ad9235ca3f8ee817406c55
  - type: url
    url: 'https://github.com/tikalk/adlc-team-skills'
    hash: sha256:cd465f376e830cc0d6e662bd36e98e3a04d558a78ce98fb40457fc5d8b387e19
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A methodology, published in the tikalk/agentic-sdlc-12-factors repository, for building software with AI coding agents as integral participants throughout the software development lifecycle, stated as twelve factors covering mindset, context, specification and planning, execution, review, testing, traceability, tooling, directives and team capability."
---

The Twelve-Factor Agentic SDLC is a methodology for building software with AI coding agents as integral
participants throughout the software development lifecycle. Its repository describes it as a framework
that optimizes the development process for AI-assisted software development, emphasizing
maintainability, scalability and effective human-AI collaboration, and says it synthesizes best
practices extracted from the real-world experience of teams adopting and scaling AI-assisted
development. Its intended readers are developers building applications with AI assistance, operations
engineers, development teams adopting agentic practices, and technical leaders guiding AI
transformation. The text is published under the Creative Commons Attribution-ShareAlike 4.0 license,
with a separate website version.

## Usage

The repository states the twelve factors as follows:

1. **Strategic Mindset** — treat AI as a fast, knowledgeable junior partner that needs clear direction,
   mentorship and rigorous review.
2. **Context Scaffolding** — manage all context (code, documentation, team standards) with the rigor of
   a critical software library.
3. **Mission Definition** — begin every task with a Mission Brief in the issue tracker to generate a
   formal, version-controlled specification (`spec.md`).
4. **Structured Planning** — use the specification to generate an AI-assisted implementation plan
   (`plan.md`) that the developer reviews, refines and triages.
5. **Dual Execution Loops** — master real-time synchronous collaboration for complex problems and
   asynchronous delegation for well-defined tasks.
6. **The Great Filter** — the human developer is the ultimate arbiter of quality, filtering all AI output
   for correctness, architectural cohesion, security and taste.
7. **Adaptive Quality Gates** — continuous "micro-reviews" for synchronous work and formal
   "macro-reviews" for all asynchronous, agent-generated code.
8. **AI-Augmented, Risk-Based Testing** — the developer defines business and security risks and the AI
   generates the targeted tests that validate them.
9. **Traceability** — an automated link from the business intent in the issue tracker to the
   specification and code in the repository.
10. **Strategic Tooling** — manage specialized tools through a central gateway to control cost,
    security and model choice.
11. **Directives as Code** — treat all natural-language instructions, from reusable rules and examples
    to task specifications, as version-controlled assets.
12. **Team Capability** — build organizational muscle memory by formalizing the sharing of best
    practices and measuring performance with a versioned suite of evaluations.

The methodology is implemented in tooling from the same GitHub organization.
[[SoftwareApplication/adlc-team-skills]] states that it implements the Twelve-Factor Agentic SDLC and maps
its skills to individual factors — mission definition to its product skills, structured planning to its
architecture skills, traceability to decisions traced from product and architecture records to code, and
directives as code to its version-controlled directive lifecycles.

The two repositories do not name every factor the same way. For factors III, IV, IX and XI the names
match, but the adlc-team-skills alignment table labels factor VII "Verification-First Evals", VIII
"Ratchet Effect", X "Context Engineering" and XII "Build to Delete", where the methodology's own list
has Adaptive Quality Gates, AI-Augmented Risk-Based Testing, Strategic Tooling and Team Capability. The
sources do not say which is the later or authoritative wording.

## When It Applies

The methodology assumes a team setting in which work starts from an issue tracker, specifications are
version-controlled, and a human reviews everything an agent produces — factor VI makes the
human developer the final arbiter of quality, and factor V distinguishes work suited to synchronous
pairing from work that can be delegated asynchronously. Its standing is that of a practitioner
synthesis: the repository presents it as extracted from teams' real-world experience, and invites contributions to it.

## Related Terms

- [[DefinedTerm/spec-driven-development]] — specification-first development, which factors III and IV build on through `spec.md` and `plan.md`
- [[DefinedTerm/context-engineering]] — the name the adlc-team-skills alignment table gives factor X
- [[SoftwareApplication/agentic-sdlc-spec-kit]] — a spec-driven development command framework from the same GitHub organization, which adlc-team-skills is designed to coexist with
