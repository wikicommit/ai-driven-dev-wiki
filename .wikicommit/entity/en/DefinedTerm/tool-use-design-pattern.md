---
title: "Tool use design pattern"
type: "schema:DefinedTerm"
lang: en
aliases: ["Tool Use Design Pattern", "Tool-based agents", "Function calling"]
tags: [agents, tool-use, llm, agent-architecture]
sources:
  - type: url
    url: 'https://docs.aws.amazon.com/prescriptive-guidance/latest/agentic-ai-patterns/tool-based-agents-for-calling-functions.html'
    hash: sha256:46cb27f189d12df845e9edb3ecdd3e7b7a520969c4e66f3af19753891f37e4ea
  - type: url
    url: 'https://microsoft.github.io/ai-agents-for-beginners/04-tool-use/'
    hash: sha256:71a0416f774296d3c63b62963e0d749c00171e54c528c1541b44d90949d22ab2
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A design pattern in which a language model is given machine-readable descriptions of callable functions, selects one and produces its arguments, and has the result fed back into its reasoning — extending an agent from producing language to taking actions against external systems."
---

The tool use design pattern gives a language model the ability to invoke external functions or
services rather than answering from language alone. The model is supplied with descriptions of the
tools available to it; it selects the one that fits the request, generates the arguments for the
call, and the resulting output is returned into its reasoning so that the final response reflects
what the call produced. AWS describes the pattern as the point at which
an agent shifts from understanding language to performing actions, enabling agents "to act rather
than just providing responses"; Microsoft's course frames tools as what widens an agent from a
limited set of actions to a broad range of them. The tool
interface is deliberately generic: it stands for any callable capability, from arithmetic through
database lookups to external APIs and cloud services.

## Usage

Two published accounts of the pattern are described here — a cloud vendor's architectural pattern
catalogue and a vendor-published teaching course — and they agree on the mechanism while differing
in what they emphasize around it.

**AWS Prescriptive Guidance** presents it as an architecture pattern named *tool-based agents for
calling functions*, and sets out a five-step control flow: the agent receives a natural-language
query; it searches internal metadata or a tool registry for available tools, schemas and
capabilities; the model receives the query together with tool metadata such as function names,
input types and descriptions, chooses the most relevant tool, constructs input arguments and
returns a structured function call; an agent shell or tool runner executes the selected function
and returns the result; and the model incorporates that result, directly or through an updated
prompt, into a natural-language answer. Its stated capabilities for the pattern are dynamic tool
selection based on task context, schema-based prompting against OpenAPI or JSON Schema, chaining
of tool outputs back into reasoning, and stateless or session-aware operation. The use cases it
names are virtual assistants with external data access, financial calculators and estimators,
API-based knowledge workers, and models invoking managed cloud services. That account closes by
placing the pattern as an important component of agentic AI in enterprise settings, particularly
when combined with declarative schemas, authorization frameworks and multi-agent systems.

**Microsoft's *AI Agents for Beginners*** course treats it as the *Tool Use Design Pattern* and
puts more weight on what implementing it requires. It names six building blocks: function or tool
schemas defining name, purpose, required parameters and expected outputs; function execution logic
governing how and when tools are invoked, which may involve planner modules or routing; a message
handling system managing the flow between user input, model responses, tool calls and tool
outputs; a tool integration framework connecting the agent to the tools themselves; error handling
and parameter validation; and state management tracking context and prior tool interactions across
turns. Its use cases are dynamic information retrieval, code execution and interpretation,
workflow automation, customer support, and content generation and editing.

That course also states the vocabulary directly: *function* and *tool* are often used
interchangeably, because functions — blocks of reusable code — are the tools agents use to carry
out tasks. Implementing function calling requires three things: a model that supports it, a schema
describing the available functions, and the code implementing each one. The mechanics it describes
are a two-call exchange — a schema and user request go to the model, which returns the name of the
selected function and its arguments rather than a final answer; the application executes that
function and returns its output; a second call then produces the response the user sees. The course
is explicit that a tool call, not the answer, is what comes back from the first call.

Microsoft's account adds a security consideration the AWS page does not raise: where a model
generates SQL dynamically, the risk of injection or destructive statements is real but is addressed
by configuring database permissions rather than by trusting the model — running the application
against a read-only role, and in enterprise settings against a read-only database or warehouse
populated from operational systems. It notes that running the application in a secure environment
strengthens this further.

The Microsoft course adds that function calling is at the heart of most agent tool use design but can
be challenging to implement from scratch, and points to agentic frameworks as the practical route,
demonstrating the pattern through [[SoftwareApplication/microsoft-agent-framework]], where a function becomes a tool through
a decorator and the framework serializes it into the schema sent to the model, and through
[[SoftwareApplication/microsoft-foundry-agent-service]], where tool calling is handled server-side
and tools are combined into a toolset.

## Related Terms

- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agentic-coding]]
- [[DefinedTerm/tool-poisoning]]
- [[DefinedTerm/two-channel-prompt-injection]]
