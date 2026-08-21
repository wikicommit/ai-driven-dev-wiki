---
title: "Adaptation of Agentic AI: A Survey of Post-Training, Memory, and Skills"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-architecture, agent-skills, evaluation, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.16301'
    hash: sha256:cea102aa7b528888c4db1d1deb39f67daf880c8e85b507da8cf194b1ab98e143
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A large multi-institution survey unifying post-training, retrieval, memory, and skill systems under a single notion of adaptation — improving an agent, its tools, or their interaction after pretraining — organised by a four-paradigm framework that separates adapting the agent from adapting its tools."
---

"Adaptation of Agentic AI" is a survey with a large author list spanning UIUC, Stanford, Princeton, Harvard, UC Berkeley, Caltech, the University of Washington, UC San Diego, Georgia Tech, Northwestern, Texas A&M, MGH, and industry.

Its framing observation is that "LLM agents are moving beyond prompting alone," and it traces three moments to make the point: ChatGPT marking the rise of general-purpose LLM assistants, DeepSeek showing "that on-policy reinforcement learning with verifiable rewards can improve reasoning and tool use," and OpenClaw highlighting "a newer direction in which agents accumulate persistent memory and reusable skills." Its diagnosis of the resulting literature is that it "remains fragmented across post-training, retrieval, memory, and skill systems."

Its unifying move is to define **adaptation** as "improving an agent, its tools, or their interaction after pretraining," and to treat everything from fine-tuning to a skill library as instances of one thing.

## Key Contributions

The organising framework has four paradigms across two sides.

- **Agent adaptation** improves the agent itself, through supervised fine-tuning, preference optimization, and reinforcement learning with verifiable rewards. It splits by what supplies the training signal: **A1 (tool-execution-signaled)** and **A2 (agent-output-signaled)**.
- **Tool adaptation** improves what the agent calls. **T1 (agent-agnostic)** "provides reusable pre-trained modules any agent can call," while **T2 (agent-supervised)** "uses the agent's outputs to train memory systems, skill libraries, or lightweight subagents."

Using that framework, the survey reviews post-training methods, adaptive memory architectures, and agent skills; compares their trade-offs "in cost, flexibility, and generalization"; and summarises evaluation practices across four application areas — deep research, software development, computer use, and drug discovery. It closes on open problems in agent-tool co-adaptation, continual learning, safety, and efficient deployment. It maintains an accompanying curated reading list.

## Notes

The framework's useful contribution here is the agent/tool axis, because it names a distinction the practitioner vocabulary blurs. [[DefinedTerm/agent-skills]] and [[DefinedTerm/agentic-memory]] are, in these terms, tool adaptation rather than agent adaptation — ways of improving what the agent can reach rather than what the agent is — and the T1/T2 split further separates a skill anyone can install from one the agent's own outputs trained. That matters for a reader deciding where to invest: the levers available to someone configuring a coding agent are almost entirely on the tool side, since the agent side requires training access.

Framed that way, [[DefinedTerm/harness-engineering]] is a practitioner name for a subset of the T-side of this taxonomy, and the survey's "agent-tool co-adaptation" open problem is the academic form of the post-training coupling that practitioners observe when a model performs best in the harness it was trained on (see [[DefinedTerm/agent-harness]]).

This is a literature survey rather than new measurement; its claims belong to the works it reviews, and the material here comes from its abstract and framework description.
