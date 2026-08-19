---
title: "Agentsway"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, software-development-process, human-ai-collaboration, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2510.23664'
    hash: sha256:9b548383406928d935923cf76102f1d6e5439b916ae6a40ffcfd540913ca2080
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A software development methodology proposed by Bandara and colleagues for AI-agent-centric teams, in which a single human orchestrator supervises specialized Planning, Prompting, Coding, Testing, and Fine-Tuning agents within a privacy-preserving, continuously self-improving lifecycle."
---

Agentsway is a software development methodology proposed by Eranga Bandara and colleagues in [[ScholarlyArticle/agentsway-software-development-methodology]] for ecosystems in which AI agents operate as first-class collaborators. It rethinks the traditional team structure by positioning the human primarily as an orchestrator while delegating specialized functions to AI agents, and adds a privacy-preserving retrospective learning loop so that each development cycle refines the models used in the next one.

## Usage

The methodology defines six entities. The human orchestrator interprets high-level business goals, conducts stakeholder interactions, validates agent-generated artifacts such as task lists, pitches, and code, and provides governance and ethical oversight. The remaining five are agent roles:

| Agent | Role |
| --- | --- |
| Planning Agent | Examines project documents, meeting summaries, and contextual artifacts to decompose requirements into executable tasks, and generates task descriptions, resource estimates, and project pitches |
| Prompting Agent | Analyzes each approved task and constructs detailed, context-aware prompts for the coding agents, encapsulating functional requirements, coding style preferences, and integration dependencies |
| Coding Agents | Translate approved prompts into executable code within defined project environments, adhering to the organization's coding standards and architectural constraints |
| Testing Agents | Execute automated unit, integration, and regression tests, perform static analysis and vulnerability scans, and produce structured reports on defects, performance, and coverage |
| Fine-Tuning Agents | Collect task data, prompts, generated code, and testing feedback after each cycle and use it to refine pre-trained LLMs incrementally |

These map onto a lifecycle of six functionalities: requirement gathering and human interaction, planning, prompting, coding, testing, and LLM fine-tuning. Human review is retained at several points — the orchestrator verifies and approves generated plans before execution begins, verifies that generated prompts accurately capture the intended requirements, and complements automated testing with manual exploratory testing for edge cases and usability aspects requiring human judgment. Deliverables such as pitches, user stories, task lists, and prompts are committed to collaborative repositories for version control, transparency, and auditability.

Two design commitments distinguish the methodology in the authors' account. The first is *privacy by design*: fine-tuning operations occur within secure organizational boundaries, so that organizational knowledge and sensitive data remain protected while the system's capability improves. The second is *responsible AI through model plurality*: rather than a single model, multiple fine-tuned LLMs operate as a consortium alongside a dedicated reasoning model, which synthesizes and validates their diverse responses into a final decision or artifact.

The paper positions Agentsway against earlier methodologies by arguing that Waterfall, the Spiral Model, Lean, Agile, Kanban, XP, Crystal, and Shape Up were all conceived for human-only collaboration, manual iteration cycles, and team-driven decision-making, and that while some of them improved productivity and adaptability, none explicitly addresses the growing role of autonomous AI agents in software creation.

## Related Terms

Agentsway is one of several methodology proposals for [[DefinedTerm/agentic-software-engineering]]. It differs from [[DefinedTerm/structured-agentic-software-engineering]] in emphasis: where that framework centres on version-controlled artifacts and separate human and agent workbenches, Agentsway centres on a fixed set of agent roles and a model fine-tuning loop that carries experience forward between cycles.
