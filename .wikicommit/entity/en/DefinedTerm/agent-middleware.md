---
title: "Agent Middleware"
type: "schema:DefinedTerm"
lang: en
tags: [agent-frameworks, context-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://blog.langchain.com/agent-middleware'
    hash: sha256:071e79d936c9e2d2b07b0eab257fff6823cbeb8a320c72649b9ca211b9cd7179
  - type: url
    url: 'https://blog.langchain.com/improving-deep-agents-with-harness-engineering/'
    hash: sha256:7628e7920b4c219963d45c07cb27a6039a14ef5a60f3939b0ccb424dd7481ddd
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An agent abstraction introduced in LangChain 1.0 in which composable middleware units hook into a fixed model-and-tools loop — before the model call, after it, or by modifying a single model request — to control what the agent sends to the model and how the loop proceeds."
---

Agent middleware is the abstraction LangChain introduced in [[SoftwareApplication/langchain]] 1.0 for
customizing an agent without abandoning its standard loop. The core loop keeps its two parts, a model
node and a tool node; a middleware attaches to it through three hooks. `before_model` runs before model
calls and can update state or jump to other nodes; `after_model` runs after model calls with the same
powers; and `modify_model_request` runs before model calls and changes, for that request only, the
tools, prompt, message list, model, model settings, output format and tool choice. A middleware can also
contribute custom state schemas and tools. Several middleware can be given to one agent, and they run
the way middleware does in web servers — sequentially on the way into the model call, and in reverse
order on the way back.

## Usage

LangChain presents middleware in [[BlogPosting/agent-middleware]] as its answer to a problem shared by
[[DefinedTerm/agent-framework]]s: an abstraction built on the simple model-prompt-tools loop gives too
little control over [[DefinedTerm/context-engineering]], so developers leave it for custom code once a
use case becomes non-trivial. Its earlier fix had been to add parameters to the agent — dynamic prompts,
custom state, pre- and post-model hooks, per-call model selection — which the post says became numerous,
interdependent and hard to combine or package as reusable variants. Middleware repackages those
customization points as composable units instead.

The three implementations that shipped with the 1.0 alpha show the hooks in use:
[[DefinedTerm/human-in-the-loop]] review of tool calls through interrupts, using `after_model`;
summarization of messages once they pass a threshold, using `before_model`; and Anthropic prompt
caching tags added to messages, using `modify_model_request`. LangChain also states that middleware
lets it replicate agent architectures it had previously shipped as separate LangGraph agents —
supervisor, swarm, bigtool, deepagents and reflection — and that it will offer off-the-shelf and
community middleware. These are the vendor's own statements about its framework, made during the alpha.

A later LangChain post, [[BlogPosting/improving-deep-agents-with-harness-engineering]], uses middleware —
glossed there as LangChain's term for hooks around model and tool calls — as one of three harness knobs
alongside the system prompt and tools, and describes three middleware built for its coding agent. A
`LocalContextMiddleware` runs when the agent starts, mapping the working directory with its parent and
child directories and finding tools such as Python installations, so that this context is injected rather
than discovered. A `LoopDetectionMiddleware` tracks per-file edit counts through tool-call hooks and, after
a set number of edits to one file, adds context suggesting the agent reconsider its approach (see
[[DefinedTerm/doom-loop]]). A `PreCompletionChecklistMiddleware` intercepts the agent before it exits and
reminds it to run a verification pass against the task specification. The post presents this kind of
deterministic context injection as a complement to prompting.

## When It Applies

The pattern assumes an agent built on a standard framework loop that the developer wants to keep
while controlling what enters the model and how steps are sequenced; its alternative, on LangChain's
account, is leaving the framework for custom code. The risk it addresses is the one its predecessor
created — many interacting parameters that were hard to coordinate, combine or offer as off-the-shelf
variants. It is one vendor's
design, described in that vendor's announcement with no reported evaluation.

## Related Terms

- [[DefinedTerm/agent-framework]] — the kind of package whose loop middleware customizes
- [[DefinedTerm/context-engineering]] — the control middleware is meant to restore
- [[DefinedTerm/human-in-the-loop]] — one of the first middleware implementations
- [[DefinedTerm/doom-loop]] — the failure mode LangChain's loop-detection middleware targets
