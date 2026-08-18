---
title: "Spec-Driven Development"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, terminology, software-development-process]
sources:
  - type: url
    url: 'https://github.github.com/spec-kit/concepts/sdd.html'
    hash: sha256:8eb0247a43c5afbc5b75f447d9f90202cdd390cf55fa951daad26cb7eedbad2f
review_status: pending
generated_at: "2026-08-18"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A structured development process in which specifications become executable and directly generate working implementations, rather than serving as scaffolding discarded once coding begins. As presented by the [[SoftwareApplication/spec-kit]] documentation, it emphasizes intent-driven development, rich specification creation, multi-step refinement, and heavy reliance on advanced AI model capabilities."
---

Spec-Driven Development is a structured development process in which specifications become executable, directly generating working implementations rather than just guiding them. The [[SoftwareApplication/spec-kit]] documentation presents it as flipping the script on traditional software development: for decades code was king and specifications were "just scaffolding we built and discarded once the 'real work' of coding began", whereas under Spec-Driven Development the specification defines the "what" before the "how" and is the artifact the implementation is generated from.

## Usage

The Spec Kit documentation describes Spec-Driven Development as a structured process emphasizing four things: intent-driven development, where specifications define the "what" before the "how"; rich specification creation using guardrails and organizational principles; multi-step refinement rather than one-shot code generation from prompts; and heavy reliance on advanced AI model capabilities for specification interpretation.

It sets out three development phases:

| Phase | Focus | Key activities |
| --- | --- | --- |
| 0-to-1 Development ("Greenfield") | Generate from scratch | Start with high-level requirements, generate specifications, plan implementation steps, build production-ready applications |
| Creative Exploration | Parallel implementations | Explore diverse solutions, support multiple technology stacks and architectures, experiment with UX patterns |
| Iterative Enhancement ("Brownfield") | Brownfield modernization | Add features iteratively, modernize legacy systems, adapt processes |

The same documentation states the research and experimentation behind the approach focuses on technology independence — validating the hypothesis that Spec-Driven Development is a process not tied to specific technologies, programming languages, or frameworks — along with enterprise constraints such as organizational cloud providers, tech stacks, engineering practices, design systems and compliance requirements; user-centric development across different user cohorts; and creative and iterative processes including parallel implementation exploration, iterative feature development, and upgrade and modernization tasks.

Spec Kit does not prescribe how teams preserve or mutate the `spec.md`, `plan.md`, and `tasks.md` artifacts after requirements change; its documentation covers that separately under spec persistence models and the evolving-specs workflows for existing projects.

## Related Terms

Under its user-centric development goal, the Spec Kit documentation lists supporting various development approaches ranging from [[DefinedTerm/vibe-coding]] to AI-native development.
