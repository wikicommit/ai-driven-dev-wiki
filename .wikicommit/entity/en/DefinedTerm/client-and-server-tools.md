---
title: "Client Tools and Server Tools"
type: "schema:DefinedTerm"
lang: en
sources:
  - type: url
    url: 'https://docs.claude.com/en/docs/agents-and-tools/tool-use/overview'
    hash: sha256:b7ea3ad279057166da87ad1e9b7af7e7b420910140fa982f5028a9e7c19e5271
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [tool-use, agent-architecture, llm]

properties:
  description: "The distinction, in Anthropic's Claude API, between tools whose code runs in the calling application and tools that run on the provider's own infrastructure — the primary axis along which tools differ."
---

Client tools and server tools are the two kinds of tool Anthropic's Claude API
distinguishes, separated by where the tool's code actually executes. Anthropic's
documentation states that tools differ primarily along this axis. Client tools run in the
calling application: the model responds with `stop_reason: "tool_use"` and one or more
`tool_use` blocks, the application's own code executes the operation, and it sends the
outcome back in a `tool_result` block. Server tools run on Anthropic's infrastructure, so
the caller sees the results directly without writing any handler — the documentation gives
web search as a minimal example, where the search runs on Anthropic's side and the cited
results come back in the same response.

## Usage

Anthropic's documentation groups the tools it offers into three categories along this
line — two of them client-side, one server-side. *Your own tools* are ones the developer defines by writing a schema, with the
application executing each call. *Anthropic-schema client tools* are ones for which
Anthropic publishes the schema and trains the model on it, while the application still
executes each call and returns the `tool_result` — among them the memory, bash, text
editor, computer use and browser use tools. *Server tools* need no handler code at all;
among them web search, web fetch, code execution, the advisor tool, the tool search tool
and the MCP connector.

The separation is not absolute in one documented case: the documentation notes that a
server tool's results are returned directly *unless* the model calls it in the same group
of parallel tool calls as one of the caller's client tools.

Where a tool runs also determines how it is billed. Anthropic states that client-side tools
are priced the same as any other API request, while server-side tools can incur additional
usage-based charges on top of tokens — its example is web search charging per search
performed.

## Related Terms

- [[DefinedTerm/tool-use-design-pattern]] — the general pattern this distinction refines
- [[DefinedTerm/computer-use]] — one of the Anthropic-schema client tools
- [[DefinedTerm/model-context-protocol]] — another route by which an agent reaches external tools
- [[DefinedTerm/code-execution-mcp]] — a related approach to running code on an agent's behalf
