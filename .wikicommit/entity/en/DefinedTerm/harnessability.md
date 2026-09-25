---
title: "Harnessability"
type: "schema:DefinedTerm"
lang: en
tags: [harness-engineering, coding-agents]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html'
    hash: sha256:cf7369071f56e7b3b36f7b003d612f4aa69fef17a7135ba19f2e22f2ad7e1cc6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The degree to which a codebase is amenable to being harnessed for a coding agent — whether properties such as strong typing, clear module boundaries or abstracting frameworks make guides and sensors available to build."
---

Harnessability is the degree to which a codebase is amenable to harnessing for a coding agent, a term
used in [[BlogPosting/harness-engineering-for-coding-agent-users]]. The article's point is that the
controls of a harness depend on properties of the codebase itself: a codebase in a strongly typed
language naturally has type checking as a sensor, clearly definable module boundaries afford
architectural constraint rules, and frameworks such as Spring abstract away details the agent does
not have to worry about, implicitly increasing its chances of success. Without such properties, the
corresponding controls are not available to build.

## Usage

The article connects the idea to a term its author attributes to her colleague Ned Letcher, **ambient
affordances**: "structural properties of the environment itself that make it legible, navigable, and
tractable to agents operating within it." It also notes that harnessability and complexity vary across
what a harness regulates — maintainability, architecture fitness or behaviour.

Harnessability plays out differently for greenfield and legacy systems. Greenfield teams can build it
in from the start, since technology and architecture choices determine how governable the codebase
will be. Legacy teams, especially with applications carrying a lot of technical debt, face the harder
problem that, in the article's words, "the harness is most needed where it is hardest to build."

## Related Terms

- [[DefinedTerm/guides-and-sensors]]
- [[DefinedTerm/harness-templates]]
- [[DefinedTerm/harness-engineering]]
