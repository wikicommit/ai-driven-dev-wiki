---
title: "LangGraph"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-architecture, context-engineering, open-source]
sources:
  - type: url
    url: 'https://www.langchain.com/blog/context-engineering-for-agents'
    hash: sha256:07e9475327ca11aeabb710cea3b419188e2ca4380d3cf4fd055291761f52fb8f
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A low-level agent orchestration framework built around an explicit state object and a graph of nodes, designed so that developers control what context is written, selected, compressed, and isolated at each step."
  applicationCategory: "Agent orchestration framework"
  author: "LangChain"
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

LangGraph is an agent framework from LangChain, described by its maintainers as low-level orchestration: a developer lays out an agent as a set of nodes, defines the logic within each, and defines a state object passed between them. In [[BlogPosting/context-engineering]] the team argues this structure is what makes deliberate [[DefinedTerm/context-engineering]] possible — because state is explicit and accessible at every step, the developer decides what reaches the model on each turn rather than accepting whatever has accumulated.

## Overview

The framework's central abstraction is the **state object**, which carries a schema whose fields can be written to and selectively exposed. One field, typically `messages`, is shown to the model each turn while other fields hold information the model does not see until it is needed — which the maintainers present as a form of context isolation comparable to running tool calls in a sandbox.

Memory is split by scope. Thread-scoped short-term memory uses checkpointing to persist agent state across every step of a run, which the post describes as usable directly as a scratchpad. Long-term memory persists across many sessions and can hold either small sets of files, such as a user profile or rules, or larger collections of memories; LangMem provides higher-level abstractions over it.

## Features

- **State schema with per-node access** — fetch and write state inside any node, giving fine-grained control over what is presented to the model at each step.
- **Checkpointing** for short-term memory, and a separate long-term memory store supporting file-style retrieval and embedding-based semantic search over a memory collection.
- **Built-in summarization and trimming utilities** for a message-list state, plus the ability to add summarization nodes at chosen points or inside a tool-calling node to compress specific tool outputs. See [[DefinedTerm/compaction]].
- **LangGraph Bigtool**, a library applying semantic search over tool descriptions to select the most relevant tools from a large collection.
- **Sandbox support** for isolating tool-call context from the model, with example integrations for E2B and Pyodide.
- **Multi-agent building blocks**, including supervisor and swarm libraries. See [[DefinedTerm/multi-agent-orchestration]].

The maintainers pair it with LangSmith for tracing, observability, and evaluation, on the argument that context engineering needs a way to see token usage and a way to test whether a change helped before it is worth doing.

## History

The sources ingested here do not cover LangGraph's release history. The context engineering post describing it dates from 2 July 2025.
