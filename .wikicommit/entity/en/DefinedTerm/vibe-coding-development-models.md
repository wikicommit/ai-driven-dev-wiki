---
title: "Vibe Coding Development Models"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2510.12399'
    hash: sha256:e7a4dc7327555d0478beeb5067576e505fb504e405921ca26c1b0f2a12f26118
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A five-model taxonomy classifying how human developers and AI coding agents divide responsibility in practice, along three axes: how much a human reviews AI output, how much the workflow relies on structured constraints, and how much context management it uses."
---

Vibe Coding Development Models is a taxonomy, proposed in an academic survey, classifying how human developers and AI coding agents divide responsibility in practice along three axes: human quality control (how much a developer reviews and comprehends AI-generated code before accepting it), structured constraint mechanisms (whether the workflow uses upfront planning documents, automated tests, or rule-based constraints), and context management capability (how much the workflow relies on codebase indexing, project documentation, or retrieval-augmented generation). Different combinations of these three axes yield five named models, which the taxonomy treats as composable rather than mutually exclusive.

## Usage

The five models are: **Unconstrained Automation Model (UAM)** — AI dominates and humans supply only requirements, validating correctness through functionality testing rather than code review; likened to Rapid Application Development, and described as the model closest to vibe coding's original narrower meaning. **Iterative Conversational Collaboration Model (ICCM)** — humans review and understand each AI output before accepting it, in a repeating generate-review-test-accept cycle; likened to pair programming, with AI as "driver" and the human as "navigator." **Planning-Driven Model (PDM)** — humans write specification, coding-rule, and implementation-plan documents before AI implementation begins; likened to the waterfall model, with humans as architect and AI as the implementing "team." **Test-Driven Model (TDM)** — humans write tests as the specification and AI writes code to pass them, following the classic red-green-refactor cycle; verification is delegated to machine-checkable tests rather than human judgment. **Context-Enhanced Model (CEM)** — not a standalone workflow but a horizontal capability (retrieval-augmented generation, codebase vector indexing, documentation loading, rule constraints) that can be layered onto any of the other four models to improve how well generated code fits an existing codebase.

The source's own comparative analysis rates the four base models (with CEM as a modifier) across upfront investment, human control, structured constraints, development speed, code quality, technical debt, maintainability, and security risk: UAM is fastest but rated highest on technical debt and security risk, while TDM is tied with PDM for the highest upfront investment but is rated strictest on quality and lowest on residual security risk.

## When It Applies

The taxonomy is presented as a practical scaffold for choosing (or combining) a workflow to match a project's risk tolerance, required speed, and governance needs — for example, PDM combined with TDM for complex, high-quality projects, or ICCM combined with CEM for maintaining a large existing codebase. UAM is presented as suitable only for low-risk scenarios such as disposable prototypes and personal utilities, not for production systems, safety-critical applications, or codebases requiring long-term maintenance. The source frames the choice of model as a way to make the boundary of human-AI collaboration explicit rather than leaving it implicit.

## Related Terms

[[ScholarlyArticle/a-survey-of-vibe-coding]], [[DefinedTerm/vibe-coding]], [[DefinedTerm/spec-driven-development]]
