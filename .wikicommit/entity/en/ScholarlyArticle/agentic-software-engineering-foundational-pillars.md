---
title: "Agentic Software Engineering: Foundational Pillars and a Research Roadmap"
type: "schema:ScholarlyArticle"
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
  description: "A 2025 vision paper proposing Structured Agentic Software Engineering (SASE), a framework of dedicated human/agent workbenches, version-controlled artifacts, and named engineering activities for the Agentic Software Engineering (SE3.0) era, alongside a six-level agency/autonomy hierarchy and a research roadmap."
  author: ["Ahmed E. Hassan", "Hao Li", "Dayi Lin", "Bram Adams", "Tse-Hsun Chen", "Yutaro Kashiwa", "Dong Qiu"]
  datePublished: "2025"
  keywords: ["Agentic Software Engineering", "AI Agent", "Agentic AI", "Coding Agent"]
---

"Agentic Software Engineering: Foundational Pillars and a Research Roadmap" is a 2025 vision paper by researchers at Queen's University, Concordia University, the Nara Institute of Science and Technology, and Huawei Canada. It argues that Agentic Software Engineering (SE3.0) needs disciplined structure rather than just more capable agents, and introduces a duality between SE for Humans and SE for Agents that reimagines software engineering's actors, processes, tools, and artifacts around that split. Its central proposal is [[DefinedTerm/structured-agentic-software-engineering]] (SASE), a conceptual scaffold of dedicated environments, version-controlled artifacts, and named engineering activities for the two modalities. The paper also proposes a six-level hierarchical framework distinguishing agency from autonomy, grounds its argument in a worked example of a developer resolving seven pull requests through a team of agents, and closes with a research roadmap and a discussion of implications for software engineering education.

## Key Points

- Proposes [[DefinedTerm/structured-agentic-software-engineering]] (SASE), reimagining software engineering's four pillars — actors, processes, tools, and artifacts — around a duality of SE for Humans (SE4H) and SE for Agents (SE4A).
- Introduces [[DefinedTerm/se-autonomy-levels]], a six-level hierarchy (SE1.0–SE5.0) distinguishing agency (executing a plan) from autonomy (formulating goals), modeled on SAE self-driving automation levels.
- Defines two purpose-built workbenches — the [[DefinedTerm/agent-command-environment]] (ACE) for human coaches and the [[DefinedTerm/agent-execution-environment]] (AEE) for agents — connected by version-controlled artifacts such as [[DefinedTerm/briefingscript]], [[DefinedTerm/loopscript]], and [[DefinedTerm/mentorscript]].
- Names five structured engineering activities — [[DefinedTerm/briefing-engineering]], [[DefinedTerm/agentic-loop-engineering]], [[DefinedTerm/ai-teammate-mentorship-engineering]], [[DefinedTerm/agentic-guidance-engineering]], and a joint [[DefinedTerm/ai-teammate-lifecycle-engineering]]/[[DefinedTerm/ai-teammate-infrastructure-engineering]] discipline — that operationalize SASE.
- Reports that recent audits of SWE-Bench-style benchmark results show agent-generated code frequently falls short of being merge-ready despite passing tests, citing findings such as GPT-4 patch true-solve rates dropping from 12.47% to 3.97% after manual review, and traces a progression from [[Dataset/swe-bench]] to [[Dataset/swe-bench-verified]] (introduced to address task ambiguity and underspecification) to [[Dataset/swe-bench-pro]] (recommended as contamination concerns grew).
- Cites an early study finding that 83.8% of Claude Code-assisted pull requests on GitHub were eventually merged, and cites the [[Dataset/aidev]] dataset of 932,791 agent-authored pull requests as evidence that agentic coding is already widespread.

## Notes

The paper positions itself as a "conceptual scaffold," not a definitive solution, explicitly inviting the community to challenge, refine, and extend its proposed activities. It compares SASE to related efforts — the [[DefinedTerm/plan-do-assess-review]] loop with [[DefinedTerm/product-requirement-prompt]]s, agent-skill plugin libraries, meta-prompt files like CLAUDE.md/AGENT.md (see [[DefinedTerm/agents-md]]), and the [[SoftwareApplication/bmad]] multi-agent framework — arguing SASE differentiates itself through "mentorship-as-code," dual workbenches, merge-readiness as the target artifact, and consultation as a first-class artifact. It builds on the same authors' earlier "Towards AI-Native Software Engineering (SE3.0)" proposal, cited in the paper's own references but not itself analyzed here.
