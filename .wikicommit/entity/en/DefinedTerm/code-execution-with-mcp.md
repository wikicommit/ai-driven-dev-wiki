---
title: "code execution with MCP"
type: "schema:DefinedTerm"
lang: en
tags: [mcp, context-engineering, agentic-coding, terminology]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/code-execution-with-mcp'
    hash: sha256:00595274b94dc84401f5d20a982fac4221bd6fef1a8b89c318ac7ad3122afaf8
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A pattern in which Model Context Protocol servers are presented to an agent as code APIs it writes code against, rather than as tool definitions loaded into context and called directly. Anthropic reports it cutting one example workflow from 150,000 to 2,000 tokens; Cloudflare has published similar findings under the name \"Code Mode\"."
---

Code execution with MCP is a pattern for connecting an agent to [[DefinedTerm/model-context-protocol]] servers in which the servers are exposed as code APIs the agent writes code against, instead of as tool definitions loaded into the context window and invoked directly. Anthropic set the pattern out in [[TechArticle/code-execution-with-mcp]], framing it as a response to two costs that grow with the number of connected servers: tool definitions loaded upfront overload the context window, and every intermediate tool result has to pass through the model. Cloudflare has published similar findings, referring to the same approach as "Code Mode"; Anthropic summarises the shared insight as LLMs being adept at writing code, so developers should use that strength rather than fight it.

## Usage

The concrete implementation Anthropic describes generates a file tree of the available tools from the connected servers — a directory per server, a file per tool, each file a thin typed wrapper that forwards to the underlying MCP tool call. The agent then discovers capabilities by exploring the filesystem: listing the servers directory to see what is available, then reading only the specific tool files it needs for the task at hand. In the worked example — reading a meeting transcript out of Google Drive and attaching it to a Salesforce record — this is reported as reducing token usage from 150,000 tokens to 2,000, which Anthropic states as a time and cost saving of 98.7%.

Anthropic groups the benefits under five headings.

- **Progressive disclosure**: because models navigate filesystems well, tool definitions can be read on demand rather than all upfront. A `search_tools` tool is offered as the alternative, ideally with a detail-level parameter so the agent can ask for names only, names and descriptions, or full schemas.
- **Context-efficient tool results**: large results can be filtered and transformed in the execution environment before anything returns to the model, so an agent working with a 10,000-row spreadsheet can see five rows instead of ten thousand. The same applies to aggregations, joins across sources, and field extraction.
- **More powerful control flow**: loops, conditionals and error handling become ordinary code rather than chains of individual tool calls, which also saves time-to-first-token latency, since the execution environment evaluates an if-statement instead of the model having to.
- **Privacy-preserving operations**: intermediate results stay in the execution environment by default, so the model only sees what is explicitly logged or returned. Anthropic adds that for more sensitive workloads the harness can tokenize PII before it reaches the model and untokenize it via a client-side lookup when the data is passed on, so real values flow between two services without ever entering the model's context — and that this can be used to define deterministic rules about where data may flow.
- **State persistence and skills**: with filesystem access an agent can write intermediate results to files and resume later, and can persist its own working code as reusable functions. Anthropic connects this directly to [[DefinedTerm/agent-skills]], noting that adding a `SKILL.md` file to such saved functions turns them into a structured skill the model can reference — so the agent gradually builds a toolbox of higher-level capabilities and evolves its own scaffolding.

Anthropic is explicit about the cost side: running agent-generated code requires a secure execution environment with sandboxing, resource limits and monitoring, which adds operational overhead and security considerations that direct tool calls avoid, and it says the token, latency and composition benefits should be weighed against those implementation costs. Its closing framing is that the problems here — context management, tool composition, state persistence — feel novel but have known solutions from software engineering, and that this pattern applies those established patterns to agents.

## Related Terms

The protocol the pattern reshapes is [[DefinedTerm/model-context-protocol]]; the context-budget problem it addresses belongs to [[DefinedTerm/context-engineering]], and the reusable-function endpoint it arrives at is [[DefinedTerm/agent-skills]]. The sandboxed environment it depends on is part of the [[DefinedTerm/agent-execution-environment]].
