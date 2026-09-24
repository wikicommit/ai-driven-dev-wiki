---
title: "Context Fluency"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, context-engineering, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.05400'
    hash: sha256:1f126c8e3d5e00a7ac0db71cd27186c357be2d109f14c9979f133b56b18b3303
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A term proposed by Andrew Zigler for the developer skill of creating rich, structured context that AI agents can act on — capturing domain expertise, value judgments and design intent in machine-legible, persistent form rather than as one-shot prompts."
---

Context fluency is a term proposed in [[ScholarlyArticle/mise-en-place-for-agentic-coding]] for the
ability to create rich, structured context that AI agents can act on. The author presents it as a
skill distinct from both traditional programming and prompt engineering: it captures domain
expertise, value judgments and design intent in machine-legible form, not as one-shot prompts but as
persistent informational environments. Where [[DefinedTerm/prompt-engineering]] optimizes individual
instructions, context fluency is described as upstream of prompting, concerned with the informational
architecture surrounding agent execution; and where the paper's
[[DefinedTerm/mise-en-place-methodology]] describes a sequence of phases producing artifacts, context
fluency names the practitioner skill that makes that process effective.

## Usage

The paper identifies four components of the skill. **Decomposition** is breaking problems into
discrete, parallelizable tasks with clear boundaries so agents can execute concurrently.
**Specification** is describing not only what to build but why, so agents can make aligned
micro-decisions without human intervention. **Constraint definition** is knowing what to exclude,
simplify or defer, treating scope management as a first-class concern. **Domain encoding** is
externalizing tacit knowledge that agents cannot generate on their own; in the paper's hackathon case,
twenty minutes of dictated pedagogical intuitions are reported to have substantially reduced iteration
on the domain-specific tutor component.

The author connects these components to backward design (outcome-driven preparation), to Polanyi's
account of tacit knowledge — "we know more than we can tell", with context fluency described as the
discipline of telling it anyway — and to pedagogical scaffolding, structuring an environment so that
a learner, or an agent, can act independently. If it is a distinct skill, the paper suggests,
developer education should cultivate specification, decomposition and domain encoding alongside
programming; practitioners with strong domain knowledge and pedagogical instincts may be
disproportionately effective in agentic workflows; and preparation aids such as task systems,
specification frameworks and context-engineering platforms become essential infrastructure. Whether
context fluency is trainable or a function of prior domain knowledge is one of the open questions the
paper poses, and it has not been empirically validated.

## Related Terms

- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/prompt-engineering]]
- [[DefinedTerm/mise-en-place-methodology]]
- [[DefinedTerm/briefing-engineering]]
