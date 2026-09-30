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
  - type: url
    url: 'https://developers.openai.com/api/docs/guides/tools-programmatic-tool-calling'
    hash: sha256:387e308af93bf5e395e63fc75ef5feab5991b415cfa035a3b416ed10b3b296ac
  - type: url
    url: 'https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/programmatic-tool-calling'
    hash: sha256:42547562a018e3bd7b2b1f333ad79a9b4e7816bd113c85e722cb90d2062d43ec
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

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

The term is used for two closely related things: a platform feature, offered under this name by
more than one model provider, and an approach evaluated in research. The two platform features below
are described side by side; neither is the reference the other departs from.

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

Anthropic's API documentation for the feature fills in the mechanics. It requires the code execution
tool at version `code_execution_20260120` or later. `allowed_callers` takes `["direct"]` (the default),
a code-execution version, or both, and the documentation advises choosing one per tool for clearer
guidance to Claude; it also states that the field steers how the tool is presented rather than blocking
direct invocation at the API level, so it must not be relied on as a security boundary. Opted-in tools
are exposed to Claude's code as async Python functions that take a single dict of arguments and return
the `tool_result` text as a string, so Claude can run them in parallel with `asyncio.gather`. When the
code calls a tool, execution pauses and the API returns a `tool_use` block whose `caller` field carries
the id of the code-execution run that made the call; the application answers every pending call in a
user message containing only `tool_result` blocks, passing the container ID and the same `tools` array
back, and the code resumes. The documentation states that a pending call times out after about four
minutes, raising a `TimeoutError` inside the code, and that idle containers are currently reclaimed
after about five minutes. Tool results from programmatic calls do not count toward input or output
token usage; only the final code-execution result and Claude's response do.

It lists several limits. Tools with `strict: true` are not supported, a programmatic call cannot be
forced through `tool_choice`, `disable_parallel_tool_use: true` is not supported, tools whose input
schema contains a recursive `$ref` cannot be opted in, and neither tools provided by an MCP connector
nor the computer use and browser use toolsets can be called programmatically. It also describes the
pattern as generalizable to one's own infrastructure, setting Anthropic's managed execution beside two
self-hosted alternatives: executing the model's code directly in the client, which it warns runs
untrusted code outside a sandbox, and a self-managed sandbox, which it describes as safe but complex to
build and maintain.

### OpenAI API feature

[[Organization/openai]]'s API documentation describes Programmatic Tool Calling as letting a model
write and run JavaScript that coordinates its tools: a program can call tools in parallel, use loops
and conditions, and keep intermediate results in the hosted runtime. OpenAI runs each generated
program in a fresh, isolated V8 runtime that supports top-level `await` but provides no Node.js,
package installation, direct network access, general-purpose filesystem, subprocess execution,
console or persistent state between executions; a program reaches external systems only through the
tools enabled in the request, and emits output with `text(...)` or `image(...)`.

In the Responses API the developer adds a `programmatic_tool_calling` hosted tool and sets
`allowed_callers` on each eligible tool — `["direct"]` (the default), `["programmatic"]`, or both — and
is advised to define an `output_schema` alongside a function's `parameters` so that generated code can
rely on the returned fields. Function, custom, MCP, `apply_patch`, local and hosted shell, and code
interpreter tools can be called from a program. The response carries a `program` item holding the
generated code, `function_call` items whose `caller` field names the program that made them, and a
`program_output` item with the program's result and a `completed` or `incomplete` status. The
application runs client-owned function calls and returns each result with its original `call_id` and
`caller`, and a program can pause more than once, so the application continues until a final message
arrives; the application never executes the generated JavaScript itself. In OpenAI's Agents API the
feature is enabled by default, running in the OpenAI-managed agent harness, which gives the agent an
`exec` tool and makes its existing tools available inside generated JavaScript; orchestrating a tool
from JavaScript does not change where that tool runs.

### Research usage

The term is also used in [[ScholarlyArticle/the-bitter-lesson-of-tool-calling]], which describes it as
extending the case for replacing JSON tool calls with executable code, a line of work that includes
[[DefinedTerm/codeact]]. In that paper's implementation, tools are exposed as typed Python stubs: the
system prompt embeds the source of a stub module whose functions correspond one-to-one with the
available function schemas, the model writes one script that imports the module and calls the
required functions, and the agent loop runs it in a shell subprocess and reads the results from its
output, with no further inference turn after the subprocess returns.

## When It Applies

All of the sources treat it as a trade-off rather than a replacement for conventional tool calling in
every case. Anthropic describes it as most beneficial for processing large datasets where only aggregates
are needed, workflows with three or more dependent tool calls, filtering or transforming results
before the model sees them, tasks where intermediate data should not influence the model's reasoning,
and parallel operations across many items; and as less beneficial for single-tool invocations, tasks
where the model should see and reason about every intermediate result, and quick lookups with small
responses. It recommends documenting tool return formats clearly so that the model can write correct
parsing code, and opting in tools that can run in parallel or are safe to retry. Its figures come from
its own internal testing.

OpenAI draws the line by the shape of the task: it recommends Programmatic Tool Calling when a stage
has predictable control flow and code can return a smaller structured result — several results to
filter, join, rank, deduplicate, aggregate or validate, or dependent calls whose later arguments code
can derive — and direct tool calling when one call is enough, when each result should inform the
model's next decision, and by default for writes, approval-sensitive actions and final citation or
native-artifact validation. Where both modes are available it advises assigning each to a specific
workflow stage rather than giving generic instructions, and defining one handoff between them. Its
tool-design advice is to return compact structured data, document return shapes and error behaviour,
make calls idempotent where possible, check arguments and permissions for every call even when a
hosted program makes it, and require application-level approval before high-impact actions whatever
the caller.

Anthropic's API documentation frames the choice as a trade of a small fixed overhead — container
startup and script generation — against savings on tool-result tokens and model round trips. It lists
as strong fits fan-out operations across many items, large tool results that can be filtered or
aggregated before reaching Claude, and agentic search and retrieval; and as weak fits strictly
sequential workflows where each call depends on Claude reasoning over the previous result, a few
calls with small responses, and tools that need immediate user feedback between calls. It reports
results from Anthropic's internal evaluations: on a 75-tool project-management agent benchmark, billed
input tokens fell by roughly 38% with no change in task accuracy; on τ²-bench, where each turn makes
one or two sequential tool calls, scores were unchanged and cost was roughly 8% higher; and across
production API traffic, requests carrying 10 to 49 tool definitions typically save 20% to 40% of
tokens. It also reports that on the agentic search benchmarks BrowseComp and DeepSearchQA, adding the
feature on top of basic search tools improved performance by an average of 11% while using 24% fewer
input tokens. Its advice where the fit is unclear is to measure billed input tokens with and without
`allowed_callers` on representative traffic before enabling it broadly.

The paper's argument is that for models that can already write executable code, emitting a JSON
object per call is a design choice rather than a necessity. It assumes an execution environment the
model's script can run in and a model able to produce valid multiline code: in the paper's
evaluation, three older OpenAI models wrote literal `\n` escape sequences instead of newlines and
fell well below their JSON baselines, while all five Anthropic models and the newest GPT-5.6
variants matched or exceeded theirs. Other costs it reports are a fixed system-prompt overhead that
makes it more expensive than JSON tool calling below roughly 26 parallel calls, and a tendency for
some models to answer aggregation questions from parametric knowledge without actually executing
the calls.

The evidence behind these accounts is limited, and the figures from Anthropic come from its own evaluations. OpenAI reports no measurements: it says the feature can reduce the amount
of intermediate tool output added to model context but that the effect depends on the task and tool
responses, and it advises starting from direct tool calling as a baseline and comparing both on
representative tasks, measuring correctness and evidence coverage alongside tokens, latency and cost.
Beyond that there are a vendor's internal measurements and one controlled comparison: a single study
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
