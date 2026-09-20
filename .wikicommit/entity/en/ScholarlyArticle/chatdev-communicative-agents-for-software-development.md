---
title: "ChatDev: Communicative Agents for Software Development"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, multi-agent, agent-architecture, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2307.07924'
    hash: sha256:615fc0d29f3cae50a8e97ac2aa2dccab1618f77299237bb910cf7c5129295e57
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint that introduces ChatDev, a chat-powered software development framework in which specialized LLM-driven agents cover the design, coding and testing phases through unified language-based communication rather than a separately designed model per phase."
  author: ["Chen Qian", "Wei Liu", "Hongzhang Liu", "Nuo Chen", "Yufan Dang", "Jiahao Li", "Cheng Yang", "Weize Chen", "Yusheng Su", "Xin Cong", "Juyuan Xu", "Dahai Li", "Zhiyuan Liu", "Maosong Sun"]
  datePublished: "2023-07-16"
  abstract: "The paper introduces ChatDev, a chat-powered software development framework in which specialized agents driven by large language models are guided in what to communicate, via a chat chain, and how to communicate, via communicative dehallucination. The agents contribute to the design, coding and testing phases through unified language-based communication, with solutions derived from their multi-turn dialogues. The authors report that natural language is advantageous for system design while communicating in programming language proves helpful in debugging, and present the paradigm as establishing language as a unifying bridge for autonomous task-solving among LLM agents."
---

This arXiv preprint introduces [[SoftwareApplication/chatdev]], a chat-powered software development
framework in which specialized agents driven by large language models take part in the design,
coding and testing phases of building software. The paper's starting point is that software
development is a complex task requiring cooperation among multiple members with diverse skills, and
that earlier work applying deep learning to individual phases of a waterfall model gave each phase
its own uniquely designed model — which the authors argue leads to technical inconsistencies across
the various phases, and so to a fragmented and ineffective development process.

ChatDev's answer is to route those phases through a single medium. Its agents are guided in *what*
to communicate by a mechanism the paper calls a chat chain, and in *how* to communicate by one it
calls communicative dehallucination. The agents actively contribute to design, coding and testing
through unified language-based communication, with solutions derived from their multi-turn
dialogues rather than from a separately designed model per phase.

The authors report an observation about which language suits which task: the agents' utilization of
natural language is advantageous for system design, while communicating in programming language
proves helpful in debugging. They present the work as demonstrating how linguistic communication
facilitates multi-agent collaboration, establishing language as a unifying bridge for autonomous
task-solving among LLM agents.

The paper is filed under Software Engineering (cs.SE), Computation and Language (cs.CL) and
Multiagent Systems (cs.MA). It was first submitted on 16 July 2023 and last revised on 5 June 2024
as version 5, carries the arXiv-issued DOI 10.48550/arXiv.2307.07924, and was accepted to ACL 2024.
The code and data are stated to be available at <https://github.com/OpenBMB/ChatDev>.

## Key Points

- The paper introduces ChatDev, a chat-powered software development framework whose specialized agents are driven by large language models and contribute to the design, coding and testing phases.
- Its stated motivation is that giving each waterfall-model phase its own uniquely designed deep learning model produces technical inconsistencies across phases, which the authors say results in a fragmented and ineffective development process.
- Agents are guided in what to communicate via a chat chain, and in how to communicate via communicative dehallucination — the paper's two named mechanisms, introduced in the abstract by their role rather than described in detail there.
- The authors report that natural language is advantageous for system design, while communicating in programming language proves helpful in debugging — a split between the two media rather than a preference for one.
- The paper's broader claim is that linguistic communication facilitates multi-agent collaboration, establishing language as a unifying bridge for autonomous task-solving among LLM agents; the abstract presents this as a paradigm-level conclusion rather than as a measured result.

## Notes

The contribution is framed against earlier work that used deep learning to improve specific phases
in a waterfall model — design, coding and testing taken one at a time. What ChatDev is offered as
replacing is therefore not any single phase's model but the arrangement of having one per phase, and
the claim the authors rest on is about consistency across phases rather than about performance
within one. The preprint went through five versions between July 2023 and June 2024.
