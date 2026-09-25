---
title: "Agent Client Protocol (ACP)"
type: "schema:DefinedTerm"
lang: en
aliases: ["ACP"]
tags: [agent-protocols, coding-agents, coding-tools]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/agent-acp-in-practise/'
    hash: sha256:2b6ec051410853e3f6c810e69eecfcbeea93b7ae55d070290144a335cdcc9ca7
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A standardized communication protocol defining how IDEs and editors interact with AI coding agents, in which the IDE runs the agent as a subprocess and sees and controls each of its tool calls. It is described by analogy with the Language Server Protocol as an LSP for AI agents."
---

The Agent Client Protocol (ACP) is a standardized communication protocol that defines the interaction
between an IDE or editor and an AI coding assistant. [[BlogPosting/acp-protocol-and-multiple-ai-coding-agents]]
describes it as something a reader familiar with the Language Server Protocol can think of as "the LSP
for AI agents", and gives its core design principle as letting the IDE fully control every step the
agent takes: every operation — reading a file, editing code, running a command — has to go through an
explicit tool call that is visible to, controllable by and auditable from the IDE.

## Usage

In the model that post describes, the IDE is the client and the agent runs as a server subprocess,
the two communicating over JSON-RPC 2.0 on standard input and output. A session begins with capability
negotiation, similar to LSP's initialization handshake. While the agent works, each step is pushed to
the IDE as it happens — the plan, the file being read, the code about to change — through
`session/update` notifications carrying plans, tool-call progress, thought chunks and message chunks.
When the agent needs to perform a sensitive operation such as modifying a file or running a command, it
must request permission from the IDE, which may approve automatically under a user-configured policy,
ask the user, or show a diff for review before applying it.

The same post lists session persistence and resumption, multiple agent modes (`ask`, `code`,
`architect`) and native support for [[DefinedTerm/model-context-protocol]] servers among its features.
It summarises the division of labour as ACP handling interaction between agent and IDE while MCP
extends the agent's reach to external systems, and it places ACP between MCP/Skills and
[[DefinedTerm/agent2agent-protocol]] in a three-layer model for governing enterprise AI platforms.

The problem it is presented as solving is the one LSP solved for languages: without a common standard,
every editor has to implement an integration for every assistant, and every assistant needs a plugin
for each editor, which raises integration cost, limits which editors an assistant supports, and leaves
enterprises unable to manage assistants' permissions, logs and usage policies in one place. The post
names Zed and JetBrains as editor vendors that set out to decouple coding assistants from particular
editors, and calls JetBrains one of the protocol's main promoters, citing its official ACP Agent
Registry for installing agents from inside the IDE and an `acp.json` file for configuring custom ones.
It reports that SDKs exist for mainstream languages, and describes its own team integrating ACP into
the coding tool AutoDev as both client and server with the official Kotlin and TypeScript SDKs.

The post also presents the protocol as a remedy for agents being a black box, arguing that without it
an enterprise cannot audit which sensitive files an agent accessed, users cannot see what it is doing,
the IDE cannot show progress, and failures cannot be traced back through the agent's operations.

## Related Terms

- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agent2agent-protocol]]
- [[DefinedTerm/lsp-for-ai]]
- [[DefinedTerm/agent-communication-protocol]]
