---
title: "Specification-Driven Development: el regreso de las especificaciones en la era de los agentes de IA"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, coding-agents]
sources:
  - type: url
    url: 'https://albertoruizmb.github.io/es/blog/2026/05/21/specification-driven-development-ai-agents/'
    hash: sha256:8b89f6c7e03fa122633c59de96f490dd8c4df9ff78776fcd052f1a76c94a5088
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Spanish-language post arguing that AI coding agents are bringing the specification back to the centre of development through Specification-Driven Development, as a persistent, reviewable statement of intent shared by people and agents, and urging a measured adoption with human oversight."
  author: ["Alberto Ruiz"]
  datePublished: "2026-05-21"
---

In this post ("Specification-Driven Development: the return of specifications in the age of AI agents"), Alberto Ruiz argues that AI-assisted development is forcing a second look at an idea that had seemed to lose prominence: the specification. As agents take on broader tasks — analysing, planning, modifying, validating and coordinating changes — the problem, he writes, is no longer only productivity but how to express intent clearly, persistently and verifiably enough for both people and automated systems to understand it. [[DefinedTerm/spec-driven-development]] (SDD) is his answer to that problem.

The post defines SDD not as writing more documentation but as changing where development starts: before a tool or agent is asked to implement anything, what is to be built, why, under which constraints and with which validation criteria is defined in structured form. It then surveys a tool ecosystem it considers still open, and ends by recommending that SDD be adopted with judgement, as an engineering practice rather than a promise of total automation.

## Key Points

- It contrasts SDD with a traditional model in which code quickly becomes the main source of truth and the initial specification is soon subordinated to it; in SDD the specification tries to stay alive at least for the life cycle of the change being developed, and in the most ambitious models may serve as a permanent reference for how a feature or system evolves.
- Citing an article by Birgitta Böckeler on Martin Fowler's site, it describes the specification as written before the code and acting as a shared source of truth between the person and the AI, which it says separates SDD from informal work built on successive prompts or ephemeral conversations with an assistant.
- It argues that the isolated prompt scales badly: it can work for a quick test or a small utility but hits limits as software grows, decisions accumulate and more team members are involved, and it locates the problem in a lack of persistent context rather than only in model quality.
- It presents the specification as more than a functional description — as a coordination interface between human intent and automated execution, and a source of structured context that lives in the project rather than in what an agent remembers from one session.
- It notes that, in Böckeler's analysis of [[SoftwareApplication/kiro]], [[SoftwareApplication/github-spec-kit]] and [[SoftwareApplication/tessl]], approaches differ in ambition: the specification may appear at the start of the work, stay as an anchor as the change evolves, or aim to become the main source from which code is derived.
- It describes [[SoftwareApplication/openspec]] as a lightweight way to add a specification layer to projects that work with AI assistants or agents, keeping requirements out of the chat history, and Spec Kit as more oriented toward operationalising SDD in coding-agent workflows, organised around artifacts such as specifications, plans and tasks.
- It argues that reducing SDD to automatic code generation misses its main value, which appears when the specification shapes the whole life cycle of a change — analysis, design, planning, implementation, review, testing and later evolution — and preserves traceability between need, decision and implementation.
- It holds that SDD does not eliminate engineering but makes it more important: the more capable agents become, the more it matters to define the problem well, bound the scope, state constraints and critically review results.

## Context

The post is the author's own argument and leans on Böckeler's analysis for its account of the tool landscape. It stresses that SDD is not yet a closed standard, that there is no single universal way to apply it, and that current tools are evolving fast at different levels of maturity. It recommends bounding use cases, defining how specifications are written and reviewed, integrating SDD with existing workflows and keeping technical oversight of relevant decisions, placing SDD's value in the space between improvised prompts and traditional documentation.
