---
title: "epistemic grounding document"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, configuration, governance, spec-driven-development, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.21744'
    hash: sha256:9f7862701079fdcc2025b4eb823bc28cb07820a6313b554d8637b079e666e6f8
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A proposed context file, named GROUNDING.md, holding a domain community's non-negotiable validity rules and agreed defaults, positioned above plan, project, and technique files so that its constraints override them. Proposed in a 2026 paper using mass-spectrometry proteomics as its worked example; not an established artifact."
  termCode: "GROUNDING.md"
  inDefinedTermSet: ""
---

An epistemic grounding document is a context file proposed in [[ScholarlyArticle/agentic-ai-assisted-coding-epistemic-grounding]] to hold what a *domain community* — rather than a user, a project, or a model's training — considers necessary for output in that field to be valid. Its proposed filename is `GROUNDING.md`, and the paper is careful that no agreed name for this kind of document yet exists. It is a proposal, illustrated with a drafted proteomics file, not a deployed convention.

The paper's definition of "epistemic" here is specific: "explicit encoding of domain knowledge, such as consensus validity criteria, and accepted inferential boundaries required for software to produce scientifically trustworthy output." The gap it is meant to fill is that a plan file, a project file such as [[DefinedTerm/agents-md]], or a technique file such as a [[DefinedTerm/agent-skills]] `SKILL.md` all "lack mechanisms to enforce domain-specific validity constraints."

## Usage

**Two kinds of content, with different force.** **Hard Constraints (HCs)** are field-scoped invariants — non-negotiable validity requirements — that override all other contexts. **Convention Parameters (CPs)** are community-agreed defaults whose violation generates a warning rather than a block. Keeping the two apart is what lets the document be strict about correctness without being rigid about preference.

**A hierarchy ordered by plasticity.** The paper arranges context documents from session to project to technique to field, "ordered by decreasing plasticity," with each layer more stable, authoritative, and general than the one below, so that field-scoped invariants constrain everything beneath them. Its statement of the resulting precedence is blunt: "the GROUNDING specification wins any conflict with the plan or skills, not the other way around, preventing the AI from optimizing for immediate goals while violating field-scoped epistemic rules." The document is intended to be loaded at inference time with highest priority, via the system prompt.

**Four stated functions.** Human-readable but agent-consumed, which is what enables community governance and portability across tools; domain knowledge encoded as HCs and CPs; loaded at inference time at highest priority; and designed to support enforcement when coupled to a suitable loading strategy, validators, tests, or agent-scaffold checks.

**Where its authority comes from.** The paper's argument is that the document's force derives from provenance rather than from placement: it encodes standards defined by the domain community "(not the software developer or the AI's training)," with its proteomics example pointing at HUPO-PSI guidelines. The practical consequence it draws is that because authority rests on community consensus about validity rather than on individual user intent, the document "resists being overridden by non-experts" — which is the case it makes for the whole idea, since the person generating bespoke domain software with an agent may not be a domain expert at all.

**What it is not.** The paper distinguishes it from existing prescriptive and informational files on the grounds that `GROUNDING.md` "is prescriptive about scientific correctness rather than workflow or style, and constrains what the agent is allowed to do, regardless of user intent." It also distinguishes it from a field's existing formal guidelines, which it accepts are authoritative but "are not written for AI consumption." Its own metaphor for the artifact is a domain's "Code of Hammurabi" for AI agents, or a software contract "describing the invariants, conventions, and failure modes that every tool in the ecosystem should respect."

**How it was tested, and how far it held.** The proposal comes with a proof-of-principle evaluation rather than a deployment. Six prompts, each violating a different Hard Constraint, were run against an agent carrying both the grounding document and an adversarial project context file instructing it to ignore scientific validity; success required the agent to refuse outright and cite the constraint, with merely generating compliant code counted as a failure. The authors report the document is "authoritative largely due to its explicit language" for Hard Constraints, but that compliance "degrades under explicit override instructions or weakened normative language." On loading, they found the system prompt more consistent than XML tagging, and warn that nesting the file in a skill folder "would incorrectly subordinate it to method-scoped layers, violating its authority" — since no scaffold enforces the ordering natively, they recommend verifying with constraint-violating test prompts in whatever system it is used.

## Related Terms

The document sits at the top of a stack whose lower layers already have entries here: [[DefinedTerm/context-files]] for the project layer, [[DefinedTerm/agents-md]] for its cross-tool convention, and [[DefinedTerm/agent-skills]] for the technique layer whose `SKILL.md` the paper explicitly says cannot host field-scoped invariants, being method-scoped. Its precedence claim — that a standing rule must beat the current goal — is the same requirement [[DefinedTerm/governance-decay]] shows is violated when a harness compacts, and the paper's coupling of the document to validators and scaffold checks connects it to [[DefinedTerm/backpressure]] and [[DefinedTerm/agent-hooks]]. Because it constrains generated output rather than describing a process, it is closer in intent to a specification than to documentation; compare [[DefinedTerm/spec-driven-development]].
