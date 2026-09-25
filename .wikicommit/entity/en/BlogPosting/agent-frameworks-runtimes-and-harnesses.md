---
title: "Agent Frameworks, Runtimes, and Harnesses- oh my!"
type: "schema:BlogPosting"
lang: en
tags: [agent-frameworks, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/'
    hash: sha256:dbbb531bd6a1b614e8c6537f3fe67ea744c2f9b7a8532abd9bfc3cd413ce1729
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A LangChain blog post by Harrison Chase proposing working definitions for three kinds of agent-building software — agent frameworks, agent runtimes and agent harnesses — using LangChain's own three open-source packages as the examples of each."
  author: ["Harrison Chase"]
  datePublished: "2025-10-25"
  publisher: "LangChain"
---

In this post Harrison Chase explains the terms he had started using for the open-source packages
LangChain maintains: [[SoftwareApplication/langchain]] is an [[DefinedTerm/agent-framework]],
[[SoftwareApplication/langgraph]] is an [[DefinedTerm/agent-runtime]], and
[[SoftwareApplication/deep-agents]] is an [[DefinedTerm/agent-harness]]. He observes that others were
using the same terms without a clear shared definition, and offers the post as an attempt to supply
one — while saying up front that murkiness and overlap remain and inviting feedback.

The post is short and deliberately provisional. Its significance is less any one definition than the
layering it proposes: a runtime supplies production infrastructure beneath a framework, and a harness
adds opinionated, batteries-included defaults above one.

## Key Points

- Most packages for building with LLMs are, on Chase's account, agent frameworks, whose main value is
  abstractions: a mental model that makes it easier to get started and gives developers a standard way
  to build and move between projects. He records the standing complaint against abstractions — done
  poorly, they obscure inner workings and lack flexibility for advanced use cases.
- He names Vercel's AI SDK, CrewAI, the OpenAI Agents SDK, Google ADK and LlamaIndex as other agent
  frameworks, and says LangChain 1.0's work went into abstractions for structured content blocks, the
  agent loop and middleware.
- An agent runtime, in the post's terms, supplies infrastructure-level considerations for running agents
  in production: chiefly durable execution, but also streaming, human-in-the-loop support, and
  thread-level and cross-thread persistence. He names Temporal, Inngest and other durable execution
  engines as the projects closest to LangGraph here.
- Runtimes are described as generally lower level than frameworks and able to power them; the post's
  example is that LangChain 1.0 is built on top of LangGraph.
- An agent harness sits higher than a framework: Deep Agents builds on LangChain and adds default
  prompts, opinionated handling of tool calls, planning tools and filesystem access — "batteries
  included".
- The post also describes Deep Agents as a "general purpose version of Claude Code", notes that Claude
  Code is itself moving toward being an agent harness through the Claude Agent SDK, and suggests that
  all coding CLIs could be argued to be agent harnesses of a kind.
- Chase states that he did not coin "agent harness", which he says he was only starting to see used
  more.
- The lines are called blurry: LangGraph is "probably best described as both a runtime and a
  framework".

## Context

The author presents this as a first attempt at mental models in an early space rather than a settled
taxonomy, and each category is illustrated with the author's own company's packages; the
classification is his proposal, not a consensus definition. The post includes a summary comparison of
when to use each kind of package as an image, which is not reproduced in its text.
