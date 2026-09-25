---
title: "Introducing advanced tool use on the Claude Developer Platform"
type: "schema:BlogPosting"
lang: en
tags: [tool-use, agent-tooling, context-engineering, mcp]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/advanced-tool-use'
    hash: sha256:37cff587dcd276ffbe27f31fcfa6f7985ccacfd5d06270baf40025725a068a97
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Anthropic's announcement of three beta tool-use features on the Claude Developer Platform — the Tool Search Tool, Programmatic Tool Calling and Tool Use Examples — each aimed at a different bottleneck in agents that work across large tool libraries: context spent on tool definitions, context and inference spent on intermediate results, and malformed tool calls."
  author: ["Bin Wu"]
  datePublished: "2025-11-24"
  publisher: "[[Organization/anthropic]]"
---

The post, on Anthropic's engineering blog, announces three beta features that let Claude discover,
learn and execute tools dynamically. It starts from a picture of agents working across hundreds or
thousands of tools — an IDE assistant spanning git, package managers, testing frameworks and
deployment pipelines, or an operations coordinator connected to many services and MCP servers at
once — and names three needs such agents have: discovering and loading tools on demand instead of
placing every definition in context upfront, calling tools from code instead of one inference pass
per call, and learning correct usage from examples rather than from schema definitions alone.

The three features answer those needs in turn: [[DefinedTerm/tool-search]] through the Tool Search
Tool, [[DefinedTerm/programmatic-tool-calling]], and [[DefinedTerm/tool-use-examples]]. For each the
post sets out the problem, how the feature works with API examples, Anthropic's internal
measurements, and when it is and is not worth the added overhead. It states that in internal testing
the features made possible things conventional tool-use patterns could not, citing Claude for Excel's
use of Programmatic Tool Calling to read and modify spreadsheets with thousands of rows.

## Key Points

- Tool definitions are presented as a large, growing cost: the post's example five-server MCP setup
  has 58 tools consuming about 55K tokens before a conversation starts, and it reports having seen
  tool definitions consume 134K tokens at Anthropic before optimization. It adds that the most common
  failures are wrong tool selection and incorrect parameters, especially between similarly named
  tools.
- The Tool Search Tool keeps tools marked `defer_loading: true` out of Claude's context until Claude
  searches for them; the post reports an 85% reduction in token use in its example and, on MCP
  evaluations with large tool libraries, accuracy rising from 49% to 74% for Opus 4 and from 79.5% to
  88.1% for Opus 4.5. It states that deferral does not break prompt caching, because deferred tools
  are not in the initial prompt.
- Traditional tool calling is said to cause context pollution from intermediate results and
  inference overhead, since every call needs a full model inference pass and Claude must synthesize
  results in natural language. Programmatic Tool Calling instead has Claude write Python that calls
  the tools, runs in a sandboxed code-execution environment and returns only its final output; the
  post reports average token use on complex research tasks falling from 43,588 to 27,297, a 37%
  reduction, and accuracy gains on internal knowledge retrieval and on GIA benchmarks.
- JSON Schema is argued to define what is structurally valid but not how a tool should be used —
  formats, ID conventions, when to fill nested structures and how parameters correlate. Tool Use
  Examples add sample calls to a tool definition, and the post reports accuracy on complex parameter
  handling improving from 72% to 90% in internal testing.
- Each feature is framed as a trade-off with its own "most beneficial" and "less beneficial"
  conditions, and the post recommends starting with the biggest bottleneck — context bloat from tool
  definitions, intermediate results polluting context, or parameter errors — before layering the
  others. It describes the three as complementary: search finds the right tools, programmatic calling
  executes them efficiently, and examples make invocation correct.
- Practical guidance includes writing clear, descriptive tool names and descriptions because search
  matches against them, keeping three to five of the most-used tools always loaded, documenting
  return formats so Claude can write correct parsing code, and keeping to one to five realistic,
  varied examples per tool focused on genuine ambiguity.

## Context

The post is a vendor's announcement of its own platform features, and all of its performance figures
come from Anthropic's internal testing. It presents the features as building on its earlier writing
on code execution with MCP ([[DefinedTerm/code-execution-mcp]]) and acknowledges inspiration from
elsewhere in the ecosystem, including Cloudflare's Code Mode. Its closing claim is that these
features move tool use from simple function calling ([[DefinedTerm/function-calling]]) toward
intelligent orchestration, as agents take on workflows spanning dozens of tools and large datasets.
