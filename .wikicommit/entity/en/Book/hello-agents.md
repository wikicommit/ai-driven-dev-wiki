---
title: "Hello-Agents"
type: "schema:Book"
lang: en
tags: [agent-architecture, tutorial, open-educational-resource, multi-agent]
sources:
  - type: url
    url: 'https://github.com/datawhalechina/hello-agents'
    hash: sha256:f563f9594d0c841186d363ed9550ff208dcbcc40524a6e257e7a6771aec097ed
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A free, open-source Chinese-language tutorial on building AI agents from scratch, published by the Datawhale community in sixteen chapters across five parts. Its stated aim is to move a reader from being a user of large language models to a builder of agent systems, by way of implementing classic agent paradigms by hand and then a framework of their own."
  author: ["Sizhou Chen", "Tao Sun", "Shufan Jiang", "Peilin Huang", "Xinmin Zeng", "Hao Hu", "Xinzhong Zhu"]
  genre: "Technical tutorial"
---

Hello-Agents is an open-source tutorial on building AI agents, published in Chinese by the
Datawhale community under the title 《从零开始构建智能体》 and cited in English as *Hello-Agents:
Building an AI Agent from Scratch*. It is distributed free through the project's repository, an
online reading site and downloadable PDF releases, and is licensed CC BY-NC-SA 4.0.

The premise the introduction states is that if 2024 was the year of competing foundation models,
2025 opened the "year of the Agent" — the technical focus shifting from training larger base models
to building more capable agent applications — while systematic, practice-heavy tutorials remained
extremely scarce. The project positions itself against that gap.

Its scope is narrowed by a distinction the introduction draws between two kinds of agent building.
One is the software-engineering kind, exemplified by Dify, Coze and n8n, which it characterizes as
process-driven software development with the LLM acting as a data-processing backend. The other is
the AI-native kind, genuinely driven by the model. The tutorial states that it is about the second,
and describes its aim as taking the reader through the framework surface to the core principles,
architecture and classic paradigms, and finally to building their own multi-agent application.

## Contents

The book runs to sixteen chapters in five parts, and the repository marks all of them complete.
Part one covers agents and language model foundations: what an agent is, its types and paradigms; a
history running from symbolic AI to LLM-driven agents; and a chapter on Transformers, prompting,
the major LLMs and their limits. Part two is the hands-on core — implementing ReAct, Plan-and-Solve
and Reflection by hand, then working with low-code platforms (Coze, Dify, n8n), then mainstream
frameworks (AutoGen, AgentScope, LangGraph), and finally building an agent framework from zero.
Part three extends into memory and retrieval, [[DefinedTerm/context-engineering]], inter-agent
communication protocols including [[DefinedTerm/model-context-protocol]], A2A and ANP, Agentic RL
from SFT through GRPO, and agent performance evaluation. Part four is three integrated projects: a
travel assistant, an automated deep-research agent, and a simulated "cyber town" of agents modelling
social dynamics. Part five is a capstone in which the reader builds a complete multi-agent
application of their own.

Alongside the main text the repository carries a community-contributed *Extra-Chapter* series —
interview questions for agent roles, a supplement on context engineering, a Dify walkthrough, a
comparison of [[DefinedTerm/agent-skills]] with MCP, GUI and Web agent primers, guidance on writing
a good Skill, a collection of practical pitfalls from agent application development, and a chapter
on agent self-evolution.

The later parts are worked through a self-built framework the project calls HelloAgents, described
as built from scratch on OpenAI's native API and since updated to v1.0.0; part three states that it
uses that framework from part two rather than a third-party one.

## Characters & Publication

The book is a Datawhale community project, described by the repository as entirely open-source and
free: it is distributed through GitHub, an online reading site with a separate mirror for readers
in China, and PDF releases. The project notes that the PDFs carry a Datawhale watermark, added to deter resellers
from repackaging the free material.

The citation the repository supplies gives the year as 2025 and names seven contributors ahead of
"all Hello-Agents contributors". The repository's own acknowledgements describe the roles behind
those names — a project lead responsible for the full text, two co-initiators who contributed a
chapter and the exercises respectively, several chapter contributors, and an academic advisor — and
credit a further set of named contributors for the Extra-Chapter material. The repository's
forward-looking list names a follow-up work on training agents from scratch, alongside video
courses and further development of the HelloAgents framework.
