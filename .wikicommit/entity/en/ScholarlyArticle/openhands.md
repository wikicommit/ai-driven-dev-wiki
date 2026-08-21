---
title: "OpenHands: An Open Platform for AI Software Developers as Generalist Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, agent-architecture, multi-agent, open-source]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2407.16741'
    hash: sha256:93aed96e187f2e30f86b5bb87cf1cad0852515081dc699763752bf89e6c8e93d
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The ICLR 2025 paper introducing OpenHands, a platform for building AI agents that interact with the world as a human developer does — by writing code, using a command line, and browsing the web — together with an evaluation across 15 benchmark tasks."
  datePublished: "2025"
  abstract: "Introduces OpenHands (formerly OpenDevin), a platform for developing AI agents that write code, interact with a command line, and browse the web, describing how it supports new agent implementations, sandboxed code execution, coordination between multiple agents, and incorporation of evaluation benchmarks."
  keywords: ["AI agents", "software engineering", "agent platform", "code execution", "benchmarks"]
---

"OpenHands: An Open Platform for AI Software Developers as Generalist Agents" is a conference paper published at ICLR 2025 by a large, multi-institution author group led by Xingyao Wang and Graham Neubig, introducing [[SoftwareApplication/openhands]] — formerly OpenDevin. Its design premise is stated as an argument about interfaces: software is the most powerful way humans currently interact with the world, so given the existing tooling around its development, use and deployment, it "provides the ideal interface for AI agents to interact with the world in complex ways".

## Key Findings

The platform's agent abstraction rests on a **state** structure whose key component is an **event stream**, a chronological collection of past actions and observations including the agent's own actions and user interactions. The state also carries auxiliary information such as the accumulated cost of LLM calls and metadata tracking multi-agent delegation.

The action space is deliberately small and programming-language-based. Drawing on CodeAct, `IPythonRunCellAction` and `CmdRunAction` let an agent execute arbitrary Python code and bash commands inside a sandboxed environment described as a securely isolated Linux operating system, while `BrowserInteractiveAction` drives a web browser through a domain-specific language. The authors argue these primitives cover most tasks performed by human software engineers and analysts, and that a language-based action space is "powerful and flexible enough to perform any task with tools in different forms" while remaining reliable and easy to maintain — with the added property that it is compatible with conventional tool-calling, since a user can define a tool as an ordinary Python function.

**AgentSkills** is the paper's answer to a maintenance problem it attributes to the agent-computer interface idea: creating, maintaining and distributing many specialized tools is a daunting engineering challenge, especially when they must work across different agent implementations. Its solution is a Python package of utility functions automatically imported into the agent's IPython environment, so defining a tool is defining a Python function. Its stated inclusion criteria are restrictive on purpose — a skill is added only when it is not readily achievable for an LLM to write the code directly, or when it involves calling an external model — with the authors giving the explicit counter-example that they do not re-teach an agent to use pandas to read a CSV. The skills described include file-editing utilities adapted from SWE-Agent and Aider, scrolling functions for viewing different parts of files, and multi-modal readers for extracting information from images and PDFs.

**Agent delegation** is handled by a dedicated `AgentDelegateAction` that lets one agent hand a subtask to another — the paper's example being the generalist CodeActAgent, which has limited web-browsing support, delegating to a specialized BrowsingAgent. Community-contributed agents live in an AgentHub, with CodeActAgent as the default generalist: at each step it can either converse in natural language to ask for clarification or confirmation, or execute code to perform the task.

On evaluation, the paper reports results across 15 benchmark tasks. On SWE-Bench Lite — a 300-instance canonical subset the authors default to for cost reasons, noting that running the complete 2,294-instance set would cost roughly $6,900 at a conservative $3 per instance — CodeActAgent v1.8 with claude-3.5-sonnet reached a 26% resolve rate, which the paper calls competitive with other open-source SWE specialists. All results are reported without the benchmark's "hint text". On HumanEvalFix the agent fixed 79.3% of bugs in the Python split, which the authors say is significantly better than all non-agentic approaches and almost double StarCoder2-15B; they note SWE-Agent's higher 87.7% but flag the comparison as uneven, since that evaluation gave the model a full successful demonstration trajectory while OpenHands was evaluated 0-shot.

## Context

The paper presents OpenHands as a community project rather than a research artifact alone: released under the permissive MIT license, spanning academia and industry, with more than 2,100 contributions from over 188 contributors at the time of writing. Its author list spans UIUC, CMU, Yale, UC Berkeley, Contextual AI, KAUST, ANU, HCMUT, Alibaba and All Hands AI.

Its comparative claims about other agent frameworks and benchmarks are its own, drawn from the benchmarks it had incorporated at the time, and the SWE-Bench Lite result is reported on a subset chosen for affordability rather than on the full benchmark.
