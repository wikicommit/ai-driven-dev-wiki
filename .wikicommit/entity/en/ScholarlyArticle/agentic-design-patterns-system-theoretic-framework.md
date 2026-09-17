---
title: "Agentic Design Patterns: A System-Theoretic Framework"
type: "schema:ScholarlyArticle"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.19752'
    hash: sha256:8507eb6e9d0c705b9a20033d2718cc2c6f14ee2603bbe1ca8272613bf9d9c67c
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A NeurIPS 2025 workshop paper proposing a system-theoretic framework that deconstructs an agentic AI system into five core functional subsystems, deriving from it a catalogue of 12 reusable agentic design patterns, and validating the framework through a case study diagnosing and prescribing improvements to the ReAct framework."
  author: ["Minh-Dung Dao", "Quy Minh Le", "Hoang Thanh Lam", "Duc-Trong Le", "Quoc-Viet Pham", "Barry O'Sullivan", "Hoang D. Nguyen"]
  keywords: ["agentic design patterns", "system theory", "agent architecture", "LLM agents", "multi-agent systems"]
---

This paper argues that existing catalogues of agentic design patterns are either high-level strategic concepts lacking implementable structure or convenience-based, bottom-up aggregations of observed functionalities that lack a unifying theoretical foundation. It proposes a system-theoretic agent architecture that deconstructs an agent into five functional subsystems arranged as nested layers: a Reasoning & World Model (RWM) subsystem at the cognitive core, an operational-interface layer consisting of Perception & Grounding (PG) and Action Execution (AE) — extensible with an optional Inter-Agent Communication (IAC) subsystem for multi-agent capabilities — and an outermost Learning & Adaptation (LA) subsystem that observes the inner layers and closes the feedback loop with strategy and knowledge updates.

## Key Points

- The paper categorizes contemporary problems in foundation-model-based agentic AI into five classes — World Modelling, Cognitive & Decision, Execution & Interaction, Learning & Governance, and Collaboration Mechanism — citing issues such as agents favoring pretrained knowledge over retrieved information (leading to hallucination), unreliable verbal confidence as a proxy for actual uncertainty, non-deterministic "black-box" tool-use behavior that is difficult to debug, catastrophic forgetting when adapting to new data, and communication/coordination breakdowns from ambiguous language or asynchronous message sequencing.
- From the five-subsystem architecture, the paper derives a catalogue of 12 Agentic Design Patterns (ADPs) organized into four groups: Foundational patterns (Integrator, Retriever, Recorder) for building the agent's understanding and state; Cognitive & Decisional patterns (Selector, Planner, Deliberator) for shaping agent thought and action; Execution & Interaction patterns (Executor, Tool Use, Coordinator) for enabling action and engagement; and Adaptive & Learning patterns (Reflector, SkillBuild, Controller) for enabling improvement and evolution.
- The paper explicitly frames its contribution as systematizing already-known individual concepts — it states that ideas such as reflection, skill acquisition, and tool use are not themselves new, and that its contribution lies in organizing them into a cohesive catalogue of architectural design patterns for LLM-based agents, not in inventing the underlying concepts.
- As a validating case study, the paper deconstructs the [[DefinedTerm/react-prompting]] framework onto its five subsystems: ReAct's "Thought" generation is mapped to a monolithic, implicit RWM; its unstructured "Observations" are mapped to a rudimentary PG; its "Act" step is mapped to AE; and the paper states ReAct has no Learning & Adaptation or Inter-Agent Communication mechanism at all, being a single-agent framework with no long-term learning.
- From this diagnosis, the paper prescribes specific patterns to enhance ReAct: the Integrator pattern to validate incoming observations (triggering the Recorder and Reflector on a critical inconsistency), the Retriever and Recorder patterns for context retrieval and state management within the RWM, the Executor and Tool Use patterns for reliable action execution, and the Reflector pattern again for causal analysis of execution feedback to adjust future strategy.
- The paper's stated limitations are that the framework is primarily conceptual and has not yet been quantitatively benchmarked against baselines; that more sophisticated patterns such as Reflector and Controller introduce architectural complexity and potential computational overhead whose trade-offs require further investigation; and that the work does not fully address broader societal impacts of large-scale autonomous systems, such as accountability and emergent behavior.

## Notes

The paper states that a detailed description of all 12 patterns is available in a full version of the work not included in this workshop paper; the summary above draws on the brief per-pattern descriptions and the Table 2 catalogue overview given in this extracted text. Several tables in the extracted text are visually garbled by OCR/markdown conversion.
