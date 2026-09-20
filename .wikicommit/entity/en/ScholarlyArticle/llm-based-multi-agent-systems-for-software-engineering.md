---
title: "LLM-Based Multi-Agent Systems for Software Engineering: Literature Review, Vision and the Road Ahead"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, multi-agent, software-engineering, survey]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2404.04834'
    hash: sha256:6218f286c191d560d4502ad7a112fbddc108bc1c0bfceeb18951631a6bbdba35
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A systematic review of 71 primary studies on LLM-based multi-agent (LMA) systems across the software development lifecycle, with two ChatDev case studies and a two-phase research agenda covering individual agent capabilities and agent synergy."
  author: ["Junda He", "Christoph Treude", "David Lo"]
  datePublished: "2025-07"
  keywords: ["Large Language Models", "Autonomous Agents", "Multi-Agent Systems", "Software Engineering"]
  citation: "arXiv:2404.04834"
---

This paper examines the role of [[DefinedTerm/llm-based-multi-agent-system]]s in software
engineering and sets out a vision for where they are heading. Its argument for the multi-agent form
is that real-world problems span multiple domains and require expertise from various fields, which
a single LLM-based agent is poorly placed to supply; the authors list three benefits of the
multi-agent arrangement — autonomous problem-solving, robustness and fault tolerance through
cross-examination in decision-making, and scalability to complex systems by adding agents and
reallocating tasks.

The core of the paper is a systematic review of 71 recent primary studies, found through a
keyword-based search of the DBLP publication database combined with forward and backward
snowballing, and filtered by explicit inclusion and exclusion criteria — short papers, duplicates,
non-primary work such as surveys and tool demonstrations, and papers that do not describe
multi-agent systems were all excluded, as were papers relying only on single-agent or non-agent LLM
methods. The review organizes what it finds across requirements engineering, code generation,
software quality assurance, software maintenance, and end-to-end software development. In code
generation it extracts a set of recurring agent roles — Orchestrator, Programmer, Reviewer, Tester,
and Information Retriever — and in end-to-end development it notes that system designs tend to
follow established software process models, with some works adopting Waterfall, others Agile, and a
few generating the process dynamically per project.

The authors then run two case studies using [[SoftwareApplication/chatdev]] to build a Snake game
and a Tetris game, and close with a research agenda in two phases: Phase 1 on enhancing individual
agent capabilities, and Phase 2 on optimizing agent synergy, covering human-agent collaboration,
evaluation, scaling to complex projects, industry principles, dynamic adaptation, and privacy.

## Key Points
- Systematically reviews 71 primary studies on LLM-based multi-agent (LMA) systems in software
  engineering, mapped across requirements engineering, code generation, quality assurance,
  maintenance, and end-to-end development
- Defines an LMA system as comprising two components — an orchestration platform and LLM-based
  agents — and characterizes the platform by its coordination models, communication mechanisms, and
  planning and learning styles
- Identifies recurring agent roles in code generation: Orchestrator, Programmer, Reviewer, Tester,
  and Information Retriever
- Observes that end-to-end LMA designs draw on established software process models, with works
  adopting Waterfall or Agile and a few generating the process dynamically from the requirement
- Reports two case studies with ChatDev: the Snake game succeeded on the second attempt, while
  Tetris required ten attempts and the resulting game still lacked the ability to remove completed
  rows — which the authors read as a limit on tasks requiring deeper logical reasoning and
  abstraction
- Argues LMA systems are a more appropriate approach than Mixture of Experts for software
  engineering, on the grounds that MoE experts do not communicate with one another while LMA agents
  can exchange information, incorporate tool feedback, and support human-in-the-loop intervention
- Proposes a two-phase research agenda: enhancing individual agent capabilities, then optimizing
  agent synergy

## Notes

The two case studies use a single framework and two classic games, so they illustrate the authors'
point about complexity limits rather than measuring it; the authors present them as demonstrations
of current capabilities and limitations.

The authors name one threat to validity themselves: relevant studies may have been inadvertently
excluded during literature search and selection, which they sought to mitigate through the breadth
of the DBLP search and through snowballing.
