---
title: "AI Unified Process"
type: "schema:DefinedTerm"
lang: en
tags: [spec-driven-development, harness-engineering, enterprise-software, traceability]
aliases: ["AIUP"]
sources:
  - type: url
    url: 'https://ai-engineering-summit.de/blog/spec-driven-development-ki-agenten/'
    hash: sha256:53083788f1424de4a3df3ee2f9dc8a768c1b897e3ceb3c6dba73e3f29f05fc19
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A spec-driven development method developed by Simon Martinelli, inspired by the Rational Unified Process, that separates a human-readable specification (use cases and an entity model), a harness of guardrails (agent skills, MCP servers and guidelines), and the AI-generated implementation."
---

The AI Unified Process (AIUP) is a [[DefinedTerm/spec-driven-development]] method developed by Simon
Martinelli in which a specification written as use cases and an entity model is the long-lived source from
which AI agents derive code and tests. It is inspired by the Rational Unified Process but, according to its
author, keeps only that process's core idea — explicit, reviewable artifacts — rather than its whole
apparatus. Its defining feature is a split into three layers: the "what" (use cases describing observable
system behaviour in domain language, plus an entity model defining domain terms, attributes and validations),
the "how" (the implementation, whether written by hand or generated), and the "with what" — the guardrails
between intent and code, also called the harness.

## Usage

In AIUP's "with what" layer, [[DefinedTerm/agent-skills]] encode reusable project knowledge (for example how a
view or a query is written in the project), [[DefinedTerm/model-context-protocol]] servers give the AI current
documentation, examples and project references, and guidelines record rules such as naming conventions,
package structure, test strategy, permitted libraries, layer boundaries and architecture decisions. Martinelli
ties this layer to Birgitta Böckeler's application of [[DefinedTerm/harness-engineering]] to coding agents and
her distinction between guides and sensors ([[DefinedTerm/guides-and-sensors]]), making it a distinct layer
between specification and code.

The layers also redistribute roles: requirements engineers and product owners work mainly on the "what",
domain experts check that use cases describe the intended behaviour, architects own the "with what", and
developers stay in the "how" but write less code by hand, steering the AI and correcting the specification or
the guardrails when results are wrong. Tests connect the layers because they are derived from use cases and
run against the implementation; in Martinelli's example each test method carries a `@UseCase` annotation
naming the use case, scenario and business rules it covers, which yields traceability from specification to
code. Use cases, the entity model and diagrams are kept as Markdown files in the Git repository alongside the
code. Optional tooling exists in the form of the AIUP Marketplace plug-ins for Claude Code and other agents,
invoked through slash commands such as `/use-case-spec` and `/implement`, but Martinelli states that it is not
a prerequisite.

## When It Applies

Martinelli positions AIUP for long-lived business applications with many stakeholders, such as ERP systems,
where traceable requirements and maintainable specifications matter more than raw development speed, and
contrasts it with tool-led spec-driven workflows that focus on developers. It assumes that domain experts can
read and approve the use cases; if they cannot, he considers the "what" not yet ready for implementation. It
is meant to proceed iteratively, one use case at a time, rather than by writing all specifications up front,
and it uses [[DefinedTerm/domain-driven-design]] bounded contexts to keep each specification, and the AI's
context, small. In existing systems, an AI agent reconstructs use cases and the entity model from current code
and tests for one bounded context at a time, and a requirements engineer corrects them with the business side.

He names three ways it is misapplied: use cases becoming technical scripts that describe the UI (including when
an AI reconstructing use cases from existing code carries implementation details over as requirements),
specification, code and tests drifting apart after hotfixes or quick refactorings, and starting with tooling
before the method. The method rests on its author's own project experience, including his
recommendations of small teams, trunk-based work and, often, Kanban; the source reports no measured results.

## Related Terms

- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/guides-and-sensors]]
- [[DefinedTerm/domain-driven-design]]
- [[DefinedTerm/agent-skills]]
