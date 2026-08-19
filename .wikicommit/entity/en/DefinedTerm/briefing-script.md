---
title: "BriefingScript"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, specification, human-ai-collaboration, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "In the Structured Agentic Software Engineering framework, a structured, version-controlled mission brief that replaces an ad-hoc prompt: a detailed work order carrying success criteria, architectural context, strategic advice, and known pitfalls for an autonomous agent."
---

A BriefingScript is the human-authored mission brief proposed in [[DefinedTerm/structured-agentic-software-engineering]] as a first-class engineering artifact replacing the ad-hoc prompt. [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] describes it as much more than a specification of intent — it is "the detailed work order that a senior developer would give a junior one to ensure success", authored and maintained under version control so that the shared understanding of a task stays current and auditable.

## Usage

The paper identifies a common failure pattern it is designed to counter: pasting a raw, vague ticket at an agent and expecting magic. It contrasts this with how highly productive practitioners work — treating an agent as a junior team member or outsourced partner rather than a magical tool, and providing a comprehensive initial briefing that includes not only the specification but also the bigger picture, relevant context, and strategic advice on how to break down and approach the task.

A BriefingScript is specified to carry four kinds of content:

- **What and success criteria** — the scope with a verifiable checklist, similar to Scrum's "Definition of Done" but enriched with formal, testable properties such as pre-conditions and invariants
- **Architectural context** — where the work fits in the system, identifying key modules, data models, or APIs to interact with
- **Strategic advice** — recommended implementation approaches, such as libraries to use or patterns to avoid
- **Potential "gotchas"** — known pitfalls or tricky areas such as subtle business logic, performance constraints, or dependency issues

The paper is explicit that a BriefingScript is not a rigid, one-shot specification. Like pair programming or collaborative design, it is meant to evolve through iterative dialogue between the human coach and the agent: early drafts may be lightweight and progressively enriched with clarifications and refinements based on agent feedback. The authors argue this iterative style avoids the brittleness of upfront, waterfall-style specifications, and that subsequent clarifications must be incorporated back into the BriefingScript as versioned updates so it becomes an evolving, auditable record.

Structurally it is described as a machine-readable artifact that may be serialized in formats such as Markdown, YAML, JSON, or a domain-specific schema — explicitly not a new programming language. The authors frame this as a modern, agent-oriented evolution of Donald Knuth's concept of literate programming: instead of treating code as the primary artifact, the focus shifts to the human-readable brief that explains the logic and intent from which the agent's work is derived.

Authoring these briefs is codified in the framework as a named activity, Briefing Engineering (BriefingEng), described as a hybrid discipline fusing requirements specification with architectural design, strategic implementation advice, and test planning. The paper argues formalization is more tractable in an agentic context than in past formal-methods efforts for three reasons: the primary consumer is a machine, which benefits from formal structure; briefs cover far more granular tasks than a monolithic Software Requirements Specification; and modern AI assistants can help humans write structured briefs, lowering the barrier to entry. Looking ahead, the authors suggest that as an agent becomes more attuned to a codebase and its human collaborators, the explicit human-drafted portion of these scripts should shrink.

## Related Terms

The BriefingScript is one of three human-authored artifacts in the framework, alongside the LoopScript (a declarative workflow playbook defining the agent's Standard Operating Procedure) and the MentorScript (a version-controlled rulebook codifying team norms and best practices). Agents respond to it with a [[DefinedTerm/consultation-request-pack]] when they need human judgment and a [[DefinedTerm/merge-readiness-pack]] when submitting finished work. The paper discusses the Product Requirement Prompt (PRP) as an emerging industry example of a BriefingScript-like artifact, and notes that meta-prompt files such as `CLAUDE.md` and `AGENT.md` are a grassroots analogue of MentorScript.
