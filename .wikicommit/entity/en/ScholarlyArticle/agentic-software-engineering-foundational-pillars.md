---
title: "Agentic Software Engineering: Foundational Pillars and a Research Roadmap"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, software-development-process, human-ai-collaboration]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A vision paper proposing Structured Agentic Software Engineering (SASE), a conceptual framework organizing the Agentic SE (SE 3.0) era around a duality between SE for Humans and SE for Agents, two purpose-built workbenches, and a set of version-controlled artifacts. It closes with a research roadmap and a discussion of implications for SE education."
  author:
    - "Ahmed E. Hassan"
    - "Hao Li"
    - "Dayi Lin"
    - "Bram Adams"
    - "Tse-Hsun Chen"
    - "Yutaro Kashiwa"
    - "Dong Qiu"
  datePublished: "2025-06"
  keywords:
    - "Agentic Software Engineering"
    - "AI Agent"
    - "Agentic AI"
    - "Coding Agent"
---

This paper argues that the arrival of autonomous coding agents has moved software engineering beyond AI-augmented development (which the authors label SE 2.0) and into an era they call [[DefinedTerm/agentic-software-engineering]], or SE 3.0. Its stated goal is not to offer a definitive solution but to provide a conceptual scaffold with structured vocabulary that can catalyze a community-wide dialogue.

Its central proposal is [[DefinedTerm/structured-agentic-software-engineering]] (SASE), a framework built on what the authors call a structured duality: the field must simultaneously serve *SE for Humans* (SE4H), which redefines the human role around high-level intent, strategy, and mentorship as an "Agent Coach", and *SE for Agents* (SE4A), which establishes a structured, predictable environment in which multiple agents can operate. The authors argue this duality requires systematically rethinking four foundational pillars of SE — actors, processes, artifacts, and tools — because each manifests differently across the two modalities.

The paper is written against a diagnosed gap it calls the "speed vs. trust" problem. It observes that autonomous coding agents are already responsible for large volumes of merged pull requests, but that a Cambrian explosion of ad-hoc practitioner techniques relying on informal, conversational prompting is inadequate for building trustworthy large-scale, long-lived software. That informality, the authors argue, keeps the paradigm locked in one-to-one "agentic coding" rather than N-to-N agentic software engineering, where teams of humans and agents collaborate at scale.

## Key Contributions

**A hierarchical autonomy framework.** Drawing an analogy to the SAE levels for autonomous driving, the paper distinguishes *agency* (the capacity to act and execute plans toward a given goal) from *autonomy* (the capacity to self-govern and independently formulate goals), and uses that distinction to define six levels: Level 0 manual coding (SE 1.0), Level 1 token assistance (SE 1.5), Level 2 task-agentic AI-augmented SE (SE 2.0), Level 3 goal-agentic Agentic SE (SE 3.0), Level 4 specialized domain autonomy (SE 4.0), and Level 5 general domain autonomy (SE 5.0), which the authors describe as still at the conceptual/research stage.

**Two purpose-built workbenches.** The paper argues the traditional all-in-one IDE is ill-equipped for this era and proposes replacing it with [[DefinedTerm/agent-command-environment]] (ACE), a command center optimized for human cognition, and [[DefinedTerm/agent-execution-environment]] (AEE), a workbench optimized for agent strengths such as high-speed computation and massive parallelism.

**Version-controlled artifacts as the interface.** Rather than an informal chat monologue, the exchange between the two environments is carried by explicit, version-controlled artifacts. Humans initiate with a [[DefinedTerm/briefing-script]] (mission plan), a LoopScript (workflow playbook), and a MentorScript (best-practices rulebook); agents respond with a [[DefinedTerm/consultation-request-pack]] to request human expertise and a [[DefinedTerm/merge-readiness-pack]] to present an evidence-backed deliverable; humans then answer with Version Controlled Resolutions (VCRs) linked to the artifact each addresses.

**Structured engineering activities.** SASE is operationalized through named activities: Briefing Engineering (BriefingEng), Agentic Loop Engineering (ALE), AI Teammate Mentorship Engineering (ATME) — described as "mentorship-as-code" — Agentic Guidance Engineering (AGE), and AI Teammate Lifecycle and Infrastructure Engineering (ATLE and ATIE).

**A research roadmap and education argument.** The paper closes with open research directions across each activity, and argues that SE curricula largely train students to *be* the agent, whereas the agentic era requires training them to manage fleets of agents — a shift toward system-level thinking, architectural reasoning, rigorous specification, and mentorship-as-code.

## Notes

The paper explicitly positions SASE relative to adjacent efforts rather than as a replacement for them. It describes SASE as adopting PRP-style briefs for intent formalization, Plan-Do-Assess-Review–style iterative loops, and BMAD-like multi-agent parallelism, while differentiating itself on five points: mentorship-as-code, the dual workbenches, merge-readiness as the target artifact, consultability as a first-class artifact, and agent lifecycle and infrastructure.

The authors also address a possible objection from Rich Sutton's "Bitter Lesson", which argues that general methods scaling with computation ultimately triumph over approaches that bake in specific human knowledge. Their response is that the lesson is most potent where data is abundant, and that for novel tasks or niche domains a human is still needed to provide overarching structure — so the framework does not reject scale but seeks to create the conditions for it to succeed reliably within a complex engineering context.

The authors are explicit that the framework is visionary rather than validated: it is offered as a conceptual scaffold to be challenged, refined, and extended by the community, and the paper presents no empirical evaluation of SASE itself.
