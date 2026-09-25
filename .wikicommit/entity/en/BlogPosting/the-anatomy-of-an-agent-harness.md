---
title: "The Anatomy of an Agent Harness"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, agent-architecture, context-engineering]
sources:
  - type: url
    url: 'https://blog.langchain.com/the-anatomy-of-an-agent-harness/'
    hash: sha256:71cffd4adc7b81b7dd5f981d26af2bebcee592b2751a882ea95bb833fa2d022e
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A LangChain blog post that defines an agent harness as everything in an agent that is not the model, and derives the harness components agents need by working backwards from what a model cannot do on its own."
  author: ["Vivek Trivedy"]
  datePublished: "2026-03-10"
  publisher: "LangChain"
---

In this post on LangChain's blog, Vivek Trivedy sets out a definition of an
[[DefinedTerm/agent-harness]] and uses it to explain why the components found in today's agents exist.
The definition is compressed into "Agent = Model + Harness" and "if you're not the model, you're the
harness": a harness is every piece of code, configuration and execution logic that is not the model
itself. On this account a raw model is not an agent; it becomes one when a harness gives it state, tool
execution, feedback loops and enforceable constraints. The author presents this as, in his opinion, the
cleanest way to draw the boundary, because it forces the design of systems around model intelligence.

The body works backwards from desired agent behaviour to harness features, following a pattern of
"behavior we want (or want to fix) → harness design to help the model achieve this". Its starting point
is that models take in data and output text, and out of the box cannot maintain durable state, execute
code, access realtime knowledge, or set up environments.

## Key Points

- A harness includes system prompts; tools, skills and MCP servers with their descriptions; bundled
  infrastructure such as a filesystem, sandbox and browser; orchestration logic such as subagent
  spawning, handoffs and model routing; and hooks or middleware for deterministic execution such as
  compaction, continuation and lint checks.
- The post calls the filesystem arguably the most foundational harness primitive: it gives agents a
  workspace, lets work be offloaded instead of held in context, and serves as a collaboration surface
  for multiple agents and humans. Git adds versioning to it.
- A bash tool lets models solve problems by writing and executing code instead of relying on a fixed
  set of pre-built tools; the post says code execution has become the default general-purpose strategy
  for autonomous problem solving.
- Sandboxes give agents safe, isolated places to run code that can be created on demand and torn down,
  and a harness is responsible for configuring their default tooling — runtimes, CLIs for git and
  testing, browsers — so that agents can observe and verify their own work.
- Without editing model weights, the only way to add knowledge is context injection: memory files such
  as [[DefinedTerm/agents-md]] loaded at start, and web search or MCP tools for information past the
  knowledge cutoff.
- Against [[DefinedTerm/context-rot]], the post describes harnesses as largely delivery mechanisms for
  good context engineering, naming [[DefinedTerm/compaction]], [[DefinedTerm/tool-call-offloading]] and
  Skills, which use [[DefinedTerm/progressive-disclosure]] to keep too many tools from being loaded at
  start.
- For long-horizon work it combines filesystems and git, the [[DefinedTerm/ralph-loop]], planning, and
  self-verification in which hooks run tests and loop failures back to the model.
- Agent products such as Claude Code and Codex are post-trained with their harnesses in the loop, which
  the post says can overfit a model to its harness; it argues that the best harness for a task is not
  necessarily the one the model was trained with, noting that on the Terminal Bench 2.0
  leaderboard Opus 4.6 in Claude Code scores far below Opus 4.6 in other harnesses.
- It expects some of what harnesses do today to be absorbed into models, but argues harness engineering
  will stay useful, as prompt engineering has.

## Context

The post is written from inside a harness vendor: it closes by naming LangChain's
[[SoftwareApplication/deep-agents]] library as where the team applies this work, and by listing open
problems it is exploring — orchestrating hundreds of agents on a shared codebase, agents that analyse
their own traces to fix harness-level failures, and harnesses that assemble tools and context
just-in-time. It also mentions an earlier LangChain result: moving its coding agent from the Top 30 to
the Top 5 on Terminal Bench 2.0 by changing only the harness. See also [[DefinedTerm/agent-harness]].
