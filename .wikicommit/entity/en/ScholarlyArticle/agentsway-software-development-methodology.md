---
title: "AGENTSWAY — Software Development Methodology for AI Agents-Based Teams"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, software-development-process, human-ai-collaboration]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2510.23664'
    hash: sha256:9b548383406928d935923cf76102f1d6e5439b916ae6a40ffcfd540913ca2080
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A preprint dated 29 October 2025 proposing Agentsway, a software development methodology designed for teams in which AI agents are first-class collaborators, with a human orchestrator, five specialized agent roles, and a privacy-preserving fine-tuning loop for retrospective learning."
  author:
    - "Eranga Bandara"
    - "Ross Gore"
    - "Xueping Liang"
    - "Sachini Rajapakse"
    - "Isurunima Kularathna"
    - "Pramoda Karunarathna"
    - "Peter Foytik"
    - "Sachin Shetty"
    - "Ravi Mukkamala"
    - "Abdul Rahman"
    - "Amin Hass"
    - "Ng Wee Keong"
    - "Kasun De Zoysa"
    - "Aruna Withanage"
    - "Nilaan Loganathan"
  datePublished: "2025-10-29"
  keywords:
    - "Agentic-AI"
    - "AI Agents"
    - "LLM-Reasoning"
    - "Large Language Model"
    - "Software Development Methods"
---

This paper argues that traditional software development methodologies such as Agile, Kanban, and Shape Up were designed for human-centric teams and are increasingly inadequate in environments where autonomous AI agents contribute to planning, coding, testing, and continuous learning. To address what the authors describe as a methodological gap — the lack of a formal process model defining how AI agents should systematically collaborate with each other and with human supervisors across the lifecycle — it presents [[DefinedTerm/agentsway]], a framework for ecosystems in which AI agents operate as first-class collaborators.

The methodology defines a team architecture in which a single human orchestrator works with a suite of specialized agents. The human is primarily responsible for interpreting high-level business goals, conducting stakeholder interactions, validating agent-generated artifacts, and providing governance and ethical oversight, while planning, prompting, coding, testing, and fine-tuning are delegated to dedicated agents.

A distinguishing feature is that the methodology closes a learning loop rather than only a delivery loop. After each development cycle, Fine-Tuning Agents collect task data, prompts, generated code, and testing feedback and use it to refine pre-trained LLMs incrementally, in what the paper calls a retrospective learning process. The authors emphasize a privacy-by-design architecture in which model training, fine-tuning, and data exchange occur entirely within secure organizational and regulatory boundaries.

## Key Contributions

The paper summarizes its contributions as four: proposing the Agentsway methodology itself; introducing a human-in-the-loop orchestration model in which the human acts as the primary orchestrator while delegating specialized functions to autonomous agents; developing a continuous improvement mechanism for LLM fine-tuning driven by feedback from different agents across the development cycle; and demonstrating applicability through a real-world use case focused on an agentic AI workflow for legal case handling automation.

Responsible AI is addressed through an ensemble arrangement rather than a single model. The paper describes multiple fine-tuned LLMs operating as a consortium alongside a dedicated reasoning LLM: an agent distributes its prompts across several fine-tuned models to obtain diverse responses, and the reasoning model then synthesizes and validates those inputs to produce the final decision or artifact. The authors argue this ensemble-based reasoning enhances both the accuracy and the accountability of agentic decisions.

The evaluation covers three components in the context of the legal case handling use case. The Planning Agent was assessed on its ability to decompose an abstract goal into actionable tasks and produce a structured pitch; the paper reports that the generated pitch received an average rating of 4.7 on a 5-point Likert scale for coherence, correctness, and implementation readiness. The Prompting Agent was assessed on generating implementation-ready prompts for downstream coding agents. The fine-tuning evaluation examined training and validation loss curves, with the authors noting that consistently positive loss differences suggest signs of overfitting at some steps.

The paper also includes a comparison table positioning Agentsway against Waterfall, Agile, Kanban, Lean, the Spiral Model, XP, Crystal, and Shape Up. In that table Agentsway is the only entry marked "Yes" for targeting AI — Agile is marked "Partial" and the rest "No" — and the only entry marked as supporting LLM fine-tuning.

## Notes

The authors state that, to the best of their knowledge, this is the first research effort to introduce a dedicated methodology explicitly designed for AI agent–based software engineering teams. They also note that while the paper focuses on managing AI agents within software development projects, the underlying principles can be extended to other collaborative, team-based environments that integrate AI agents — and identify legal, tourism, and cybersecurity as domains for future evaluation of the method's scalability and domain adaptability.
