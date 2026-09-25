---
title: "Codex as a platform: build on the open agent harness"
type: "schema:BlogPosting"
lang: en
tags: [agent-harness, harness-engineering, human-oversight, mcp, open-source]
sources:
  - type: url
    url: 'https://developers.openai.com/blog/codex-as-a-platform'
    hash: sha256:f11a770f50c28f9e474cc72c15c33a9564aeb6eb21371cbaf0a6c7929f2d1b62
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An OpenAI developer blog post arguing that the open-source harness behind the Codex app, CLI and IDE extension can be embedded in other products, so that an agent works inside software built around a specific job rather than in a general-purpose coding assistant."
  author: ["Nicolas Bonamy", "Derrick Choi"]
  datePublished: "2026-08-19"
  publisher: "[[Organization/openai]]"
---

This post argues that [[SoftwareApplication/openai-codex]] is more than the App, command-line interface and IDE extension most people know it through: all three are powered by the same open-source Codex harness, and that harness can be built into other software. Instead of asking every team to move its work into a general-purpose coding assistant, the post suggests bringing the agent into software designed around the actual job — an engineering workflow, an operations dashboard, a security investigation, a customer-support console, or an internal application for one team.

Its central claim is that the reusable part is the agent loop. A capable agent, it argues, needs more than a prompt and a model response: it has to understand a task, maintain context, inspect information, call tools, expose progress, handle failures, request human approval and return a useful result — and that surrounding execution system is the [[DefinedTerm/agent-harness]]. OpenAI presents the Codex harness as managing conversation state, streaming execution, using tools, enforcing configured sandbox and approval policies and carrying work across turns, and [[SoftwareApplication/codex-app-server]] as exposing those capabilities through a documented client protocol.

The post illustrates the idea with Relay, a sample operations application OpenAI built on Codex app-server, and closes by describing the opportunity as making existing dashboards, timelines, maps and records more capable rather than replacing them with a universal chat box.

## Key Points

- Harness design is presented as materially changing results; as its evidence the post points to a benchmark case in which retained reasoning and context compaction alone substantially raised a model's score while reducing its output tokens.
- The harness is said to help models gather context, reason through tasks, use tools, operate within configured boundaries, request approval and carry work forward.
- Because the harness is open source, the post argues developers can inspect the layer between their application and the model and adapt the integration to their product.
- The post names three things a host application controls: its interface (existing dashboards, editors, queues and approval flows rather than a generic chat window), the context and tools it exposes, including application-owned MCP services, and the operational boundaries — where the agent runs, what it can access, which actions need approval, and how results return to the system of record.
- The Codex CLI, app-server and official Codex SDK are published as open-source components; the post states that model access and managed services remain separate from that open-source layer.
- It distinguishes three integration layers: `codex exec` for a script, CI job or one-off background task that returns structured output; the Codex SDK for application code that starts, resumes or streams tasks; and Codex app-server when the agent is part of the product itself.
- In Relay, the user selects a shipment and clicks an action rather than writing a prompt; the application supplies context, Codex uses the application's MCP tools to fetch current data, and any consequential write — such as rebooking a shipment — requires human approval. Relay uses fictional seeded data.
- The post says the pattern is already showing up in public implementations, including IDE integrations and uses outside software engineering, and argues it applies equally to support, operations, security, sales and marketing teams, with the application providing context, tools and approvals while Codex powers the agent loop.

## Context

The post is OpenAI's own promotion of its product as a platform; the adoption examples it lists are linked to other announcements and are not detailed in the post itself. Its argument sits alongside other writing that treats the harness, rather than the model, as the main engineering surface for agents (see [[DefinedTerm/harness-engineering]]).
