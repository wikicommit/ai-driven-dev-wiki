---
title: "Microsoft Agent Framework"
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
  description: "An open-source Microsoft framework for building AI agents, in which an ordinary function becomes a callable tool through a decorator and the framework generates the schema and manages the exchange between the model and the application's code."
  applicationCategory: "AI agent framework"
  featureList: "Decorator-based tool definition, automatic schema generation, model-to-code call handling, prebuilt File Search and Code Interpreter tools"
  author: "Microsoft"
---

Microsoft Agent Framework is an open-source framework for building AI agents. Its distinguishing
feature, as described in Microsoft's *AI Agents for Beginners* course, is how little ceremony it
requires to expose a function to a model: tools are defined as Python functions carrying a `@tool`
decorator, and the framework serializes the function and its parameters into the schema sent to the
model, then handles the back-and-forth between the model and the application's code. This is what the framework
contributes to a direct implementation of the [[DefinedTerm/tool-use-design-pattern]]: the schema is
generated rather than written by hand, and the exchange with the model is the framework's
responsibility rather than the application's.

## Capabilities

An existing function is converted into a tool by decorating it, with an approval mode specified on
the decorator. Agents are created from a chat client configured with a project endpoint, model
deployment and credential, and are given a name, instructions and the tools they may use; the agent
is then run against a natural-language request.

Beyond functions the developer writes, the framework provides access to prebuilt tools — File
Search and Code Interpreter are the two the course names — through its `FoundryChatClient`.

## Adoption & Ecosystem

The framework appears in the course as one of two Microsoft routes to implementing tool use, the
other being [[SoftwareApplication/microsoft-foundry-agent-service]]; the course provides worked
samples in both Python and .NET.
