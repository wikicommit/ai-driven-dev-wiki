---
title: "OpenAI Agents SDK"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, multi-agent, orchestration, guardrails, human-in-the-loop]
sources:
  - type: url
    url: 'https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf'
    hash: sha256:9d619ed7dd7cb94569658ca3de72615ef792761e6e4147e36c45edf2f945bbf9
  - type: url
    url: 'https://github.com/openai/openai-agents-js/blob/main/examples/agent-patterns/human-in-the-loop-stream.ts'
    hash: sha256:b539be2209796c131f666763bb7f0bc31443222962ec94c0ae76eb1d5d80a43e
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "OpenAI's code-first agent framework, in which an agent is declared with a name, instructions and a list of tools, run in a loop by a Runner until an exit condition is reached, and composed with other agents either as tools or through handoffs."
  applicationCategory: "Agent framework"
  featureList: "Agent objects defined by name, instructions and tools; Runner loop with exit conditions; agents exposed as tools; handoffs between agents; input guardrails with tripwires; per-tool approval gates that pause a run and resume it from the same run state"
  author: "[[Organization/openai]]"
---

The OpenAI Agents SDK is OpenAI's framework for building agents in code. It is the library
[[TechArticle/a-practical-guide-to-building-agents]] uses for every worked example, while stating
that the same concepts can be implemented with any preferred library or built directly from
scratch — so the guide presents it as one realisation of its patterns rather than a requirement
for them.

Its basic unit is an `Agent` declared with a name, a set of instructions and a list of tools. The
guide's opening example is a weather agent given a single `get_weather` tool, and functions are
turned into tools with a `@function_tool` decorator; built-in tools such as `WebSearchTool` can be
listed alongside the developer's own.

The SDK is also distributed as a JavaScript/TypeScript package, `@openai/agents`, whose repository
carries its own set of worked agent-pattern examples.

## Capabilities

Agents are started through a `Runner.run()` method that loops over the LLM until an exit condition
is met. The guide names two for this SDK specifically: a final-output tool is invoked, defined by
a specific output type, or the model returns a response with no tool calls at all. The guide
treats this loop as central to what makes something an agent rather than an SDK detail.

The SDK supports both multi-agent shapes the guide describes. For the
[[DefinedTerm/manager-pattern]], a specialist agent is converted into a tool with `as_tool(...)`,
given a tool name and description, and listed in a manager agent's `tools` array. For the
[[DefinedTerm/decentralized-pattern]], a handoff is itself a type of tool or function: agents are
listed in another agent's `handoffs` array, and calling a handoff immediately begins execution on
the agent handed off to while transferring the latest conversation state.

[[DefinedTerm/guardrails]] are described as first-class concepts in the SDK. A guardrail is
written as a function decorated with `@input_guardrail`, returning a `GuardrailFunctionOutput`
whose `tripwire_triggered` field decides whether to interrupt; guardrails are attached to an agent
through its `input_guardrails` list, and a triggered tripwire surfaces as a
`GuardrailTripwireTriggered` exception the caller can catch. The guide notes the SDK relies on
optimistic execution by default: the primary agent generates output while guardrails run
concurrently, raising an exception if a constraint is breached. The guide's own example wires an
LLM-based churn-detection agent in as such a guardrail.

The SDK also provides a [[DefinedTerm/human-in-the-loop]] approval gate at the level of an
individual tool call. An example in the `@openai/agents` repository attaches a `needsApproval`
predicate to a tool, and to an agent exposed as a tool through `asTool(...)`, and that predicate is
evaluated against the arguments the model generated for the call rather than against the tool as a
whole — so the same tool can run unattended for one input and require sign-off for another. When it
fires, the call is not executed: the run finishes carrying a list of `interruptions`, each of which
identifies the agent, the tool name and the generated arguments awaiting a decision. The host
application resolves each interruption by calling `approve` or `reject` on the run's state object
and then starting the agent again with that same state; the example repeats this until a run
completes with no interruptions left, so a resumed run can raise further approvals of its own. The
mechanism works with streaming runs — the example pipes the run's text stream to standard output
both before and after the approval step.

## Adoption & Ecosystem

The guide positions the SDK against what it calls declarative frameworks, which require every
branch, loop and conditional to be defined upfront as a graph of nodes and edges. It argues that
approach offers visual clarity but becomes cumbersome as workflows grow dynamic, often requiring a
specialized domain-specific language, and describes the Agents SDK as taking a more flexible,
code-first approach in which workflow logic is expressed with familiar programming constructs and
the graph need not be pre-defined. That comparison is the vendor's own framing of its product
against unnamed alternatives.
