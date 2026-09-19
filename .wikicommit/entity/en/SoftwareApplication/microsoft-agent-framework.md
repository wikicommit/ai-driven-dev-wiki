---
title: "Microsoft Agent Framework"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, tool-use, agent-architecture]
sources:
  - type: url
    url: 'https://microsoft.github.io/ai-agents-for-beginners/04-tool-use/'
    hash: sha256:71a0416f774296d3c63b62963e0d749c00171e54c528c1541b44d90949d22ab2
  - type: url
    url: 'https://github.com/microsoft/agent-framework/blob/main/docs/decisions/0024-prompt-injection-defense.md'
    hash: sha256:51eb7a8188be72cbaed8c44f9f3fb847df2aaacf057d21f16ab59e9312c5d6d9
  - type: url
    url: 'https://learn.microsoft.com/en-us/agent-framework/workflows/human-in-the-loop'
    hash: sha256:c8d4c0ec859c61f78664fbc60f846dfd583f0efa4b93d0d0c42cffa2dcdce9f8
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source Microsoft framework for building AI agents, in which an ordinary function becomes a callable tool through a decorator and the framework generates the schema and manages the exchange between the model and the application's code."
  applicationCategory: "AI agent framework"
  featureList: "Decorator-based tool definition, automatic schema generation, model-to-code call handling, prebuilt File Search and Code Interpreter tools, a FunctionMiddleware pipeline, workflows built from executors and edges, typed request/response ports that pause a workflow for external input, tool approval in agent orchestrations, checkpoints that preserve pending requests"
  author: "Microsoft"
---

Microsoft Agent Framework is an open-source framework for building AI agents. Its distinguishing
feature, as described in Microsoft's *AI Agents for Beginners* course, is how little ceremony it
requires to expose a function to a model: tools are defined as Python functions carrying a `@tool`
decorator, and the framework serializes the function and its parameters into the schema sent to the
model, then handles the back-and-forth between the model and the application's code. This is what the framework
contributes to a direct implementation of the [[DefinedTerm/tool-use-design-pattern]]: the schema is
generated rather than written by hand, and the exchange with the model is the framework's
responsibility rather than the application's.

## Capabilities

An existing function is converted into a tool by decorating it, with an approval mode specified on
the decorator. Agents are created from a chat client configured with a project endpoint, model
deployment and credential, and are given a name, instructions and the tools they may use; the agent
is then run against a natural-language request.

Beyond functions the developer writes, the framework provides access to prebuilt tools — File
Search and Code Interpreter are the two the course names — through its `FoundryChatClient`.

Above individual agents the framework has a workflow system, in which units of work called
executors are wired together with edges through a builder. Microsoft's documentation describes
[[DefinedTerm/human-in-the-loop]] in that system as a consequence of a more general capability
rather than a feature of its own: an executor can send a request out of the workflow and wait for
the answer, which covers a human operator as one case of an external system among others. The
channel for this is a typed request port. When a request reaches it the workflow pauses and emits
an event carrying the request's details; an external system subscribes to those events, produces a
response, and hands it back, and the framework routes it to the executor that asked. The same
mechanism is offered in the framework's C#, Python and Go surfaces, with Python letting an executor
issue the request directly and register a response handler whose type annotations the framework
matches incoming responses against.

Tool approval reuses that machinery rather than adding another. Where agents run under one of the
prebuilt orchestrations, a tool marked as needing approval pauses the workflow and emits the same
event, differing only in that the payload is an approval request rather than a request type the
developer defined. The documentation is explicit about the limits of this: sequential, concurrent
and group-chat orchestrations do not stop for free-form user input on their own, so a workflow that
needs a conversation between steps has to pair them with a request port in a custom workflow. The
handoff orchestration is the exception, being interactive by default — when an agent answers
without handing off to another agent, control returns to the user for the next input.

Waiting also survives being checkpointed. Pending requests are stored as part of a checkpoint's
state and re-emitted when it is restored, and a run can be resumed from a checkpoint with the
responses supplied in the same call, so [[DefinedTerm/checkpoint-and-resume]] and an outstanding
approval do not have to be handled as separate concerns.

## Adoption & Ecosystem

The project also develops in the open through architecture decision records kept in its repository,
which is where a second source describes parts of the framework not covered by the course.

The record read here, ADR-0024, proposes [[DefinedTerm/fides]] (Flow Integrity Deterministic
Enforcement System), a label-based information-flow-control defence against
[[DefinedTerm/prompt-injection]]; it carries the status *proposed* rather than accepted. It also
shows how those records relate to one another, naming two earlier ones as its own lineage: an
agent-filtering-middleware record it says established the middleware patterns it builds on, and a
user-approval record it says it references for the human-in-the-loop pattern. Neither of those
records was read here, so what stands above is how ADR-0024 describes them.

What that record incidentally documents about the framework itself is its extension surface. There
is a `FunctionMiddleware` base class through which behaviour can be inserted around tool calls, and
the record's stated reason for its choice is that the option it picked was the only one giving
deterministic, formally verifiable guarantees while integrating non-invasively with that existing
pipeline and staying backwards compatible. Labels and similar metadata can be attached to content through an
`additional_properties` field without schema changes, and a `SerializationMixin` persists them.

Remote MCP connections belong to the proposal rather than to that existing surface: the design
would secure a connection made by tool or by URL by mapping MCP `ToolAnnotations` such as
`readOnlyHint` and `openWorldHint` onto its own labels, and by reading a server's `_meta.ifc`
result metadata (see [[DefinedTerm/model-context-protocol]]).

The framework appears in the course as one of two Microsoft routes to implementing tool use, the
other being [[SoftwareApplication/microsoft-foundry-agent-service]]; the course provides worked
samples in both Python and .NET.
