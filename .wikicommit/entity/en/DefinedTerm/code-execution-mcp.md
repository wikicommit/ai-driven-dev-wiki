---
title: "Code Execution MCP"
type: "schema:DefinedTerm"
lang: en
aliases: ["CE-MCP"]
tags: [agents, mcp, security]
sources:
  - type: url
    url: https://arxiv.org/pdf/2602.15945
    hash: sha256:60c6e2cb0a71555099b80957589b805892374a300cde0b5fcf920cd270f4c095
  - type: url
    url: 'https://www.anthropic.com/engineering/code-execution-with-mcp'
    hash: sha256:100631c97989ce08b85030b756c939a2b9630de43337516938b86c6af9a4f494
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A context-decoupled MCP execution model in which an agent generates a single executable program that orchestrates tool calls within an isolated runtime, rather than invoking tools iteratively through the model's reasoning context."
---

Code Execution MCP (CE-MCP) is an execution model for [[DefinedTerm/model-context-protocol]] in
which the agent generates a single, self-contained executable program — encoding control flow,
tool invocations, and data transformations — that runs within an isolated runtime environment,
rather than invoking tools iteratively through natural-language exchanges. Only the final result of
that program re-enters the agent's context, so context consumption stays near-constant regardless
of task complexity or the size of the tool ecosystem. Major industry deployments, including
Anthropic's and Cloudflare's, have introduced this execution paradigm; CE-MCP extends the
traditional MCP rather than replacing it, exposing tools as callable functions within the execution
environment.

## Usage
Anthropic's own account of the approach, [[BlogPosting/code-execution-with-mcp]], motivates it with two
costs of direct tool calling at scale: most MCP clients load every tool definition into the context
window upfront, and every intermediate tool result passes through the model, sometimes twice. Its
remedy is to present MCP servers as code APIs that the agent calls from a code execution environment.
One implementation it describes generates a file tree with a TypeScript file per tool, which the
agent explores to read only the definitions it needs; in the post's example this cut token usage from
150,000 to 2,000. The same post lists further benefits — filtering large results in code before they
reach the model, running loops and conditionals in the execution environment, keeping sensitive data
out of the model's context by tokenizing it in the client, and persisting state and reusable code as
skills — and reports that Cloudflare published similar findings under the name "Code Mode". It also
cautions that running agent-generated code requires a secure execution environment with sandboxing,
resource limits and monitoring, operational overhead that direct tool calls avoid and that should be
weighed against the benefits.

An empirical comparison across 10 MCP-Bench servers and three GPT-4 model variants found that
CE-MCP consistently reduces token usage, execution time, and the number of interaction turns
compared to traditional MCP, while maintaining comparable task fulfillment, tool selection
accuracy, and parameter accuracy in most settings ([[ScholarlyArticle/from-tool-orchestration-to-code-execution]]).
The same study found CE-MCP best suited to complex, multi-tool tasks with structured, data-parallel
workflows — because it can parallelize tool usage and aggregate outcomes programmatically — while
traditional MCP retains an advantage on context-sensitive, heavily textual, or highly iterative
tasks that benefit from incremental reasoning and localized retries between turns.

That study also found that shifting from declarative tool invocation to model-generated code
execution fundamentally changes the system's security posture: because untrusted tool outputs and
exception messages are elevated into executable semantics, applying the MAESTRO threat-modeling
framework to CE-MCP identified sixteen attack classes across five execution phases — tool
discovery, code generation and planning, code execution, result return and validation, and runtime
impact — several of which the study validated as practically exploitable without any sandbox
escape, including denial-of-service via an induced non-terminating regeneration loop and
unauthorized privilege escalation via a poisoned exception message. It proposed a three-stage
defense-in-depth architecture (pre-execution static validation and semantic gating, isolated and
monitored execution, and post-execution semantic gating) that blocked every attack it tested, while
noting the defenses were not evaluated against adversaries aware of them.

## Related Terms
- [[DefinedTerm/model-context-protocol]] — the protocol this execution model extends
- [[ScholarlyArticle/from-tool-orchestration-to-code-execution]] — source of the efficiency/security
  comparison above
- [[BlogPosting/code-execution-with-mcp]] — Anthropic's description of the approach and its benefits
- [[DefinedTerm/progressive-disclosure]] — loading tool definitions only when needed
