---
title: "Memory bank"
type: "schema:DefinedTerm"
lang: en
tags: [spec-driven-development, coding-agents]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html'
    hash: sha256:a502c8234d3e0bd54bf8eec4d887723cc3b3872d1015d79b4f4c6143f2498f7b
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The general context documents for a codebase — such as rules files and high-level descriptions of the product and codebase — that are relevant across all AI coding sessions, as distinguished from task-specific specs; a name some tools use, adopted by Birgitta Böckeler for this category."
---

A memory bank is the set of general context documents for a codebase that an AI coding agent is given
across all sessions — things like rules files or high-level descriptions of the product and the
codebase. In [[BlogPosting/understanding-spec-driven-development-kiro-spec-kit-and-tessl]], Birgitta
Böckeler adopts the name, which she says some tools use for this context, to draw a line between it and
specs in [[DefinedTerm/spec-driven-development]]: memory bank files are relevant to every AI coding
session in the codebase, whereas specs are relevant only to the tasks that create or change the
particular functionality they describe.

## Usage

The article's examples of memory bank files include [[DefinedTerm/agents-md]], a project description
and an architecture description. It also maps the concept onto three SDD tools: in
[[SoftwareApplication/kiro]] the memory bank is called "steering", and asking Kiro to generate steering
documents creates product.md, structure.md and tech.md by default, though its workflow does not seem to
rely on any specific files being present; in [[SoftwareApplication/github-spec-kit]] it is the
"constitution", a prerequisite of the workflow meant to hold high-level, "immutable" principles
applied to every change — in the author's words, a very powerful rules file; and in the Tessl
Framework ([[SoftwareApplication/tessl]]) it included a framework folder together with KNOWLEDGE.md and
AGENTS.md files. The author reports that "How do I structure my memory bank?" is among the questions
she hears most often from practitioners.

## Related Terms

- [[DefinedTerm/spec-driven-development-levels]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/agents-md]]
