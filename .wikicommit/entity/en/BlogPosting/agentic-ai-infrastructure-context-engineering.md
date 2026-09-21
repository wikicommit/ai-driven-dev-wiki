---
title: "Agentic AI基础设施实践经验系列（九）：Context Engineering 上下文工程"
type: "schema:BlogPosting"
lang: en
tags: [agents, context-window, aws, agent-frameworks]
sources:
  - type: url
    url: 'https://aws.amazon.com/cn/blogs/china/agentic-ai-infrastructure-practice-series-nine-context-engineering/'
    hash: sha256:1ea97ed3d4e23cb29114ffee329716c05e979b914a7a52d5b181bf258202267f
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The ninth post in AWS China's Agentic AI infrastructure series, presenting context engineering as a three-component discipline — retrieval and generation, processing, and management — and then setting out AWS's own three-layer agent stack as the way to build on it."
  author: ["李明洁", "富宸", "姬军翔"]
  datePublished: "2025-11-21"
  publisher: "Amazon Web Services"
---

This post sets out [[DefinedTerm/context-engineering]] as a response to a problem it frames quantitatively: moving from a chat application to an agent changes the scale of what has to be held in context, not just its content. Its worked example is a task an agent decomposes into ten subtasks, each requiring two tool calls, which the post counts as 41 new context records — one initial decomposition plus four per subtask. In a multi-agent system each agent carries that whole load and the total multiplies again.

From there the post defines context engineering against prompt engineering, and the contrast is the piece it is most explicit about: traditional prompt engineering takes a static string and cannot handle dynamic multi-source information such as live data, historical state or tool interfaces, so it optimizes how context is phrased for a single output. Context engineering instead treats context as a collection of dynamic structured components, managed through explicit memory and modular composition across the whole information lifecycle — acquisition, filtering, storage, retrieval and final assembly.

The second half is a vendor account rather than a general one. The post presents AWS's stack in three layers and claims the services correspond to context engineering's core elements: a foundation-model layer (Amazon Bedrock, for the Converse API's standardized context structure, Prompt Cache and native tool calling), an agent-framework layer ([[SoftwareApplication/strands-agents]], for conversation management, memory and tool integration), and an agent runtime layer ([[SoftwareApplication/amazon-bedrock-agentcore]], for deployment, Memory, Gateway, Identity and Observability). Each layer is presented with worked Python.

## Key Points

- The definition it works from — relayed as an understanding the industry has converged on in recent years, not offered as the authors' own — is that context engineering is a technical framework for optimizing a model's reasoning and decision-making by dynamically managing what enters its context window, aiming to fill the window precisely while reducing cost, and addressing the limitations of prompt engineering rather than extending it.
- It decomposes context engineering into three core components forming a dynamic iterative loop: context retrieval and generation, context processing, and context management — with context management acting as the hub that organizes, compresses and schedules information across the whole flow.
- Its account of what context is made of is input (system instructions, external knowledge retrieval, tool definitions, global state, user input), memory (long-term and short-term), and output (tool execution results and model-generated structured content).
- It names four challenges as the motivation: the physical limit of the context window, cost rising with token count, the need to persist user preferences across visits, and a hidden degradation in both speed and accuracy — citing "Lost in the Middle" as the mechanism by which an over-long context loses track of key information.
- It names a "context optimizer" as the component doing this work and is careful about its status: today, it says, this is mainly an engineering implementation, while a possible future evolution is a model-driven optimizer that would decide — from the current user input, the task goal and the model's state — whether to compress, which compression strategy to use, what to discard, what to store as memory, and when to backfill memory.
- On AgentCore Gateway it argues the notable mechanism is semantic tool search: retrieving the most relevant tool definitions dynamically rather than loading every tool into context, which the post says cuts token use and improves selection accuracy where many tools exist.
- The post does put cost figures behind its AWS layer, asserted rather than measured: cached tokens billed 90% below standard input tokens, an input-to-output ratio as high as 100:1 in agent tasks, and — for code assistants such as Claude Code in a stable agent workflow — a cache hit rate above 90% with overall inference cost reduced by 80%. No methodology or benchmark setup is given for any of them.

## Context

The post is one instalment of a numbered series on Agentic AI infrastructure and links back to earlier entries, so it assumes the surrounding series rather than standing wholly alone. Its general half draws explicitly on an external survey of context engineering for the evolutionary path from basic RAG to multi-agent and tool-integrated reasoning systems, and names a wide range of third-party frameworks — Mem0, Letta, MemOS, SCM, FlashRAG, ComposeRAG, Self-RAG, PlanRAG, GraphRAG, HippoRAG, GNN-RAG, SagaLLM — in surveying the field before turning to AWS's own services.

The authors' stated perspective is that context engineering is not merely a technical optimization but the foundational methodology for building sustainable, scalable AI applications, and that AWS's contribution is turning that theory into a deployable stack. That framing is the post's own, written by the vendor about the vendor.
