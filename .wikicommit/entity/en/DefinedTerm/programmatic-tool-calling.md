---
title: "Programmatic tool calling"
type: "schema:DefinedTerm"
lang: en
tags: [tool-use, agents, agent-architecture]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.06370'
    hash: sha256:dec66d23f3c920237899e23a098559303cf1572e36040c7738b274d516b55dd4
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A tool-use paradigm in which tools are exposed to a language model as typed code stubs and the model invokes them by writing a script, which is executed and its results handled in a single agent turn instead of one structured JSON call per function."
---

Programmatic tool calling is a way for a language model agent to use tools in which the tools are
exposed as typed Python stubs that the model invokes through code, with execution and results
handled in a single agent turn. It is defined against native JSON tool calling, the standard
deployment pattern for tool-augmented models, in which the model emits one structured JSON object
per function call through a tool-calling API. Because the calls are ordinary code, a script can
chain them — computing one call's argument from another's result — or fan them out in a loop or an
`asyncio.gather` block, where JSON tool calling needs a further inference turn for each dependent
step and has to emit every parallel call as its own object in a single response.

## Usage

The term is used in [[ScholarlyArticle/the-bitter-lesson-of-tool-calling]], which describes it as
extending the case for replacing JSON tool calls with executable code, a line of work that includes
[[DefinedTerm/codeact]]. In that paper's implementation, the system prompt embeds the source of a
stub module whose functions correspond one-to-one with the available function schemas, the model
writes one script that imports the module and calls the required functions, and the agent loop runs
it in a shell subprocess and reads the results from its output, with no further inference turn
after the subprocess returns.

## When It Applies

The paper's argument is that for models that can already write executable code, emitting a JSON
object per call is a design choice rather than a necessity. It assumes an execution environment the
model's script can run in and a model able to produce valid multiline code: in the paper's
evaluation, three older OpenAI models wrote literal `\n` escape sequences instead of newlines and
fell well below their JSON baselines, while all five Anthropic models and the newest GPT-5.6
variants matched or exceeded theirs. Other costs it reports are a fixed system-prompt overhead that
makes it more expensive than JSON tool calling below roughly 26 parallel calls, and a tendency for
some models to answer aggregation questions from parametric knowledge without actually executing
the calls.

Its standing is that of an approach with one controlled comparison behind it: a single study of 14
models on a subset of [[Dataset/berkeley-function-calling-leaderboard]] v4 whose stubs echo their
arguments rather than calling real APIs, so it measures argument serialisation rather than
end-to-end tool use. On that evidence the paper finds it matching or exceeding JSON tool calling in
11 of 14 models, handling large parallel fan-out without the call-dropping threshold JSON tool
calling showed for Claude Sonnet 5, and staying stable when decoy schemas flood the context.

## Related Terms

- [[DefinedTerm/codeact]]
- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/agentic-tool-use]]
- [[DefinedTerm/context-rot]]
