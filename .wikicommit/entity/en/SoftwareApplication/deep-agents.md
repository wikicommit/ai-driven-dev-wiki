---
title: "Deep Agents"
type: "schema:SoftwareApplication"
lang: en
aliases: ["DeepAgents"]
tags: [agent-harness, agent-frameworks, agents]
sources:
  - type: url
    url: 'https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/'
    hash: sha256:dbbb531bd6a1b614e8c6537f3fe67ea744c2f9b7a8532abd9bfc3cd413ce1729
  - type: url
    url: 'https://blog.langchain.com/improving-deep-agents-with-harness-engineering/'
    hash: sha256:7628e7920b4c219963d45c07cb27a6039a14ef5a60f3939b0ccb424dd7481ddd
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source package from LangChain that its makers classify as an agent harness: it builds on LangChain and adds default prompts, opinionated tool-call handling, planning tools and filesystem access, and is described as a general-purpose version of Claude Code."
  applicationCategory: "Agent harness"
  featureList: "Default prompts; opinionated handling of tool calls; tools for planning; access to a filesystem"
  author: "LangChain"
---

Deep Agents (written "DeepAgents" in the post this page draws on) is an open-source package maintained
by LangChain, which Harrison Chase in [[BlogPosting/agent-frameworks-runtimes-and-harnesses]]
describes as its newest project and an increasingly popular one. He classifies it as an
[[DefinedTerm/agent-harness]], distinguishing it from [[SoftwareApplication/langchain]], an
[[DefinedTerm/agent-framework]], and [[SoftwareApplication/langgraph]], an
[[DefinedTerm/agent-runtime]].

## Capabilities

On the post's account Deep Agents is higher level than an agent framework: it builds on top of
LangChain and adds default prompts, opinionated handling for tool calls, tools for planning, and access
to a filesystem, among other things. Chase's summary is that it is more than a framework — it comes
with batteries included.

The project also includes deepagents-cli, which LangChain calls its coding agent, and is available in
Python and JavaScript. In [[BlogPosting/improving-deep-agents-with-harness-engineering]] LangChain reports
improving deepagents-cli on Terminal Bench 2.0 by changing only its harness — its system prompt, tools and
[[DefinedTerm/agent-middleware]] — while keeping the model fixed. The middleware described there inject
the agent's working directory and available tools at start, detect repeated edits to the same file, and
remind the agent to verify its work against the task before exiting.

## Adoption & Ecosystem

LangChain has also described Deep Agents as a "general purpose version of Claude Code", referring to
[[SoftwareApplication/claude-code]]. The post sets it beside the [[SoftwareApplication/claude-agent-sdk]],
which it reads as Claude Code's own step toward being an agent harness; besides that SDK, Chase says he
did not think there were many other general-purpose agent harnesses at the time, while allowing that
all the coding CLIs could be argued to be agent harnesses in a way.
