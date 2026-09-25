---
title: "Client Tools and Server Tools"
type: "schema:DefinedTerm"
lang: en
sources:
  - type: url
    url: 'https://docs.claude.com/en/docs/agents-and-tools/tool-use/overview'
    hash: sha256:b7ea3ad279057166da87ad1e9b7af7e7b420910140fa982f5028a9e7c19e5271
  - type: url
    url: 'https://ai.google.dev/gemini-api/docs/tools'
    hash: sha256:56f15bec50e7429858d3e245833b8767f93534d45e9f989d56c4ec97baaa3a96
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"
tags: [tool-use, agent-architecture, llm]

properties:
  description: "The distinction, drawn by model providers' tool-use APIs, between tools whose code runs in the calling application and tools that run on the provider's own infrastructure. Anthropic's Claude API calls these client tools and server tools; Google's Gemini API draws the same line between custom tools and built-in tools."
---

Client tools and server tools are the two kinds of tool Anthropic's Claude API
distinguishes, separated by where the tool's code actually executes. Anthropic's
documentation states that tools differ primarily along this axis. Client tools run in the
calling application: the model responds with `stop_reason: "tool_use"` and one or more
`tool_use` blocks, the application's own code executes the operation, and it sends the
outcome back in a `tool_result` block. Server tools run on Anthropic's infrastructure, so
the caller sees the results directly without writing any handler — the documentation gives
web search as a minimal example, where the search runs on Anthropic's side and the cited
results come back in the same response. Google's [[SoftwareApplication/gemini-api]] draws the same
line under different names, as described below.

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

Google's Gemini API documentation divides its tools into *built-in* tools managed by Google and
*custom* tools managed by the developer, and describes a different execution flow for each. For
built-in tools — Google Search, Google Maps, URL Context, File Search and Code Execution — the entire
process happens within one API call: the model decides it needs a tool, executes it on Google's
servers and returns a final answer grounded in the results. For custom tools, defined through
function calling, the application handles execution: the model returns structured JSON calling a
function, always with a unique `id`; the application executes it and sends the result back with the
same `id`; and the model produces a final response or another call. Computer use falls on the
client side in both accounts: Anthropic lists it among its Anthropic-schema client tools, and
Google's documentation places its Computer Use tool, though listed among the built-in tools, in the
application-executed flow alongside custom tools.

The two accounts also each describe a case where the two kinds meet in one exchange. Anthropic's is
the parallel-call exception above. Google's is a preview feature for its Gemini 3 series models that
combines built-in and custom tools in a single turn, which its documentation calls tool context
circulation: the model runs the built-in tools and yields to the application when a client-side
function call is generated, and the application returns all parts of the model's response —
including encrypted thought signatures that preserve context — together with its own function
results, so the final answer is generated from the combined context.

## Related Terms

- [[DefinedTerm/tool-use-design-pattern]] — the general pattern this distinction refines
- [[DefinedTerm/computer-use]] — a tool both accounts place on the client side
- [[DefinedTerm/model-context-protocol]] — another route by which an agent reaches external tools
- [[DefinedTerm/code-execution-mcp]] — a related approach to running code on an agent's behalf
- [[SoftwareApplication/gemini-api]] — the Google API whose built-in and custom tools draw the same line
