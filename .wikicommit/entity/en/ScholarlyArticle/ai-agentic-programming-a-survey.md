---
title: "AI Agentic Programming: A Survey of Techniques, Challenges, and Opportunities"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, ai-assisted-programming, agent-architecture, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A University of Leeds survey defining AI agentic programming as a paradigm in which LLM-based coding agents autonomously plan, execute, and interact with tools such as compilers, debuggers, and version control. It offers a taxonomy of agent behaviours and system architectures and reviews planning, context management, tool integration, execution monitoring, and benchmarking."
  author:
    - "Huanting Wang"
    - "Jingzhi Gong"
    - "Huawei Zhang"
    - "Jie Xu"
    - "Zheng Wang"
---

"AI Agentic Programming" is a survey by five authors at the University of Leeds. It defines its subject as "an emerging paradigm where large language model (LLM)-based coding agents autonomously plan, execute, and interact with tools such as compilers, debuggers, and version control systems."

Its distinction from what came before is stated in terms of behaviour rather than capability: "Unlike conventional code generation, these agents decompose goals, coordinate multi-step processes, and adapt based on feedback, reshaping software development practices." Where traditional code-completion tools "respond to a single prompt with a static code snippet," the agents this survey covers "operate within dynamic software environments, performing iterative, tool-augmented tasks to achieve complex goals" — generating whole programs or modules from natural-language specifications, diagnosing and fixing bugs from compiler or test feedback, writing and executing test cases, and refactoring, as well as orchestrating external tools across an end-to-end workflow.

The survey's stated motivation is that the field is moving fast enough to need conceptual consolidation: "there is an urgent need to clarify its conceptual landscape, identify common patterns and system architectures, and assess the suitability of current development ecosystems."

## Key Contributions

The survey states five deliverables: a conceptual foundation and taxonomy of AI coding agents; a review of core system architectures and underlying techniques; a summary of the behaviour dimensions, operating modes, evaluation strategies, and benchmarking practices of AI coding agents; a discussion of key challenges and current limitations; and an exploration of future research directions, "including opportunities to bridge perspectives across disciplines such as programming languages, software engineering, AI, and human-computer interaction."

Its technical coverage spans planning, context management, tool integration, execution monitoring, and benchmarking datasets. Its scope is stated as "primarily LLM-driven agentic systems for software development, though many insights extend to general AI agents in other domains."

Its closing argument is a claim about direction rather than a summary of results: the challenges it catalogues "show that AI agentic programming is not just a new way of using existing" tools, and the opportunities it identifies are for "building reliable, transparent, and collaborative coding agents."

## Notes

This is a survey rather than an empirical study; its claims belong to the works it reviews, and the material summarised here comes from its abstract and introduction.

Its value as a reference point is terminological. "AI agentic programming" is one of several names in circulation for the same territory this wiki tracks under [[DefinedTerm/agentic-coding]], and the definition it gives — autonomous planning and execution with tool interaction, as against single-prompt code generation — matches the boundary the practitioner accounts draw, arrived at independently and from the academic side. Its three named virtues for future systems, reliability, transparency, and collaboration, sit alongside the [[DefinedTerm/verification-bottleneck]] and review-cost concerns the industry evidence records.
