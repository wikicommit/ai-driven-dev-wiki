---
title: "可控、可测、可进化——B2B 跨境支付的 AI 驾驭实践｜QCon 上海"
type: "schema:NewsArticle"
lang: en
tags: [qcon, loop-engineering, ai-evaluation, enterprise-ai-adoption]
sources:
  - type: url
    url: 'https://www.infoq.cn/article/UC6jk6tu7fWE5bDO8oQw'
    hash: sha256:981ebc4561e43e76aa238b5b9f3b230ea9f73f1d5cd0a1fef2754811e83941ed
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A September 2026 InfoQ China announcement of a QCon Shanghai 2026 talk by a senior technical director at XTransfer, outlining a three-layer \"controllable, testable, evolvable\" AI engineering flywheel used for risk control in B2B cross-border payments."
  datePublished: "2026-09-27"
  publisher: "InfoQ"
---

The article ("Controllable, testable, evolvable — AI harnessing practice in B2B cross-border payments") is InfoQ China's announcement, dated 27 September 2026, of a talk scheduled for QCon Shanghai 2026, held 22–24 October, in a track on AI-native engineering practice in finance. The speaker is a senior technical director at XTransfer, and the talk is titled "可控、可测、可进化——B2B跨境支付风控的 AI 驾驭实践", with risk control named explicitly. The article reproduces the speaker's talk outline, so its content is the speaker's own account of his team's practice ahead of the talk rather than independent reporting.

The problem the talk sets out is that B2B cross-border trade involves many countries, many document types and many risks: business licences and customs declarations come in widely varying layouts, verification draws on fragmented data sources, and transaction risk review and customer service depend heavily on people. Its framing is that the industry is moving from "AI tools" to "AI digital employees", and that the stronger the model, the more it needs engineering to harness it.

## Key Points

- The team's answer is a three-layer AI engineering flywheel described as "controllable, testable, evolvable", organised around four actions: harnessing (access and scheduling), constraining (standards and gates), feedback (evaluation and observation) and evolution (feeding results back for iteration).
- The minute-level layer is an Agentic Coding Loop called CodeLynx, described as evolving from Sonar static rule scanning to a knowledge-base-driven code workflow agent and then a native agent, covering both incremental change review and full-repository scans.
- CodeLynx's stated key decisions include preferring structured rules over free LLM reasoning, routing to the best model on the basis of annotated evaluation, and splitting work between a light reasoning engine for low-cost broad scanning of code standards and a heavy reasoning engine aimed at zero missed detections on red-line checks.
- The hour-level layer is a Developer Feedback Loop called EvalHub: one evaluation infrastructure for large and small models, multimodal models, knowledge bases and agents, built from evaluation sets, evaluation scenarios, scorers (including LLM-as-a-judge and the Ragas and DeepEval metric sets) and evaluation tasks.
- The day-level layer is an External Feedback Loop called EagleEye, built on the OpenTelemetry protocol, which observes infrastructure, models, services and business effect, attributes tokens by application and consumer, and feeds bad cases — pre-labelled by an LLM and confirmed by people — back into the evaluation sets.
- The speaker describes the three loops as interlocking: minute-level checks protect the quality of AI-written code, hour-level evaluation gates release quality, and day-level production feedback drives further evolution.
- Reported outcomes, in the speaker's own account, are that multimodal models made previously "non-automatable" risk-control document review automatable with manual entry steadily falling, that AI-driven multi-source cross-validation surfaces hidden relationships in supply chains, and that customer service moved from "people using tools" to "people managing a team of agents".
- The core lessons listed are treating evaluation sets as assets with versioning, freshness and feedback mechanisms; making AI cost attributable and explainable; and treating AI engineering as organisational engineering, with developers, rule maintainers and managers in distinct roles.
- Stated pain points are that general OCR and multimodal models are unstable on minority-language and non-standard document layouts, and that pure LLM free reasoning drifts in highly deterministic scenarios such as coding standards and risk-control red lines.

## Context

The same QCon Shanghai programme lists tracks on [[DefinedTerm/loop-engineering]] and on quality debt in the [[DefinedTerm/vibe-coding]] era, and the conference itself is framed around engineering practice for "harness AI". The talk's split between deterministic rules and model judgment, and its use of evaluation as a release gate, sit alongside themes this wiki covers under [[DefinedTerm/llm-as-a-judge]] and [[DefinedTerm/deterministic-quality-gate]]. All results here are the speaker's own claims made in a pre-conference outline.
