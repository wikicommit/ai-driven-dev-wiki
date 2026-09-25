---
title: "Tool search"
type: "schema:DefinedTerm"
lang: en
tags: [tool-use, agent-tooling, context-engineering]
sources:
  - type: url
    url: 'https://platform.openai.com/docs/guides/function-calling'
    hash: sha256:837fddfb4f47440271a02bb4e3bf476c552ccbfc1b962b602a0217dc5bf68f47
  - type: url
    url: 'https://www.anthropic.com/engineering/advanced-tool-use'
    hash: sha256:37cff587dcd276ffbe27f31fcfa6f7985ccacfd5d06270baf40025725a068a97
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A technique for giving a model access to a large set of tools without loading them all up front: some or all tools are deferred, and the model searches for the relevant ones, adds them to its context and then calls them."
---

Tool search is a way of giving a model access to a large ecosystem of tools without placing every tool
definition in its context from the start. Some or all tools are **deferred**; the model searches for the
tools relevant to the task, loads them into its context, and then uses them like any other tool. Both
OpenAI and Anthropic offer it as a platform feature — OpenAI as the `tool_search` tool in its
function-calling guide, Anthropic as the Tool Search Tool on the Claude Developer Platform — and in
both it is the answer offered when an application has many tools or large schemas.

## Usage

The motivation both vendors give is cost and accuracy. Tool definitions sit in the model's context, so
they count against the context limit and, in OpenAI's guide, are billed as input tokens; and both
connect a large set of available tools with lower accuracy. Deferring large or infrequently used parts
of the tool surface addresses both. The two implementations differ in their details.

### OpenAI `tool_search`

OpenAI's function-calling guide recommends keeping the functions available at the start of a turn few
for higher accuracy, and presents tool search as the way to do that while still exposing a large tool
surface. When tool search is in use, the model's output may contain tool-search call and output items
before a function call; once a function has been loaded it is handled like any other call, and
`tool_choice` constrains only the tools currently callable in that turn.

Tool search interacts with how tools are described. Where deferred tools are grouped into namespaces
(see [[DefinedTerm/tool-namespacing]]), the guide advises keeping the namespace description concise and
putting the detailed guidance in each function's description: the namespace helps the model decide what
to load, and the function description helps it use the loaded tool correctly. OpenAI states that only
`gpt-5.4` and later models support `tool_search`.

### Anthropic Tool Search Tool

In Anthropic's version, introduced in [[BlogPosting/introducing-advanced-tool-use]], tools are marked
`defer_loading: true` and Claude initially sees only the search tool plus any tools left undeferred;
when it searches, matching tools are returned as references and expanded into full definitions in its
context. An MCP server can be deferred as a whole while specific high-use tools stay loaded. The
platform provides regex-based and BM25-based search tools, and developers can implement their own,
for example with embeddings. Anthropic states that this does not break prompt caching, because deferred
tools are absent from the initial prompt.

Anthropic motivates it with context consumed by MCP tool definitions — about 55K tokens for its example
five-server setup — and with wrong tool selection and incorrect parameters as the most common failures.
It reports an 85% reduction in token use in its example and, in internal MCP evaluations with large
tool libraries, accuracy rising from 49% to 74% for Opus 4 and from 79.5% to 88.1% for Opus 4.5.

## When It Applies

The trade-off is an extra search step before a tool can be invoked. Anthropic recommends tool search
when tool definitions exceed about 10K tokens, when tool selection accuracy is a problem, for
MCP-powered systems with several servers, or when more than ten tools are available, and considers it
less beneficial for small tool libraries, tools used in every session, or compact definitions. Because
search matches against tool names and descriptions, it advises clear, descriptive definitions and
keeping the three to five most-used tools always loaded. Anthropic's performance figures come from its
own internal testing.

## Related Terms

- [[DefinedTerm/function-calling]]
- [[DefinedTerm/tool-namespacing]]
- [[DefinedTerm/virtual-tools]]
- [[DefinedTerm/embedding-guided-tool-routing]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/programmatic-tool-calling]]
- [[DefinedTerm/tool-use-examples]]
