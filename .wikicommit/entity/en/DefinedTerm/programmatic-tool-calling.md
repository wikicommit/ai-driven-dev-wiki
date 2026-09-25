---
title: "Programmatic tool calling"
type: "schema:DefinedTerm"
lang: en
tags: [tool-use, agents, agent-architecture]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.06370'
    hash: sha256:dec66d23f3c920237899e23a098559303cf1572e36040c7738b274d516b55dd4
  - type: url
    url: 'https://www.anthropic.com/engineering/advanced-tool-use'
    hash: sha256:37cff587dcd276ffbe27f31fcfa6f7985ccacfd5d06270baf40025725a068a97
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A tool-use approach in which a language model invokes tools by writing code that calls them, so that several calls, their chaining and the processing of their results happen in one executed script rather than through one model-emitted structured call per function."
---

Programmatic tool calling is a way for a language model agent to use tools in which the model writes
code that calls the tools, rather than emitting one structured call per function and receiving each
result back in turn. It is defined against conventional tool calling: in native JSON tool calling, the
standard deployment pattern for tool-augmented models, the model emits one structured JSON object per
function call through a tool-calling API, and each dependent step needs a further inference turn.
Because the calls are ordinary code, a script can chain them — computing one call's argument from
another's result — or fan them out in a loop or an `asyncio.gather` block, and can filter or aggregate
their results before anything is returned to the model.

## Usage

The term is used for two closely related things: a platform feature and an approach evaluated in
research.

### Claude Developer Platform feature

[[Organization/anthropic]] introduced Programmatic Tool Calling as a beta feature of the Claude
Developer Platform in [[BlogPosting/introducing-advanced-tool-use]]. A developer opts tools in with an
`allowed_callers` field alongside the code-execution tool, and the API exposes them to Claude as Python
functions. Claude writes orchestration code that runs in a sandboxed code-execution environment; each
time the code calls a tool, the developer receives a tool request carrying a `caller` field and
returns the result, which is processed by the script rather than by the model, and only the script's
final output enters Claude's context. Anthropic's motivation is two problems it attributes to
conventional tool calling: context pollution from intermediate results, and the inference overhead of
one model pass per call followed by synthesis in natural language. It reports average token use on
complex research tasks falling from 43,588 to 27,297, a 37% reduction, fewer inference passes when
many calls run in one code block, and accuracy gains on internal knowledge retrieval (25.6% to 28.5%)
and GIA benchmarks (46.5% to 51.2%), and it states that Claude for Excel uses the feature to read and
modify spreadsheets with thousands of rows.

### Research usage

The term is also used in [[ScholarlyArticle/the-bitter-lesson-of-tool-calling]], which describes it as
extending the case for replacing JSON tool calls with executable code, a line of work that includes
[[DefinedTerm/codeact]]. In that paper's implementation, tools are exposed as typed Python stubs: the
system prompt embeds the source of a stub module whose functions correspond one-to-one with the
available function schemas, the model writes one script that imports the module and calls the
required functions, and the agent loop runs it in a shell subprocess and reads the results from its
output, with no further inference turn after the subprocess returns.

## When It Applies

Both sources treat it as a trade-off rather than a replacement for conventional tool calling in every
case. Anthropic describes it as most beneficial for processing large datasets where only aggregates
are needed, workflows with three or more dependent tool calls, filtering or transforming results
before the model sees them, tasks where intermediate data should not influence the model's reasoning,
and parallel operations across many items; and as less beneficial for single-tool invocations, tasks
where the model should see and reason about every intermediate result, and quick lookups with small
responses. It recommends documenting tool return formats clearly so that the model can write correct
parsing code, and opting in tools that can run in parallel or are safe to retry. Its figures come from
its own internal testing.

The paper's argument is that for models that can already write executable code, emitting a JSON
object per call is a design choice rather than a necessity. It assumes an execution environment the
model's script can run in and a model able to produce valid multiline code: in the paper's
evaluation, three older OpenAI models wrote literal `\n` escape sequences instead of newlines and
fell well below their JSON baselines, while all five Anthropic models and the newest GPT-5.6
variants matched or exceeded theirs. Other costs it reports are a fixed system-prompt overhead that
makes it more expensive than JSON tool calling below roughly 26 parallel calls, and a tendency for
some models to answer aggregation questions from parametric knowledge without actually executing
the calls.

Its evidence base is a vendor's internal measurements and one controlled comparison: a single study
of 14 models on a subset of [[Dataset/berkeley-function-calling-leaderboard]] v4 whose stubs echo
their arguments rather than calling real APIs, so it measures argument serialisation rather than
end-to-end tool use. On that evidence the paper finds it matching or exceeding JSON tool calling in
11 of 14 models, handling large parallel fan-out without the call-dropping threshold JSON tool
calling showed for Claude Sonnet 5, and staying stable when decoy schemas flood the context.

## Related Terms

- [[DefinedTerm/codeact]]
- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/agentic-tool-use]]
- [[DefinedTerm/context-rot]]
- [[DefinedTerm/tool-search]]
- [[DefinedTerm/tool-use-examples]]
- [[DefinedTerm/code-execution-mcp]]
