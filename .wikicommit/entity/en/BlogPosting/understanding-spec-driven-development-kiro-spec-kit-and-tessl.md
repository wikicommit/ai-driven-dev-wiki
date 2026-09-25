---
title: "Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl"
type: "schema:BlogPosting"
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
  description: "An October 2025 article by Birgitta Böckeler in the \"Exploring Gen AI\" series on martinfowler.com that tries three tools labelled as spec-driven development — Kiro, spec-kit and the Tessl Framework — proposes three implementation levels of SDD, and raises questions about the approach's real-world usefulness."
  author: ["Birgitta Böckeler"]
  datePublished: "2025-10-15"
  publisher: "martinfowler.com"
---

This article, part of the "Exploring Gen AI" series on martinfowler.com, sets out to untangle what
[[DefinedTerm/spec-driven-development]] (SDD) means by looking at three tools that label themselves
as SDD tools: [[SoftwareApplication/kiro]], [[SoftwareApplication/github-spec-kit]] and the Tessl
Framework ([[SoftwareApplication/tessl]]). The author notes that the definition is still in flux and
summarises the usage she has seen as writing a "spec" before writing code with AI, with the spec
becoming the source of truth for the human and the AI.

From the usages of the term and the tools, she concludes that SDD has several implementation levels —
spec-first, spec-anchored and spec-as-source ([[DefinedTerm/spec-driven-development-levels]]) — and
offers her own definition of a spec, which she separates from a [[DefinedTerm/memory-bank]] of general
context documents. She describes how each tool works as she used it in September 2025, then sets out
her observations and open questions, cautioning that the tools evolve quickly and that she had not
yet heard reports from long-term use on a real codebase.

## Key Points

- The author's definition: a spec is "a structured, behavior-oriented artifact - or a set of related
  artifacts - written in natural language that expresses software functionality and serves as
  guidance to AI coding agents", with each variant of SDD defining its own structure, level of detail
  and organisation for specs.
- Every SDD approach she found is spec-first, but not all aim to be spec-anchored or spec-as-source,
  and the strategy for maintaining specs over time is often vague or left open.
- Kiro is described as the most lightweight of the three and mostly spec-first, with a
  Requirements → Design → Tasks workflow of one Markdown document per step inside its VS Code based
  distribution; requirements are user stories with GIVEN/WHEN/THEN acceptance criteria, and its memory
  bank is called "steering".
- Spec-kit, GitHub's version of SDD, is a CLI that sets up workspace files for many coding assistants
  and is then driven by slash commands, making it the most customisable of the three. Its workflow is
  Constitution → Specify → Plan → Tasks, with the "constitution" acting as a powerful rules file, and it
  relies heavily on checklists in its files. Although GitHub's writing suggests an aspiration to be
  spec-anchored, the author notes that spec-kit creates a branch per spec, which makes her think it is
  still spec-first only.
- The Tessl Framework, in private beta at the time, is the only one of the three that explicitly aims
  to be spec-anchored and is exploring spec-as-source: a spec can be the maintained artifact, mapping
  1:1 to a generated code file marked as not to be edited. Even at that low abstraction level the
  author saw non-determinism when generating code repeatedly from the same spec.
- The three tools differ considerably, so SDD "is not just one thing".
- Kiro and spec-kit each offer one opinionated workflow, which the author doubts suits most real
  problems: Kiro turned a small bug into 4 user stories with 16 acceptance criteria, and spec-kit felt
  like overkill for a mid-sized feature building on existing code. She argues an effective SDD tool
  must offer flexibility for different sizes and types of change.
- Spec-kit produced many repetitive, verbose Markdown files; the author says she would rather review
  code, and that an effective SDD tool needs a very good spec review experience.
- Despite all the files, templates and checklists, she frequently saw the agent not follow all
  instructions — for example regenerating existing classes described in research notes as if they
  were new — and also over-eagerly follow them. She is sceptical of large up-front spec design, given
  that small iterative steps have proven the best way to stay in control.
- She found it hard in practice to separate functional specs from technical detail, and questions who
  the target user is, since the tools present developers doing requirements analysis as a given.
- For spec-as-source in particular she draws a parallel with model-driven development (MDD), which
  she worked with early in her career. LLMs remove some of MDD's overhead and constraints but bring
  non-determinism and lose the tool support a parseable spec language allowed, and she wonders whether
  spec-as-source, and even spec-anchoring, might combine the downsides of both: inflexibility *and*
  non-determinism.
- She concludes that the spec-first principle is valuable in many situations, but that "spec-driven
  development" is not well defined and already semantically diffused
  ([[DefinedTerm/semantic-diffusion]]), and she asks whether some tools feed existing workflows to AI
  agents too literally, amplifying review overload and hallucinations.

## Context

The article is explicitly based on the author's own trials of the three tools in September 2025, with
limited attempts per tool, and she presents her descriptions as how she thinks the tools work. The
three levels and the definition of a spec are her own proposals for organising a term she regards as
still in flux.
