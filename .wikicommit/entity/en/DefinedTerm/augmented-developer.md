---
title: "Augmented developer"
type: "schema:DefinedTerm"
lang: en
aliases: ["Développeur augmenté"]
tags: [coding-agents, team-organization]
sources:
  - type: url
    url: 'https://blog.octo.com/le-developpement-logiciel-a-l''ere-des-agents-ia'
    hash: sha256:5f3659e3312d232fa458c15b3683f0b90d22b6de8edc980b38fc9be979fbd6a5
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A developer whose value lies in understanding the business domain and steering several AI agents in parallel, rather than in writing code by hand. The term is used in a January 2026 blog post that presents a pair of such developers as the basic unit of a development team."
---

An augmented developer (*développeur augmenté*), as the term is used in
[[BlogPosting/software-development-in-the-age-of-ai-agents]], is a developer who delegates several
tasks at once to different AI agents — feature generation, test writing, exploring technical options,
preparing migrations, analysing architecture — and whose role is to orchestrate that production rather
than to type code. The post describes this developer as a "conductor" who steers, coordinates and guides
specialised agents, and locates their value in understanding the business domain, structuring the work,
guiding production and keeping increasingly complex systems coherent.

## Usage

In that post the augmented developer works from explicit artefacts — generally Markdown files — that
state the application's target architecture, testing and mocking strategies, code-generation
conventions and known business rules, and from an explicit execution plan that says which agent does
what, where, and in what order. Waiting time during generation is turned into extra production capacity
by running work in parallel, and the flow of parallel work is managed with Kanban-style tools that limit
work in progress. The post sets the role in a team context: established companies are advised to slow
recruitment in favour of profiles able to take on this role and to train their most business-autonomous
developers, and the pair of augmented developers is presented as the minimal viable unit. The key profile
it names is a senior developer with strong business maturity, at the crossroads of Tech Lead and Product
Owner.

## When It Applies

- **Conditions.** The post frames the role for organizations adopting generative-AI coding agents, and
  ties its productivity to a strong understanding of the business domain.
- **Assumptions.** It assumes clear, contextualised business requirements illustrated with concrete
  examples; the post argues that poorly qualified user stories become the limiting factor once agents
  take over execution. It also assumes a fully automated CI/CD chain able to absorb the faster pace.
- **Failure modes.** Entrusting orchestration to a single developer is described as a dangerous
  illusion because of the bus factor, which is why the post insists on pairs. It also notes that the
  model suits developers who have already been through an intensive period of hands-on coding, and that
  junior developers need a redesigned path — pair programming with a senior, adjusting generated code,
  and deliberate practice such as code katas — to build the technical grounding the role presupposes.
- **Establishment.** The term and its framing come from a single practitioner's blog post; its claims,
  including that a business-aligned pair can deliver in a day what a team of five previously took months
  to produce, are asserted without supporting measurements.

## Related Terms

- [[DefinedTerm/example-mapping]] — a practice the post names as supplying the raw material for prompts
