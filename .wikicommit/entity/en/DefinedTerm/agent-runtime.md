---
title: "Agent Runtime"
type: "schema:DefinedTerm"
lang: en
tags: [agent-frameworks, agent-architecture, agent-state]
sources:
  - type: url
    url: 'https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/'
    hash: sha256:dbbb531bd6a1b614e8c6537f3fe67ea744c2f9b7a8532abd9bfc3cd413ce1729
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/runtime/harness/'
    hash: sha256:82cf9e7387cf2117eac969bb6ccb6061e9f58fd5de7e0191c1baed3aae3a014b
review_status: pending
generated_at: "2026-10-14"
generated_by: "claude-opus-5-5"
generated_with: "0.10.0"

properties:
  description: "Infrastructure for running LLM agents in production. LangChain uses the term for the layer beneath agent frameworks that supplies durable execution, streaming, human-in-the-loop support and persistence, with LangGraph as its example; Jimmy Song uses it for the multi-agent operating platform above single-agent harnesses that handles scheduling, persistence and governance."
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

Jimmy Song's chapter on the [[DefinedTerm/agent-harness]] draws the boundary the other way up. There
the agent runtime is the layer above the harness: where a harness is the runtime substrate of one agent and
looks after that agent's execution quality, the agent runtime is an operating platform for many agents,
responsible for multiple sessions and tenants, scheduling, persistence, governance and the control plane, and
a single runtime can manage several harness instances. In the workload framing the chapter uses, the harness
is the execution layer of an agent workload and the runtime is its management layer; Song describes the two
as complementary, and their separation as what lets each evolve independently at its own scale.

## Related Terms

- [[DefinedTerm/agent-framework]] — the abstraction layer a runtime can power
- [[DefinedTerm/agent-harness]] — the batteries-included layer above a framework in LangChain's layering, and the single-agent layer beneath a runtime in Song's
- [[DefinedTerm/human-in-the-loop]] — one of the capabilities the post assigns to a runtime
