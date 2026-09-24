---
title: "Context Driven Engineering"
type: "schema:DefinedTerm"
lang: en
aliases: ["CDE", "Context-Driven Engineering"]
tags: [context-engineering, spec-driven, methodology, ai-adoption]
sources:
  - type: url
    url: 'https://eventuallycoding.com/2026/02/context-driven-engineering/'
    hash: sha256:2af38c61949d6c58913e8b63fdf818bcf71314f01f14f330e3346f3ee531f9ff
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A name used in a 2026 practitioner survey for the practice of giving an AI coding agent a complete context — the intent together with its constraints, such as coding guidelines — instead of a bare prompt, with a written specification and plan required before any code."
---

Context Driven Engineering (CDE) is a name one practitioner's survey post uses for AI-assisted software development in which the developer supplies an agent with a complete context — the intent **and** the constraints the work must respect, such as coding guidelines, tools to use and documentation to follow — rather than giving it a prompt. In the account of [[BlogPosting/impact-of-ai-on-the-state-of-the-art-in-software-engineering-in-2026]], it is presented as the term people now use in place of [[DefinedTerm/vibe-coding]], alongside [[DefinedTerm/agentic-engineering]], and its stated aim is to reduce the non-deterministic part of the process and make the quality of what is produced more reliable. Its defining consequence, in that account, is that the specification becomes a first-class citizen again and an obligation before code is written.

## Usage

The post that frames the practice under this name describes it through a three-step workflow it finds recurring across teams: **spec**, **plan**, **act**. The spec gathers the use cases and the team's intent, whether a company calls it an RFC, an ADR or a PRD, and is usually reviewed by product experts. The plan lists every step needed to implement the spec, each one achievable by an agent on its own with sufficient context, and is usually reviewed by senior engineers such as architects, staff engineers or tech leads. The act step is the implementation, carried out in agentic sessions either in a copilot mode that validates each change one by one or in an agent mode where the developer states the intent and then checks the result. Teams vary the pattern: one company described in the post breaks the work into elaborate, plan, implement, assert, review, learn and push steps.

Beyond the specification, the context in this sense includes what the post calls the AI rules ecosystem — the per-assistant context files and the shared [[DefinedTerm/agents-md]] convention, skills, specialised agents and MCP servers — and the post says it brings conventional engineering practices such as test harnesses and linters back to the fore, without which the quality of the code and architecture cannot be ensured. Separately, it reports that teams make linting, test harnesses and code review mandatory around agents because instructions are regularly ignored or misread.

## When It Applies

As described, CDE applies to teams moving AI-assisted coding from individual use to an industrialised team practice. It assumes the team can write down its intent and constraints explicitly, and that it has the harnesses — tests, linting, review — needed to check an agent's output against them.

The post's own caution is about over-specification: having tried BMAD and Spec Kit, two tools often cited for structuring this kind of workflow, the author found they could easily produce verbose over-documentation and slow the development cycle, and argues that a specification meant for an AI must be simple and unambiguous. Its conclusion states the failure mode plainly — if a team cannot explain what it wants to do and how it means to do it, AI will not save it but will produce technical debt at industrial speed.

How well established it is: the name is used in one practitioner's survey post, which links it to wider discussion of context engineering and agentic engineering rather than claiming to have coined it. The post supports the spec/plan/act workflow mainly with quotes from practitioners' own published writing, plus one contributing company's account of its variant; none of it is a measured comparison.

## Related Terms

- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/agentic-engineering]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/vibe-coding]]
- [[DefinedTerm/agents-md]]
