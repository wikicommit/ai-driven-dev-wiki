---
title: "Code execution with MCP: Building more efficient agents"
type: "schema:BlogPosting"
lang: en
tags: [mcp, context-engineering, tool-use]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/code-execution-with-mcp'
    hash: sha256:100631c97989ce08b85030b756c939a2b9630de43337516938b86c6af9a4f494
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An Anthropic engineering post arguing that agents connected to many MCP servers should call tools by writing code in an execution environment rather than through direct tool calls, so they load only the tool definitions they need and keep intermediate results out of the model's context."
  author: ["Adam Jones", "Conor Kelly"]
  datePublished: "2025-11-04"
  publisher: "[[Organization/anthropic]]"
---

The post begins from the success of the [[DefinedTerm/model-context-protocol]]: developers now routinely build agents with access to hundreds or thousands of tools across dozens of MCP servers. It argues that at that scale two common patterns make agents slower and more expensive. Most MCP clients load every tool definition into the context window upfront, so an agent connected to thousands of tools may process hundreds of thousands of tokens before reading a request; and every intermediate tool result passes through the model, so a document fetched by one tool and written by another flows through context twice.

Its proposed answer is to present MCP servers as code APIs rather than as direct tool calls, and let the agent write code that calls them inside a code execution environment — the approach this wiki records as [[DefinedTerm/code-execution-mcp]]. The agent can then load only the tools it needs and process data in the execution environment before passing a result back to the model.

## Key Points

- Tool definitions loaded upfront occupy context window space and increase response time and cost.
- Intermediate results that pass through the model cost tokens — the post's example of a two-hour sales meeting transcript is put at about 50,000 extra tokens — can exceed context limits, and make copying mistakes between tool calls more likely.
- One implementation generates a file tree of the connected servers, with one TypeScript file per tool wrapping the underlying MCP call; the agent discovers tools by listing the directory and reading only the files it needs.
- In the post's example, this reduced token usage from 150,000 to 2,000 tokens, which it describes as a 98.7% saving in time and cost.
- Cloudflare is reported to have published similar findings under the name "Code Mode"; the shared insight is that LLMs are adept at writing code and agents should use that strength to interact with MCP servers.
- Tool definitions can be read on demand as a form of [[DefinedTerm/progressive-disclosure]], or found through a `search_tools` tool whose detail-level parameter lets the agent choose how much of each definition to load.
- Large results can be filtered, aggregated or joined in code, so that the agent sees, for example, five rows of a 10,000-row spreadsheet rather than all of them.
- Loops, conditionals and error handling can run as code instead of as a chain of tool calls through the agent loop, which also saves "time to first token" latency.
- Intermediate results stay in the execution environment by default, and the harness can tokenize sensitive data such as personal information before it reaches the model and untokenize it when it is passed to another tool, so real values flow between systems without ever entering the model's context.
- Filesystem access lets agents persist state and save working code as reusable functions; adding a `SKILL.md` file to such functions ties them to the concept of [[DefinedTerm/agent-skills]].
- Code execution brings its own costs: running agent-generated code needs a secure execution environment with appropriate [[DefinedTerm/sandboxing]], resource limits and monitoring, and the post says these costs should be weighed against the benefits.

## Context

The post is written by Anthropic, the organization that launched MCP, and its figures come from its own illustrative example rather than a measured study. It frames the problems it addresses — context management, tool composition, state persistence — as having known solutions from software engineering that code execution applies to agents, and invites implementers to share their findings with the MCP community. Its concern with keeping the context window lean connects it to this wiki's coverage of [[DefinedTerm/context-engineering]].
