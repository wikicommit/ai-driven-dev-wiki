---
title: "Code execution with MCP: Building more efficient agents"
type: "schema:TechArticle"
lang: en
tags: [mcp, context-engineering, agentic-coding]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/code-execution-with-mcp'
    hash: sha256:00595274b94dc84401f5d20a982fac4221bd6fef1a8b89c318ac7ad3122afaf8
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Anthropic engineering post of 4 November 2025 arguing that agents scale better by writing code against MCP servers than by calling their tools directly, and setting out an implementation in which each server's tools are exposed as files in a generated TypeScript tree."
  author: ["Adam Jones", "Conor Kelly"]
  datePublished: "2025-11-04"
  publisher: "[[Organization/anthropic]]"
---

"Code execution with MCP: Building more efficient agents" is an engineering post published under Anthropic's "Engineering at Anthropic" banner on 4 November 2025, written by Adam Jones and Conor Kelly. Its thesis is stated in its own standfirst: direct tool calls consume context for each definition and result, so agents scale better by writing code to call tools instead. It is a design guide rather than an argument about practice — it names two specific cost patterns, proposes a concrete file-tree implementation for [[DefinedTerm/model-context-protocol]] servers, enumerates the properties that fall out of it, and states the operational cost of adopting it.

The post opens by restating what MCP is for — one universal protocol in place of a custom integration per tool-and-agent pairing — and reports that since the November 2024 launch the community had built thousands of servers, that SDKs existed for all major programming languages, and that the industry had adopted MCP as the de-facto standard for connecting agents to tools and data. The problem it then addresses is a consequence of that success: developers routinely build agents with access to hundreds or thousands of tools across dozens of servers.

## Key Practices

- **Diagnose the two token sinks separately.** Tool definitions loaded upfront occupy context before a request is even read — at thousands of tools, hundreds of thousands of tokens. Intermediate results are the second sink: every result passes through the model, so in the post's Google Drive to Salesforce example a full meeting transcript flows through context twice, which for a two-hour meeting it puts at an additional 50,000 tokens, and larger documents may exceed the window entirely. It also notes that with large documents or complex data structures, models may be more likely to make mistakes when copying data between tool calls.
- **Expose servers as a generated file tree.** The implementation shown uses a `servers/` directory per server and one TypeScript file per tool, each exporting a typed function that forwards to `callMCPTool`. The example workflow then becomes ordinary import-and-call code.
- **Let the agent discover tools by exploring the filesystem**, listing the servers directory and reading only the tool files it needs — reported as taking the example from 150,000 tokens to 2,000, a 98.7% saving. As an alternative it suggests a `search_tools` tool with a detail-level parameter (name only, name and description, or full schema).
- **Filter and transform results in the execution environment** before returning anything, so an agent handling a 10,000-row sheet logs five rows rather than all of them.
- **Write control flow as code.** Loops, conditionals and error handling become familiar code rather than chained tool calls, which also removes model round-trips from if-statement evaluation and so cuts time-to-first-token latency.
- **Keep sensitive data out of context by default.** Intermediate results stay in the execution environment unless logged; for sensitive workloads the post describes the client intercepting and tokenizing PII (`[EMAIL_1]`, `[PHONE_1]`) before the model sees it and untokenizing on the way out, so real values move between two services without entering context — and notes this also allows deterministic rules about where data may flow.
- **Persist state and code.** Filesystem access lets an agent write intermediate results to files and resume, and save its own working code as reusable functions; adding a `SKILL.md` to such a function makes it a structured skill, which the post ties to [[DefinedTerm/agent-skills]] and describes as the agent evolving its own scaffolding over time.

## Scope & Caveats

The post is explicit that the pattern is not free: running agent-generated code requires a secure execution environment with sandboxing, resource limits and monitoring, and those infrastructure requirements add operational overhead and security considerations that direct tool calls avoid. It states that the benefits — reduced token costs, lower latency, improved tool composition — should be weighed against those implementation costs.

It also does not claim the idea as Anthropic's alone: it notes Cloudflare published similar findings, referring to code execution with MCP as "Code Mode", and says the core insight is the same. Its concluding framing is that the problems involved — context management, tool composition, state persistence — feel novel but have known solutions from software engineering, and that this approach applies those established patterns to agents. The examples throughout are hypothetical Google Drive and Salesforce servers rather than measurements from a deployed system, and the 98.7% figure is given for that one illustrative workflow.
