---
title: "Agent Framework"
type: "schema:DefinedTerm"
lang: en
tags: [agent-frameworks, agent-architecture]
sources:
  - type: url
    url: 'https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/'
    hash: sha256:dbbb531bd6a1b614e8c6537f3fe67ea744c2f9b7a8532abd9bfc3cd413ce1729
  - type: url
    url: 'https://blog.langchain.com/agent-middleware'
    hash: sha256:071e79d936c9e2d2b07b0eab257fff6823cbeb8a320c72649b9ca211b9cd7179
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A package for building LLM agents whose main value lies in its abstractions — a mental model of the world that makes it easier to start and gives developers a standard way to build. The term is used by LangChain to separate such packages from agent runtimes below them and agent harnesses above them."
---

An agent framework, in the classification [[BlogPosting/agent-frameworks-runtimes-and-harnesses]]
proposes, is a package for building with LLMs whose main value add is abstractions. Harrison Chase,
who wrote that post, describes those abstractions as representing a mental model of the world: ideally
they make it easier to get started, and they give developers a standard way to build applications, so
that onboarding and moving between projects is easier. He classifies most packages for building with
LLMs this way, naming [[SoftwareApplication/langchain]] as LangChain's own example alongside Vercel's
AI SDK, [[SoftwareApplication/crewai]], the [[SoftwareApplication/openai-agents-sdk]], Google's
[[SoftwareApplication/agent-development-kit]] and LlamaIndex.

## Usage

The term is defined by contrast with two neighbours in the same post. An
[[DefinedTerm/agent-runtime]] sits below a framework, supplying production infrastructure such as
durable execution, and can power one — LangChain 1.0 is built on LangGraph. An
[[DefinedTerm/agent-harness]] sits above, adding default prompts, opinionated tool-call handling,
planning tools and filesystem access on top of a framework. Chase stresses that the boundaries are
blurry and that no clear definition yet exists; [[SoftwareApplication/langgraph]], for example, is
called both a runtime and a framework.

The standing criticism of the category is also about abstractions. Chase records the complaint that
poorly made abstractions obscure how things work and do not give the flexibility advanced use cases
need. A second LangChain post, [[BlogPosting/agent-middleware]], states the same problem more
specifically: frameworks built around the core loop of a model, a prompt and a list of tools do not
give developers enough control over context engineering, so developers end up "graduating off of the abstraction"
for any non-trivial use case. That post's answer is to keep the loop and make it modifiable through
[[DefinedTerm/agent-middleware]].

## Related Terms

- [[DefinedTerm/agent-runtime]] — the lower-level infrastructure layer
- [[DefinedTerm/agent-harness]] — the higher-level, batteries-included layer
- [[DefinedTerm/agent-middleware]] — LangChain 1.0's abstraction for customizing a framework's agent loop
- [[DefinedTerm/context-engineering]] — the control the middleware post says frameworks fail to give
