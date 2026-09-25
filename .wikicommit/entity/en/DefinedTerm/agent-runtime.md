---
title: "Agent Runtime"
type: "schema:DefinedTerm"
lang: en
tags: [agent-frameworks, agent-architecture, agent-state]
sources:
  - type: url
    url: 'https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/'
    hash: sha256:dbbb531bd6a1b614e8c6537f3fe67ea744c2f9b7a8532abd9bfc3cd413ce1729
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Infrastructure for running LLM agents in production — above all durable execution, together with streaming, human-in-the-loop support and persistence within and across threads. The term is used by LangChain for the layer beneath agent frameworks, with LangGraph as its example."
---

An agent runtime, in the classification [[BlogPosting/agent-frameworks-runtimes-and-harnesses]]
proposes, is what running agents in production calls for: software providing infrastructure-level
considerations rather than abstractions for building. Harrison Chase, who wrote that post, names
durable execution as the main one, and puts support for streaming, [[DefinedTerm/human-in-the-loop]]
support, thread-level persistence and cross-thread persistence in the same category. LangChain's own
example is [[SoftwareApplication/langgraph]], which Chase says was built as a production-ready agent
runtime from scratch; the projects he considers closest to it are Temporal, Inngest and other durable
execution engines.

## Usage

The post places runtimes beneath [[DefinedTerm/agent-framework]]s: they are generally lower level and
can power a framework, as LangChain 1.0 is built on LangGraph to take advantage of the runtime it
provides. [[DefinedTerm/agent-harness]]es sit higher again, on top of a framework. Chase describes the
boundaries as blurry — LangGraph is probably best described as both a runtime and a framework — and
presents the classification as his own attempt at a definition rather than an established one.

## Related Terms

- [[DefinedTerm/agent-framework]] — the abstraction layer a runtime can power
- [[DefinedTerm/agent-harness]] — the batteries-included layer above a framework
- [[DefinedTerm/human-in-the-loop]] — one of the capabilities the post assigns to a runtime
