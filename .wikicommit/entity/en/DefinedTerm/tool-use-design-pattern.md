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
  - type: url
    url: 'https://blog.dagworks.io/p/agentic-design-pattern-1-tool-calling'
    hash: sha256:f5276fdca09410e46b0e304c27f4f41294afee574a8aae025568b5534898ad22
  - type: url
    url: 'https://leehanchung.github.io/blogs/2024/05/09/tools-for-llms/'
    hash: sha256:8ef12294dde175a73b84aebfc72fd77dc2272d9cbae8e71e34c79396b3dddc5a
  - type: url
    url: 'https://www.anthropic.com/engineering/writing-tools-for-agents'
    hash: sha256:7541e4e46d675b2aed1175d9291d45d75f493ae908aea2afc77b29c615a324ea
  - type: url
    url: 'https://blog.langchain.com/tool-calling-with-langchain/'
    hash: sha256:272d889d15308a542b7029c3aae6528c22e13a794ef6e75763f377ff9e0b206a
  - type: url
    url: 'https://docs.claude.com/en/docs/agents-and-tools/tool-use/implement-tool-use'
    hash: sha256:b617f4377dcd4fcab5698ec8b5919a3fec12cf22b96c9f6c69bfb3d73b497ce6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

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

Five published accounts of the mechanism are described here — a cloud vendor's architectural pattern
catalogue, a vendor-published teaching course, a framework vendor's engineering blog post, an
independent practitioner's survey of the research and the vendor APIs, and a second framework vendor's
announcement of a cross-provider interface — and they agree on the mechanism while differing in what
they emphasize around it.

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

**A framework vendor's blog post** ([[BlogPosting/agentic-design-pattern-tool-calling]]) opens
with the vocabulary before any mechanism, judging the distinction between "tool",
"function" and "structured output" to be made more complex than it is. Its answer is that a tool and
a function are synonyms: for an agent built in code, the simplest way to do something on a user's
behalf is to call a function, and "tool" is the higher-level word for the same thing — which that
account offers as the reason the phrase is "tool call", merging "function call" with "tool use". It
observes that the industry has yet to align on one word, with major model providers naming the same
feature differently in their own APIs and documentation.

It separates structured outputs from the pattern on a different axis. What a model returns when it
picks a tool is JSON naming the tool and its arguments, and that JSON-producing behaviour can be
co-opted to get a fully structured response with no tool behind it at all — which that account
presents as a way to generalize beyond any one provider's tool-calling API. It also states the
reframing the pattern asks of the developer in plain terms: because current models are largely closed
off from the internet, the question to put to the model is not what the weather is but how to
determine it given that X, Y and Z can be done, the model's strength being to determine intent and say
what to do rather than to execute it.

On implementation, that account treats the pattern as a thin layer over whatever provider API supports
tool calling, though its worked example assumes one provider throughout: function signatures are read
by Python's `inspect` module and formatted into the type that provider expects, so that adding a tool
means adding a function. It recommends including a fallback
tool that lets the model answer from its own knowledge, and — modelling the flow as a state machine in
[[SoftwareApplication/burr]] — argues for one action per tool rather than a single dispatching action,
so that every available tool is visible in the application graph. It is also the only one of these accounts
to report the pattern misbehaving: the model was finicky about choosing a tool, sometimes declining to
choose one and sometimes losing track of the instructions, and reasonable behaviour came from prompt
engineering iterated against the framework's own debugging UI.

**An independent practitioner's post** by Han Lee approaches the pattern from two directions at
once: what earlier research proposed, and what the model vendors actually shipped. Its starting
premise is that language models suffer from a lack of access to current or proprietary
information, a lack of ability to reason or plan, and hallucination, and that other mechanisms are
therefore needed to provide tools to language models as agents. Lee summarises the research
lineage without dwelling on it: a pre-ChatGPT proposal to augment a language model with external
expert modules, neural ones being other language models and symbolic ones callables such as a
calculator, a currency converter or an API call, reached through a generated input adapter, contemporaneous efforts to give models web browsing and Python
interpreters, and post-ChatGPT work both on training a model to use tools such as calculators and
search engines and on having it retrieve from a large set of tools rather than a fixed few.

Where that post is most concrete is in comparing what the vendors converged on. It sets out
OpenAI's `tools` parameter, added to the Chat Completion API in June 2023, as the baseline: a list
of function specifications naming the function, describing it, and declaring its parameters as a
JSON Schema object with required fields, existing so the model can generate arguments that adhere
to the specification. It then reads the others as the same schema with different key names —
Google's Gemini Pro (announced November 2023) uses `functionDeclarations` and omits the tool
`type`; Anthropic's tool-calling beta (April 2024) renames `parameters` to `input_schema`; and
Cohere's (April 2024) renames it to `parameter_definitions`. LangChain added generic support
across models in the same month, exposing it either through a `@tool` decorator or by extending a
`BaseTool` class. Lee's point in laying them side by side is that the schema is essentially
settled, and that what actually determines quality is the descriptions: they are the prompts the
model uses to work out how to generate the best input parameters.

Its conclusion is a definition — a tool for a language model is a callable (a function, an API, a
SQL query) carrying a name, a description, and a clearly defined input JSON schema — and a
correction of a common way of speaking about it. On Lee's account the LLM does not use tools at
all: it only generates the input parameters, and it is the developer's responsibility to call the
tool with them and append the result to the conversation history for the model to produce the
final output. That restates, from outside any vendor, the same division of labour the AWS and
Microsoft accounts describe from inside one.

**LangChain's own announcement** of that cross-model support,
[[BlogPosting/tool-calling-with-langchain]], tells the same convergence from the framework side. It dates
native tool calling to OpenAI's "function calling", released roughly a year before the post and evolving
into "tool calling" that November, with Gemini, Mistral, Fireworks, Together, Groq, Cohere and Anthropic
following over the next months — each through a slightly different interface, OpenAI's, Anthropic's and
Gemini's among them incompatible with one another. Where Lee reads the vendors' schemas as essentially the
same, LangChain's response was to hide the remaining differences behind one interface: `bind_tools()` to
attach tool definitions to any tool-calling model, a `tool_calls` attribute returning each invocation as
a name, arguments and an id, and an agent constructor that works with any model implementing both. The
post also relates the pattern to structured output: its `with_structured_output()` is built on tool
calling for most models, always returning output in the given schema, whereas binding tools leaves the
model free to call one tool, several or none.

## Designing Tools for Agents

A further account, [[BlogPosting/writing-effective-tools-for-agents]], takes the mechanism above as
given and asks what follows for how tools should be designed. Its starting claim is that a tool is a
different kind of artifact from a function: conventional software establishes a contract between
deterministic systems, where the same call fetches the same thing the same way every time, whereas a
tool is a contract between a deterministic system and a non-deterministic agent, which may call the
tool, answer from general knowledge, ask a clarifying question first, or fail to grasp how to use it.
The stated consequence is that tools and MCP servers should not be written the way functions and APIs
are written for other developers or systems — they need designing for agents instead.

Four design positions follow from that. **Do not simply wrap existing endpoints**: more tools are said
not to always lead to better outcomes, and the reason given is that agents have different affordances from
traditional software — an agent has limited context, so a tool that returns every record forces it to
read through irrelevant ones, where the natural move is to skip to the relevant one. The recommendation
is a few thoughtful tools aimed at high-impact workflows, consolidating several underlying operations
where a workflow is frequently chained. **Namespace them** (see [[DefinedTerm/tool-namespacing]]) so an
agent with hundreds of tools can tell them apart. **Return only high-signal context**, preferring fields
that inform an agent's next action over low-level technical identifiers; the authors report that merely
resolving arbitrary alphanumeric UUIDs into semantically meaningful language, or even a 0-indexed ID
scheme, significantly improved Claude's precision on retrieval tasks by reducing hallucinations, and they
suggest a response-format parameter letting the agent choose concise or detailed output. **Bound the
response size**, with pagination, filtering and truncation on sensible defaults — the post states that
Claude Code restricts tool responses to 25,000 tokens by default — and treat truncation messages and
error text as places to steer the agent toward more token-efficient strategies rather than as opaque
codes.

That account converges with the independent practitioner survey above on which part matters most.
Where that survey concludes that the schema is essentially settled and the descriptions are what
determine quality, this post names prompt-engineering the tool descriptions and specs as one of the most
effective methods available, recommends writing them as one would brief a new hire — making implicit
context explicit — and reports Claude Sonnet 3.5 reaching state-of-the-art performance on
[[Dataset/swe-bench-verified]] after precise refinements to tool descriptions. Its method for getting
there is an evaluation loop rather than judgment: build evaluation tasks from realistic work, run them
as simple agentic loops, and read the resulting transcripts — a discipline the post reports applying to
Anthropic's own internal tools, with held-out test sets showing gains beyond expert implementations
written either by its researchers or by Claude.

Anthropic's own API documentation on defining tools sets out the declaration side of the same
advice for its Claude API. A user-defined tool is declared in the request's `tools` parameter with a
`name` (letters, digits, underscores and hyphens, up to 128 characters), a detailed plaintext
`description`, an `input_schema` given as a JSON Schema object, and optionally `input_examples` —
sample inputs that must validate against the schema, which the documentation recommends for tools
with nested objects or format-sensitive parameters and says add roughly 20–50 prompt tokens for a
simple example and 100–200 for a complex nested one. From the tool definitions, the tool
configuration and any user-supplied system prompt, the API constructs a special system prompt that
instructs the model to use the tools. Its best practices restate the positions above in a vendor's
reference documentation: it calls extremely detailed descriptions by far the most important factor in
tool performance and asks for at least three to four sentences per tool, covering what the tool does,
when it should and should not be used, what each parameter means and what the tool does not return;
it recommends consolidating related operations into one tool with an `action` parameter rather than
one tool per action, prefixing tool names with the service they belong to, and returning semantic,
stable identifiers and only the fields the model needs for its next step.

The same page documents a control the accounts above do not cover: `tool_choice`, which takes four
values — `auto`, in which the model decides whether to call a tool (the default when tools are
provided); `any`, in which it must call one of the provided tools; `tool`, in which it must call one
named tool; and `none`, in which it may not call tools (the default when none are provided). With
`any` or `tool` the API prefills the assistant turn to force a tool call, so the model emits no
natural-language explanation before it. Forced tool use is not available everywhere: the
documentation states that manual extended thinking rejects `any` and `tool`, and that Claude Opus 5.5,
Claude Fable 5.1 and Claude Mythos 5.1 return an error for them regardless of thinking settings,
pointing instead to `auto` combined with strict tool use, or to structured outputs when a response in
a fixed JSON shape is needed.

## Related Terms

- [[DefinedTerm/tool-namespacing]]
- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agentic-coding]]
- [[DefinedTerm/tool-poisoning]]
- [[DefinedTerm/two-channel-prompt-injection]]
- [[SoftwareApplication/burr]]
- [[BlogPosting/agentic-design-pattern-tool-calling]]
- [[BlogPosting/tool-calling-with-langchain]]
- [[DefinedTerm/structured-tool]]
