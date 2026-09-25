---
title: "Example Mapping"
type: "schema:DefinedTerm"
lang: en
tags: [requirements, spec-driven-development]
sources:
  - type: url
    url: 'https://blog.octo.com/organiser-une-equipe-de-developpement-a-l''ere-de-l''ia-part-ii.2'
    hash: sha256:b7d9c3f04b780f1bc180222edb9e7de30615d0f444f9f8ecff35d2b389d4377c
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A workshop format used in Behavior-Driven Development that turns conversations about a user story into structured behavioural knowledge: business rules, examples, counter-examples, edge cases and open questions."
---

Example Mapping is a workshop format associated with [[DefinedTerm/behavior-driven-development]] in
which a team works through a user story by laying out its business rules together with the examples,
counter-examples and edge cases that illustrate them, and the questions that remain open. Each of these
becomes a piece of structured information that progressively reduces ambiguity about the expected
behaviour.

## Usage

[[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-ii-2]] argues that the workshop takes
on new importance with AI agents: it no longer serves only to align the team, but turns conversations
into behavioural knowledge that agents can use. In that post's chain, the output of Example Mapping is
formalised as Gherkin scenarios, which then feed a living specification in
[[DefinedTerm/spec-driven-development]]. The same post suggests that the open questions an Example
Mapping session raises can be put in real time to an agent that holds the project's context, which can
recall existing rules, detect inconsistencies, highlight impacts or suggest lines of investigation — while
the decisions remain the participants'.

## When It Applies

- **Conditions.** It applies when a user story's behaviour has to be clarified collectively before
  implementation, with business experts and the team in the room.
- **Assumptions.** It assumes the rules and examples it produces are then carried into a durable form —
  in the post's account, Gherkin scenarios and a specification — rather than left in the conversation.
- **Failure modes.** The post stresses that agents reason only from what is explicit, so rules, exceptions
  or edge cases left out of the workshop's output become potential sources of error in what the agents
  produce.
- **Establishment.** The post links to Cucumber's documentation for the practice; its claim that the
  workshop gains importance in agent-driven development is the post author's argued position.

## Related Terms

- [[DefinedTerm/behavior-driven-development]]
- [[DefinedTerm/spec-driven-development]]
