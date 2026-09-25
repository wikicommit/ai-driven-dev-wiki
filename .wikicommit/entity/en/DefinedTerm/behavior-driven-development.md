---
title: "Behavior-Driven Development"
type: "schema:DefinedTerm"
lang: en
aliases: ["BDD"]
tags: [spec-driven-development, requirements]
sources:
  - type: url
    url: 'https://blog.octo.com/organiser-une-equipe-de-developpement-a-l''ere-de-l''ia-part-ii.2'
    hash: sha256:b7d9c3f04b780f1bc180222edb9e7de30615d0f444f9f8ecff35d2b389d4377c
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A development practice that puts conversation at the centre: starting from a user story, business experts, product managers, developers and testers collectively clarify business rules, special cases and acceptance criteria. With AI agents it is also presented as a way to give agents an explicit description of the system's expected behaviour."
---

Behavior-Driven Development (BDD) is a practice that brings out the behaviour of a business domain —
the rules a system applies in response to events, such as booking a place, calculating a risk or
validating a payment — by placing conversation at the heart of development. Starting from a user
story, business experts, product managers, developers and testers collectively clarify the management
rules, special cases and acceptance criteria, and the result is formalised as scenarios.

## Usage

[[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-ii-2]] sets out how the practice
changes once AI agents are involved. BDD's long-standing purpose was to build a shared understanding of
expected behaviour among the people in the conversation; that post argues it now has a further one:
giving agents an explicit description of how the system behaves. Agents do not attend discovery
workshops, ask questions, test their assumptions or compensate for ambiguity through experience — they
reason only from what is explicit in their context — so any implicit rule or undocumented exception
becomes a potential source of error.

On that account the chain runs as follows. [[DefinedTerm/example-mapping]] workshops turn conversations
into behavioural knowledge — rules, examples, counter-examples, edge cases and open questions. That
knowledge is then written as scenarios in Gherkin syntax, which the post describes as no longer only
acceptance criteria for tests but an instruction language for agents, each scenario stating initial
conditions, triggering events, expected decisions and observable results. Because an imprecise scenario
now impoverishes the agents' context and not only the acceptance tests, the post gives new weight to the
BRIEF principles for scenarios: Business language, Real data, Intention revealing, Essential and
Focused.

The same post places BDD between two other practices. [[DefinedTerm/domain-driven-design]] answers
"what does the business represent?" and provides structural context; BDD answers "how does the business
behave?" and provides behavioural context; and [[DefinedTerm/spec-driven-development]] gathers both into
a living specification. In its account, invariants carried by an aggregate are broken down into user
stories and then specified through BDD scenarios.

## When It Applies

- **Conditions.** The post recommends heavy investment in BDD, together with DDD and SDD, for a
  domain's Core Domain, where the organization's competitive advantage lies; Supporting Domains may
  benefit when their complexity justifies it, while Generic Domains lend themselves to more automation.
- **Assumptions.** It assumes that business experts and the team can meet to have the conversations the
  practice is built on, and that the resulting scenarios are kept precise.
- **Failure modes.** The post warns that an imprecise or incomplete scenario directly impoverishes the
  context agents reason from, and lists pitfalls of the DDD/BDD/SDD combination: specifications that are
  too long or too thin, knowledge duplicated across places, specifications that stop evolving, and
  specifications that describe a solution rather than the need.
- **Establishment.** BDD itself predates AI agents — the post describes its original role of aligning
  business experts, product managers, developers and testers. Its use as a language for agents is that
  post's argued position, not a measured result.

## Related Terms

- [[DefinedTerm/example-mapping]]
- [[DefinedTerm/domain-driven-design]]
- [[DefinedTerm/spec-driven-development]]
