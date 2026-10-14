---
title: "Function calling"
type: "schema:DefinedTerm"
lang: en
aliases: ["Tool calling", "Tool use design pattern", "Tool-based agents", "ツール利用デザインパターン"]
tags: [tool-use, agent-tooling, llm-api, agents, agent-architecture]
sources:
  - type: url
    url: 'https://platform.openai.com/docs/guides/function-calling'
    hash: sha256:33e313e8ef53f2cc87fbe55e08f0ea5a56700f9f25a58c86e79dd18a8adac2a0
  - type: url
    url: 'https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/how-tool-use-works'
    hash: sha256:09b206b0019d5f083146422256f13de76bbf7d52aa69dc09f4125dd542b626a8
  - type: url
    url: 'https://simonwillison.net/2023/Jun/13/function-calling/'
    hash: sha256:e586b3ef6e21a9825daf98ac133095de870d331bdf427672a6c2e1b4bcbb726d
  - type: url
    url: 'https://simonwillison.net/2025/May/27/llm-tools/'
    hash: sha256:897bec73f778aa6be11624201d969f7572e6c5d2ac80b9e64fdf62a5631aa0e5
  - type: url
    url: 'https://www.promptingguide.ai/agents/function-calling'
    hash: sha256:5ea7116ae7f1bdf8996a498ac5020c6475235d5868c1b114d1148753e14fc0bf
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
  - type: url
    url: 'https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-3-tool-use'
    hash: sha256:102825bd22956a3a1ad7b346c85fe7d13cfd7c98f9d6af78d46a4d428a52fd84
review_status: pending
generated_at: "2026-10-14"
generated_by: "claude-opus-5-5"
generated_with: "0.10.0"

properties:
  description: "A model capability, also called tool calling and described as the tool use design pattern of agentic systems, in which an application describes the tools a model may use and the model responds with a structured request to call one, which the application executes and returns to the model before it produces its final answer — extending an agent from producing language to taking actions against external systems."
---

Function calling, also known as tool calling, is the mechanism by which a language model interfaces
with external systems and data outside its training data. The application tells the model which
**tools** it has access to — in OpenAI's vocabulary, a function is a kind of tool defined by a JSON schema for its inputs — and
the model, when it judges that following a prompt needs one of them, responds with a **tool call**
naming the tool and its arguments instead of a final answer. The application executes the call, sends
the output back referencing that call (OpenAI's **tool call output**), and the model then answers or makes further calls.
OpenAI's API guide describes this as a multi-step conversation between the application and the model in
five steps: request with tools, receive a tool call, execute it on the application side, send the output
back, and receive a final response or more tool calls. Anthropic's conceptual guide to tool use in the
Claude API describes the same exchange as a contract: the application specifies which operations are
available and what shape their inputs and outputs take, the model decides when and how to call them, and
the model never executes anything on its own — it emits a structured request, the application's code (or
Anthropic's servers) runs the operation, and the result flows back into the conversation.

Described as a design pattern of agentic systems — the *tool use design pattern* — the same mechanism gives a language model the ability to invoke external functions or
services rather than answering from language alone. The model is supplied with descriptions of the
tools available to it; it selects the one that fits the request, generates the arguments for the
call, and the resulting output is returned into its reasoning so that the final response reflects
what the call produced. AWS describes the pattern as the point at which
an agent shifts from understanding language to performing actions, enabling agents "to act rather
than just providing responses"; Microsoft's course frames tools as what widens an agent from a
limited set of actions to a broad range of them. In AWS's account the tool
interface represents any callable capability, from arithmetic through
database lookups to external APIs and cloud services.

## Usage

### Vendor APIs

In OpenAI's API a function definition has a type, a name, a description of when and how to use it, a
JSON Schema for its parameters, and a `strict` flag. Beyond JSON-schema function tools, the guide
describes *custom tools*, which take and return free-form text and can have that input constrained by a
context-free grammar (in a Lark variant or as a regular expression), and built-in platform tools such as
web search, code execution and access to [[DefinedTerm/model-context-protocol]] servers. Related tools
can be grouped into namespaces (see [[DefinedTerm/tool-namespacing]]), and rarely used ones deferred
with [[DefinedTerm/tool-search]] so that they are loaded only when the model needs them.

In Anthropic's Claude API the model's request arrives as a `tool_use` block carrying the tool name and a
JSON object of arguments, and the application returns the output in a `tool_result` block on the next
request. Anthropic's guide says this makes the model behave less like a text generator and more like a
function the application calls, so that engineers used to classical APIs can integrate it like any
other typed interface — define the schema, handle the callback, return a result — the difference being
that the caller choosing which function to invoke is a language model reading the conversation. It
describes the canonical shape of the resulting loop as a `while` loop keyed on `stop_reason`: while the
response stops with `"tool_use"`, execute the requested tools and continue the conversation, and exit on
any other stop reason. The same guide sorts tools by where their code runs, which decides whether the
application has to drive that loop at all (see [[DefinedTerm/client-and-server-tools]]).

The OpenAI guide's recommendations for defining functions are to write clear names, parameter descriptions and
instructions, using the system prompt to say when (and when not) to use each function; to apply ordinary software-engineering practice,
such as using enums and object structure so invalid states cannot be expressed and checking whether a
human intern could use the function from the description alone; to keep arguments the application
already knows out of the model's hands and to merge functions that are always called in sequence; and to
keep the number of functions available at the start of a turn small, suggesting fewer than 20 as a soft
guide. It notes that function definitions are injected into the model's context, so they count against
the context limit and are billed as input tokens.

Several controls shape how calls are made. `tool_choice` lets the application leave the decision to the
model, require at least one call, force one specific function, restrict calls to an allowed subset, or
disable calls. A model may call several functions in one turn unless parallel calls are turned off.
*Strict mode* makes calls reliably conform to the schema by building on structured outputs, which
requires every object to forbid additional properties and every field to be marked required; OpenAI
recommends always enabling it. If `strict` is omitted, the guide says the default depends on the API: the
Responses API tries to normalize the schema into strict mode and falls back to non-strict, best-effort
calling when it cannot, while Chat Completions stays non-strict by default. Results are usually returned
as a string in whatever format the application chooses — or, for functions that produce images or files,
as an array of image or file objects — and a function with no return value should still report success
or failure.

### As an agentic design pattern

Six further published accounts describe the mechanism. Four of them present it as a design pattern — a
cloud vendor's architectural pattern catalogue, a vendor-published teaching course, a framework vendor's
engineering blog post, and a letter in an AI newsletter — and two describe how the vendors converged on
it: an independent practitioner's survey of the research and the vendor APIs, and a second framework
vendor's announcement of a cross-provider interface. They agree on the mechanism while differing in what
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
so that every available tool is visible in the application graph. It is also the only one of these six accounts
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
search engines and on having it retrieve from a large set of tools.

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
into "tool calling" that November (Lee, above, dates OpenAI's `tools` parameter itself to June 2023; the two accounts do not reconcile the dates), with Gemini, Mistral, Fireworks, Together, Groq, Cohere and Anthropic
following over the next months — each through a slightly different interface, OpenAI's, Anthropic's and
Gemini's among them incompatible with one another. Where Lee reads the vendors' schemas as essentially the
same, LangChain's response was to hide the remaining differences behind one interface: `bind_tools()` to
attach tool definitions to any tool-calling model, a `tool_calls` attribute returning each invocation as
a name, arguments and an id, and an agent constructor that works with any model implementing both. The
post also relates the pattern to structured output: its `with_structured_output()` is built on tool
calling for most models, always returning output in the given schema, whereas binding tools leaves the
model free to call one tool, several or none.

**A letter in DeepLearning.AI's *The Batch***, [[BlogPosting/agentic-design-patterns-part-3-tool-use]],
the third in a series on agentic design patterns, calls Tool Use a key design pattern of AI agentic
workflows, in which an LLM is given functions it can request to call for gathering information, taking
action or manipulating data. It describes the mechanism at the level of generated text: the model is
fine-tuned or prompted, perhaps with few-shot prompting, to emit a special string requesting a call —
to a search engine, or to a Python interpreter to evaluate an arithmetic expression it would be unlikely
to get right by generating the answer directly — and a post-processing step detects that string, calls
the function with the relevant parameters and passes the result back to the model as additional
context, the exact format of the string depending on the implementation. The letter also raises the
question of scale: in systems where the model has access to hundreds of tools, too many to put all of
them into its context, heuristics may pick the most relevant subset for the current step, which it
likens to the way retrieval augmented generation systems pick a subset of text. It notes that much
early tool-use work came from the computer vision community, because before large multimodal models
became widely available an LLM-based system could manipulate an image only by calling a function on
it, and it calls GPT-4's function calling capability a significant step toward a general-purpose
implementation.

### Designing tools for agents

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

The same page documents Claude's version of `tool_choice` (compare OpenAI's, above), which takes four
values — `auto`, in which the model decides whether to call a tool (the default when tools are
provided); `any`, in which it must call one of the provided tools; `tool`, in which it must call one
named tool; and `none`, in which it may not call tools (the default when none are provided). With
`any` or `tool` the API prefills the assistant turn to force a tool call, so the model emits no
natural-language explanation before it. Forced tool use is not available everywhere: the
documentation states that manual extended thinking rejects `any` and `tool`, and that Claude Opus 5.5,
Claude Fable 5.1 and Claude Mythos 5.1 return an error for them regardless of thinking settings,
pointing instead to `auto` combined with strict tool use, or to structured outputs when a response in
a fixed JSON shape is needed.

## In Agent Loops

DAIR.AI's Prompt Engineering Guide, in its page on function calling in AI agents, presents the mechanism
from the side of someone building and debugging an agent. It names tool calling and reasoning as the two
capabilities LLM-based agents rely on, and describes the flow as: the user's query arrives; the system
message, tool definitions and user message are assembled into the context; the model decides whether a tool
is needed and, if so, outputs which tool to call with what parameters; the developer's code executes it; the
result comes back as the *observation*; and the observation is passed back with all prior messages so the
model can respond. The guide calls tool definitions — a name, a description of what the tool does and when
to use it, and typed parameters — arguably the most critical component, since they are the only way the
model knows what tools exist, and notes that they are part of the context on every call and so cost tokens
and latency. It frames the agent as a repeated cycle of action, environment response, observation and
decision, in which each observation is added to the context for the next step (compare
[[DefinedTerm/plan-act-observe-loop]]).

For debugging, the guide recommends inspecting the intermediate steps — which tools were called, with what
arguments, what each returned and how many tokens each step used — as workflow tools such as n8n can expose,
and getting as close to the raw API calls as possible. It lists incorrect tool selection, bad arguments,
missing guidance in the tool definition and misinterpreted observations as common failure causes. Its
recommendations for tool definitions, which it says come from practical experience building agents, are to
write specific descriptions that say when to use a tool, to repeat guidance on when to use which tool in the
system prompt, to constrain parameters with enums and examples, and to have tools return informative error
messages that help the agent recover.

## When It Applies

Anthropic's guide also states when tool use fits: when a task needs something the model cannot do from text
alone — actions with side effects such as sending an email or writing a file, fresh or external data
such as current prices or the contents of a database, structured output of a guaranteed shape, and calls
into existing systems such as internal APIs or filesystems. It offers a rule of thumb: an application
that writes a regular expression to extract a decision from model output should have made that decision
a tool call. It also states when tool use does not fit: when the model can answer from training alone
(summarization, translation, general-knowledge questions), when the interaction is one-shot question and
answer with nothing to execute, and when the latency of at least one extra round trip per call would
outweigh a trivial task. These criteria are one vendor's guidance in its own documentation.

## Introduction and Early Reception

A link post by Simon Willison dated 13 June 2023 records OpenAI announcing function calling that day,
among other API updates, for GPT-3.5 and GPT-4. As that post describes it, a developer sends a JSON
schema defining one or more functions, and the model returns a blob of JSON describing a function it
wants called, if it determines that one should be; the developer's code executes the function and
passes the result back to the model so that execution continues. Willison characterised this as
effectively an implementation of the [[DefinedTerm/react-prompting]] pattern, with models that have
been fine-tuned to execute it. He also noted that OpenAI's announcement acknowledged the risk of
[[DefinedTerm/prompt-injection]], though not by name, quoting its advice that developers can protect
their applications by only consuming information from trusted tools and by including user
confirmation steps before actions with real-world impact, such as sending an email, posting online or
making a purchase.

Writing in May 2025, in [[BlogPosting/large-language-models-can-run-tools-in-your-terminal-with-llm-0-26]],
Willison describes the same mechanism as having become, in his view, the single most effective way to
extend what language models can do, and as a simple trick: the model is told which tools it can use,
outputs special syntax requesting one — JSON, XML or `tool_name(arguments)`, which he says does not
matter — and stops; the caller's code parses that output, runs the tool and starts a new prompt with
the result. By then, according to that post, it worked with almost every model, most of which were
specifically trained for tool use, and there were leaderboards such as the Berkeley Function-Calling
Leaderboard tracking which models did it best. He writes that all the big model vendors — OpenAI,
Anthropic, Google, Mistral and Meta — have a version of it built into their APIs, called either tool
usage or function calling, and that it is the same underlying pattern; that local runtimes had it
too, with Ollama having added tool support and the llama.cpp server supporting it; and that a year
earlier he had not felt model tool support was mature enough to design an abstraction over it, whereas
there was now a very definite consensus among vendors on how it should work. He built that
abstraction into his own [[SoftwareApplication/llm]] tool.

## Related Terms

- [[DefinedTerm/agentic-tool-use]]
- [[DefinedTerm/tool-namespacing]]
- [[DefinedTerm/tool-search]]
- [[DefinedTerm/programmatic-tool-calling]]
- [[DefinedTerm/client-and-server-tools]]
- [[DefinedTerm/react-prompting]] — the pattern one early commentator described function calling as implementing
- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agentic-coding]]
- [[DefinedTerm/tool-poisoning]]
- [[DefinedTerm/two-channel-prompt-injection]]
- [[SoftwareApplication/burr]]
- [[BlogPosting/agentic-design-pattern-tool-calling]]
- [[BlogPosting/tool-calling-with-langchain]]
- [[BlogPosting/agentic-design-patterns-part-3-tool-use]]
- [[DefinedTerm/structured-tool]]
