---
title: "Microsoft Foundry Agent Service"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, tool-use, agent-architecture]
sources:
  - type: url
    url: 'https://microsoft.github.io/ai-agents-for-beginners/04-tool-use/'
    hash: sha256:71a0416f774296d3c63b62963e0d749c00171e54c528c1541b44d90949d22ab2
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A fully managed Microsoft service for building and deploying AI agents, in which tool calling is executed server-side and conversation state is held in managed threads, so the developer neither parses tool calls nor stores conversation history themselves."
  applicationCategory: "Managed AI agent service"
  featureList: "Server-side automatic tool calling, managed conversation threads, toolsets combining custom and prebuilt tools, knowledge tools (Bing grounding, File Search, Azure AI Search), action tools (function calling, Code Interpreter, OpenAPI-defined tools, Azure Functions)"
  author: "Microsoft"
---

Microsoft Foundry Agent Service is a managed service for building, deploying and scaling AI agents
without managing the underlying compute and storage. Microsoft's *AI Agents for Beginners* course
presents it as the newer of two Microsoft routes to implementing the
[[DefinedTerm/tool-use-design-pattern]], and positions it for enterprise applications on the
grounds that it is fully managed and offers enterprise-grade security.

The course states three advantages over calling a model API directly: tool calling is automatic, so
the application does not parse a tool call, invoke the tool and handle the response itself, all of
which happens server-side; conversation state is managed through threads rather than by the
developer; and a set of tools is available out of the box for reaching common data sources.

## Capabilities

Tools are divided into two categories. **Knowledge tools** retrieve information — grounding with
Bing Search, File Search, and Azure AI Search. **Action tools** do something — function calling,
Code Interpreter, tools defined from an OpenAPI specification, and Azure Functions.

Tools are combined into a **toolset**, which may mix functions the developer supplies with prebuilt
ones; the model decides which to use for a given request. The course's worked example builds a
toolset from a custom SQLite query function and the Code Interpreter tool, then creates an agent
with a model, name, instructions and that toolset, so the model chooses between querying the data
and computing over it depending on what is asked. **Threads** hold the message history of a
particular conversation.

## Adoption & Ecosystem

The course illustrates the service through a sales-data scenario, in which a conversational agent
answers questions about an organization's sales figures by querying them and analysing the results.
It appears alongside [[SoftwareApplication/microsoft-agent-framework]] as the managed alternative
to running an agent framework yourself.
