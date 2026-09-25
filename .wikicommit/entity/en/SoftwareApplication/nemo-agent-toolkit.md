---
title: "NVIDIA NeMo Agent Toolkit"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-tooling, agent-frameworks, open-source]
sources:
  - type: url
    url: 'https://github.com/NVIDIA/NeMo-Agent-Toolkit'
    hash: sha256:d54f74713ca7f1585f0193c83cc0185f720f56daee1f1ff9182ccd60d91e4479
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source Python library from NVIDIA for connecting and optimizing teams of AI agents. It works alongside existing agent frameworks rather than replacing them, adding instrumentation for profiling, observability, evaluation and optimization."
  applicationCategory: "Agent instrumentation and optimization library"
  author: "[[Organization/nvidia]]"
---

NVIDIA NeMo Agent Toolkit is an open-source library from [[Organization/nvidia]], released under the Apache 2.0 license and installed from PyPI as `nvidia-nat`, for connecting and optimizing teams of AI agents. It is framework-agnostic: rather than replacing agent frameworks it works side by side with them — the README names [[SoftwareApplication/langchain]], LlamaIndex, [[SoftwareApplication/crewai]], Microsoft Semantic Kernel and Google's [[SoftwareApplication/agent-development-kit]], as well as custom enterprise frameworks and simple Python agents — and adds the instrumentation needed to observe, profile and optimize the agents built with them.

## Capabilities

Workflows are declared in a YAML configuration file that names the tools (functions), the LLMs and the workflow type, and are run with the `nat` command-line tool; the README's introductory example is a [[DefinedTerm/react-prompting]] agent given a Wikipedia search tool. Components are meant to be built once and reused, pre-built agents, tools and workflows can be customized, and a built-in chat interface lets developers interact with their agents, visualize output and debug workflows.

For understanding agents at runtime, the toolkit profiles whole workflows from the agent level down to individual tokens to find bottlenecks and analyze token efficiency, and provides observability for tracing execution flows in production, including native LangSmith tracing. For improving them, it offers an offline evaluation system, a hyper-parameter and prompt optimizer that searches for the best configuration and prompts, reinforcement-learning fine-tuning of LLMs for a specific agent, an experimental integration with NVIDIA Dynamo to improve agent performance at scale, and Agent Performance Primitives that accelerate graph-based frameworks such as LangChain, CrewAI and Agno with parallel execution, speculative branching and node-level priority routing.

On the protocol side, it can integrate [[DefinedTerm/model-context-protocol]] tools into agents or serve tools and agents as MCP servers, and it supports the [[DefinedTerm/agent2agent-protocol]] for building teams of distributed agents with authentication. It also provides skills that give AI coding agents task-specific guidance for building, evaluating, optimizing and observing its workflows, and a public plugin API against which third parties build integrations maintained outside the repository.

The `nat` tool includes opt-in telemetry. The first interactive command shows a one-time consent prompt that defaults to yes, while non-interactive contexts such as CI, cron jobs and piped scripts never send data unless it is explicitly enabled through an environment variable. Each event records the command name, its outcome, duration and exit code, the class name of any exception, and the Python version, and the README states that command arguments, workflow, function and model names, configuration contents, file paths and identifying information are never collected.

## Adoption & Ecosystem

The README credits Synopsys with Google ADK and Microsoft AutoGen framework support and the W&B Weave team with contributions to the evaluation and telemetry system, and names externally maintained plugins for Tavily, Redis and ATR built on its plugin API. Its stated roadmap includes a standalone evaluation harness, support for further programming languages, adding skills and sandboxes to existing agents, and an improved memory interface to support self-improving agents.
