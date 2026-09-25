---
title: "Shift Left"
type: "schema:DefinedTerm"
lang: en
aliases: ["Shift-Left", "Shift Left AI"]
tags: [devops, specification, software-quality]
sources:
  - type: url
    url: 'https://www.codecentric.de/wissens-hub/blog/shift-left-and-right-wie-ki-integration-ueber-das-coding-hinauswaechst'
    hash: sha256:c56eb7ca57b7c6a3d943d7e214b28e500b4b15141ffd4b5854443353c81b9ebc
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The practice of ensuring quality and clarity earlier in the software development lifecycle; in AI-assisted development, the specification before coding becomes its main lever."
---

Shift Left is the practice of ensuring quality and clarity earlier in the software development lifecycle. According to [[BlogPosting/shift-left-and-right-how-ai-integration-grows-beyond-coding]], the term was coined in 2001 by Larry Smith in response to a then-common problem: testing happened at the end of the cycle, which led to high rework costs and poor quality, and testing early avoided expensive iterations. That post counts test-driven development, the test pyramid and ultimately CI/CD as practices that developed from the idea and are, at their core, Shift Left movements.

## Usage

The term comes from the DevOps and testing world. The codecentric post applies it to AI-assisted development, where it argues that the specification becomes the decisive lever: when the AI coding loop receives a clear, consistent and complete specification as input, the number of generate-check-discard cycles falls, whereas a patchy specification leads the loop to generate several variants, most of which are thrown away. The kinds of AI support it names for this stage are LLM spec reviews that check requirement consistency, find contradictions and propose test cases; automatic consistency checks of new requirements against existing ones; and AI-proposed, testable acceptance criteria tailored to each feature. It adds that more people take part in specifying — engineers so that technical feasibility enters the spec from the start, designers so that user-experience decisions are made at specification level, and product managers who must define requirements precisely enough, with the right context, for a coding agent.

Its counterpart, applied after deployment, is [[DefinedTerm/shift-right]].

## When It Applies

The codecentric post presents the AI-era version of the practice as a response to accelerated code generation: its suggested signal for addressing it is that coding-loop acceleration already exists but the business sees no tangible added value, for instance when product owners and requirements engineers can no longer keep pace. It assumes that the specification is sharpened for the next coding cycle before entering it and refined continuously — not that everything is specified up front, which it says would be a misreading that makes the practice sound like waterfall. The evidence it offers for the AI-assisted version is the practice experience it reports, including one anonymised customer project where LLM-supported spec reviews were reported to halve coding-loop iterations per feature; it rates the practice's maturity in Germany as just emerging.

## Related Terms

- [[DefinedTerm/shift-right]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/outer-loop]]
