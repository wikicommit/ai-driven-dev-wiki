---
title: "Organiser une équipe de développement à l’ère de l’IA - Part II.2"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, coding-agents, team-organization]
sources:
  - type: url
    url: 'https://blog.octo.com/organiser-une-equipe-de-developpement-a-l''ere-de-l''ia-part-ii.2'
    hash: sha256:b7d9c3f04b780f1bc180222edb9e7de30615d0f444f9f8ecff35d2b389d4377c
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The second half of part II of a French-language series on blog.octo.com about organizing a development team in the age of AI, dated 30 July 2026. It argues that Domain-Driven Design, Behavior-Driven Development and Spec-Driven Development form one chain that turns business knowledge into a living specification usable by both teams and AI agents."
  author: ["Bruno Boucard"]
  datePublished: "2026-07-30"
---

This post continues part II of a series on organizing a development team in the age of AI. The
series' premise, restated at the start, is that with AI value shifts from code to knowledge and the
quality of decisions; this instalment sets out concretely how to build and structure that body of
knowledge (*patrimoine de connaissances*) so that it is as explicit as possible for teams and agents
alike.

Its argument runs through three practices treated as successive stages.
[[DefinedTerm/domain-driven-design]] answers "what does the business represent?" and supplies the
structural context; [[DefinedTerm/behavior-driven-development]] answers "how does the business
behave?" and supplies the behavioural context; and [[DefinedTerm/spec-driven-development]] gathers both
into a living, coherent, versioned specification that becomes the project's source of truth. Because
agents do not take part in discovery workshops, ask no questions and have no tacit business knowledge,
the post argues that anything left implicit becomes a potential source of error — which is what gives
these practices a new role.

The post then draws organizational conclusions: agentic teams are presented as a consequence of value
shifting towards knowledge rather than as its cause, and the investment in DDD, BDD and SDD — and the
autonomy given to agents — is scaled to the kind of subdomain being worked on.

## Key Points

- With agents, BDD gains a new purpose: besides aligning business experts, product managers,
  developers and testers, it gives agents an explicit description of how the system should behave.
- [[DefinedTerm/example-mapping]] workshops turn conversations into behavioural knowledge — rules,
  examples, counter-examples, edge cases and open questions — which is then formalised as Gherkin
  scenarios that act as an instruction language for agents.
- The post presents the BRIEF principles for scenarios (Business language, Real data, Intention
  revealing, Essential, Focused) as a way to make that knowledge precise and directly usable by agents.
- The invariants carried by an aggregate are broken down into user stories and then specified through
  BDD scenarios describing the expected behaviour.
- In SDD the specification replaces the prompt as the starting point: code becomes the consequence of
  explicitly structured knowledge rather than the reference. The post names Kiro (AWS), GitHub Spec Kit
  and Tessl as initiatives putting this into practice.
- It describes [[SoftwareApplication/github-spec-kit]] as open source from GitHub, keeping
  specifications, plans, tasks and architecture decisions as Markdown files versioned in Git, with a
  workflow built on three commands once the project is initialised: `/specify` (the what and why),
  `/plan` (an implementation plan consistent with the chosen architecture) and `/tasks` (a breakdown
  into actionable tasks).
- An agent enriched with the project's context can act as a facilitation assistant in workshops,
  answering open questions from Example Mapping or the hot spots from EventStorming by recalling
  existing rules, detecting inconsistencies or suggesting lines of investigation — without replacing the
  participants' decisions.
- SDD does not mean all code is generated: the Core Domain justifies heavy investment in DDD, BDD and
  SDD with careful review of agent-generated code, Supporting Domains may benefit when their complexity
  warrants it, and Generic Domains lend themselves to far more automation or to existing solutions.
- The post gives an indicative team shape per subdomain: four seniors for a core subdomain, two seniors
  and a junior for a supporting one, and one senior and a junior for a generic one.
- It lists ways the DDD/BDD/SDD trio can be misapplied: over-specification, under-specification,
  duplicating knowledge instead of keeping a single source of truth, specifications that stop evolving
  with the software, and specifications that describe a solution instead of the need.
- Adopting agentic AI is presented as requiring committed governance and progressive support, since it
  changes work organization, collaboration and skills.

## Context

This is one instalment of a series, and it refers back to a first half of part II; it is written as the
author's argued position and reports no measurements. Related posts in this wiki:
[[BlogPosting/software-development-in-the-age-of-ai-agents]] and
[[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-iii]].
