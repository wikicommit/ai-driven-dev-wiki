---
title: "Domain-Driven Design"
type: "schema:DefinedTerm"
lang: en
aliases: ["DDD"]
tags: [software-design, spec-driven-development, team-organization]
sources:
  - type: url
    url: 'https://blog.octo.com/organiser-une-equipe-de-developpement-a-l''ere-de-l''ia-part-ii.2'
    hash: sha256:b7d9c3f04b780f1bc180222edb9e7de30615d0f444f9f8ecff35d2b389d4377c
  - type: url
    url: 'https://blog.octo.com/organiser-une-equipe-de-developpement-a-l''ere-de-l''ia-partie-iii'
    hash: sha256:e22c6ff5cc8796eeca599798cb9ffe523e8ab45671155c15e5710a9f86016472
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An approach that structures a business domain by identifying its concepts, its ubiquitous language and the responsibilities that organize the system. In writing on AI-driven development it is presented as the source of the structural context that agents need to reason about a business."
---

Domain-Driven Design (DDD) is an approach that structures a business domain by identifying its
concepts, its ubiquitous language and the responsibilities that organize the system — describing the
concepts, their responsibilities, relationships, boundaries and invariants, and the architecture that
holds them together. It distinguishes core, supporting and generic subdomains, and work on it is
carried by the team in charge of a bounded context.

## Usage

[[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-ii-2]] frames DDD as the answer to
the question "what does the business represent?", and pairs it with
[[DefinedTerm/behavior-driven-development]], which answers "how does the business behave?". On that
post's account DDD provides the structural context and BDD the behavioural one, and together they
produce an explicit representation of the business that AI agents can understand and use — agents, unlike
an experienced developer, having neither business intuition nor tacit knowledge. The resulting model,
behaviours, architecture decisions and quality requirements are then gathered into a living specification
through [[DefinedTerm/spec-driven-development]].

The same post uses DDD's subdomain classification to decide how much autonomy to give agents. The Core
Domain, where the company's competitive advantage lies, justifies significant investment in DDD, BDD and
SDD and careful review of agent-generated code; there, SDD combines with tactical DDD's Deep Modeling and
Supple Design, refining the model through iterative exploration of the business. Supporting Domains may
benefit when their complexity justifies it, while Generic Domains, whose rules are largely standardised,
lend themselves to more automation or to adopting existing solutions.

[[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-iii]] turns to strategic DDD to
organize teams rather than code. It describes strategic DDD as a frame in which a diverse audience —
business experts, product managers, UX designers, developers, architects — builds a shared understanding
of the domain and identifies the boundaries within which concepts, rules and behaviours form a coherent
whole: a domain splits into subdomains, and each bounded context has its own business model, ubiquitous
language and clearly delimited responsibilities. Those business boundaries are then used to organize
teams around coherent, sufficiently autonomous perimeters whose life cycle they can master end to end,
in line with Conway's law, so that business, software and organizational boundaries are aligned. That
post adds that bounded contexts guide team responsibilities without imposing a one-to-one mapping: one
team may take several bounded contexts when their complexity and cognitive load remain manageable, while
the most complex or strategic domains may justify a team focused on a narrower perimeter. It pairs
strategic DDD with Team Topologies, which sizes teams by the cognitive load they can absorb, and in its
proposed [[DefinedTerm/augmented-sdlc]] places DDD at the centre of the Design moment, where knowledge
from EventStorming workshops is turned into aggregates, domain events, business services, policies and
ubiquitous language.

## When It Applies

- **Conditions.** The part II.2 post concentrates the investment on the Core Domain; the part III post
  applies strategic DDD at the level of the teams that own a business perimeter.
- **Assumptions.** It assumes that business experts and the team work together in workshops to build the
  shared model, and that the model is then kept explicit enough for agents to use.
- **Failure modes.** The post warns that the DDD/BDD/SDD combination is no silver bullet and can be
  misapplied — through over- or under-specification, duplicated knowledge, specifications that stop
  evolving, or specifications that describe the solution instead of the need.
- **Establishment.** The part III post lists DDD among the approaches that have enriched software
  engineering over the last thirty years. Its framing as the structural layer of an agent's context, and
  as the basis for sizing teams working with agents, is the argued position of both posts, which come
  from the same series, rather than a measured result.

## Related Terms

- [[DefinedTerm/behavior-driven-development]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/example-mapping]]
- [[DefinedTerm/augmented-sdlc]]
