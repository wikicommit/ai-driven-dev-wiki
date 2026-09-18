---
title: "SE Autonomy Levels (SE1.0–SE5.0)"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A six-level hierarchy (Level 0-5, corresponding to SE1.0-SE5.0) that classifies AI involvement in software engineering by distinguishing agency (executing a given plan) from autonomy (independently formulating goals), modeled on the SAE levels of self-driving automation."
---

SE Autonomy Levels is a six-level hierarchy proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] that distinguishes agency — the capacity of a system to act and execute plans to achieve a given goal — from autonomy — the capacity of a system to self-govern and independently formulate those goals. It maps six levels of AI involvement in software engineering onto this distinction, drawing an explicit parallel with the Society of Automotive Engineers' levels of self-driving automation.

## Usage

The six levels are: **Level 0, Manual Coding (SE1.0)** — no AI mapping; the human manually translates ideas into code using plain text editors, paralleling SAE Level 0 (no automation). **Level 1, Token Assistance (SE1.5)** — maps a developer's immediate editing intent to predicted tokens, as in standard IDE autocomplete, paralleling SAE Level 1 (driver assistance). **Level 2, Task-Agentic (SE2.0)** — maps a planned code change to a complete generated block of code (e.g. GitHub Copilot, Amazon CodeWhisperer), paralleling SAE Level 2 (partial automation, human must supervise). **Level 3, Goal-Agentic (SE3.0)** — maps a technical goal (e.g. "add a caching layer") to a multi-step plan of code changes; emerging agents such as Cognition's [[SoftwareApplication/devin]], Anthropic's [[SoftwareApplication/claude-code]], Google's [[SoftwareApplication/google-jules]], and OpenAI's Codex aim for this level, paralleling SAE Level 3 (conditional automation). **Level 4, Specialized Domain Autonomy (SE4.0)** — maps a broad technical mandate for a specific domain (e.g. "ensure the reliability of the payment service") to a list of concrete technical goals, specializing along a technical-stack axis or a quality-attribute axis, paralleling SAE Level 4 (high automation within a geo-fenced domain). **Level 5, General Domain Autonomy (SE5.0)** — maps a general technical mandate to domain-specific mandates for any unfamiliar domain; the paper states this level does not yet exist and is at the conceptual/research stage, paralleling SAE Level 5 (full automation).

The paper states the immediate, industry-defining challenge lies in mastering Level 3 (SE3.0, "Agentic SE"), since the transition from Level 2 to Level 3 fundamentally shifts the human-computer relationship by introducing complexity in workflow orchestration, trust, and verification — and that the community must establish disciplined practices for goal-agentic systems before it can realistically pursue full autonomy (Levels 4–5).

## Related Terms

[[DefinedTerm/structured-agentic-software-engineering]], [[DefinedTerm/agentic-autonomy-levels]] (a separate, two-axis autonomy scheme for AI coding agents proposed by a different author)
