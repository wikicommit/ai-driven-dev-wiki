---
title: "Function calling using LLMs"
type: "schema:TechArticle"
lang: en
tags: [tool-use, agents, prompt-injection, mcp]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/function-call-LLM.html'
    hash: sha256:1c1dd75185abb251f131bc42253cf8f85504020b87557cd597a63c250f5362d4
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A May 2025 article by Kiran Prakash on martinfowler.com that explains LLM function calling by building a small shopping agent in Python, covering function schemas, restricting the agent's action space, prompt-injection guardrails, action classes, and how function calling relates to tool calling and the Model Context Protocol."
  author: ["Kiran Prakash"]
  publisher: "martinfowler.com"
  datePublished: "2025-05-06"
---

This article, published on martinfowler.com, is a worked introduction to function calling — the
capability described on this wiki under [[DefinedTerm/tool-use-design-pattern]] — for building
agents that interact with external systems. It defines function calling as letting an LLM analyse a
natural-language input, extract the user's intent, and generate structured output containing a
function name and the arguments needed to invoke it. The article stresses that the LLM does not
execute the function itself: it returns the call as structured JSON, which the program deserialises
into a function call and executes in its own runtime.

To show this, the author builds a *Shopping Agent* in Python on OpenAI's Chat Completions API that
helps users find fashion products, choosing on each turn between searching by keywords, fetching a
product's details, or asking the user for clarification. The walkthrough proceeds from an agent
scaffold and unit tests to the system prompt and function schemas, security measures, a refactoring
to reduce boilerplate, and finally a version of the agent that discovers its tools through the
[[DefinedTerm/model-context-protocol]].

## Details

- **Scaffold and tests.** The agent receives a user message and the conversation history, selects
  one of a predefined set of actions, executes it and returns the result. Unit tests are written
  first to check that the agent picks the expected action — for example, a search containing the
  right keyword, or product details for an ID that appeared earlier in the conversation.
- **System prompt and schemas.** The system prompt sets the agent's role, the expected output format
  (the functions) and constraints such as asking for clarification when a request is unclear. The
  article suggests one-shot or few-shot prompting can improve accuracy in real applications. Each
  function is declared to the model with a schema naming its parameters and which are required, and
  a `description` field that helps the model understand functions whose names are not
  self-explanatory.
- **Restricting the action space.** The article says it is essential to restrict which functions the
  agent can invoke through explicit conditional logic, warning that dynamically invoking functions
  with `eval` poses significant security risks, including prompt injections that could lead to
  unauthorised code execution (see [[DefinedTerm/action-space]]).
- **Guardrails against prompt injection.** A user-facing agent should anticipate adversarial users
  trying to trick it into unintended actions — compared to SQL injection, but through language — for
  instance by getting it to reveal its system prompt. Restricting the action space is described as a
  necessary first step but not sufficient; the article recommends sanitising input with a combination
  of traditional techniques such as regular expressions and denylists and LLM-based validation in
  which another model screens inputs, and shows a simple denylist check
  ([[DefinedTerm/prompt-injection]], [[DefinedTerm/guardrails]]).
- **Action classes.** The author uses the name *action classes* for the classes that serve as the
  gateway between the LLM's decision and actual system operations, turning the model's interpretation
  of the request into calls to microservices or other internal systems. In the author's implementation
  the conversation history is kept in the user interface's session state and passed in on each call,
  so the agent can, for example, pick up a product ID from earlier search results.
- **Reducing boilerplate.** Because the function schemas duplicate information already in the action
  classes, the article shows defining actions as Pydantic models and using the instructor library to
  generate the schema and deserialise the model's response.
- **Rules engines.** The article argues that rules engines rarely live up to their promise because of
  the combinatorial interactions of growing rule sets, and suggests LLM-based systems offer a
  compelling alternative — context-aware rather than rigid, and possibly more accessible to business
  users through natural-language prompts — though without full transparency or determinism. It
  proposes combining LLM-driven reasoning with explicit manual gates for critical decisions.
- **Function calling versus tool calling.** The two terms are often used interchangeably, but the
  article calls "tool calling" the more general and modern term, covering built-in tools such as a
  code interpreter or retrieval mechanisms as well as custom functions.
- **Relation to MCP.** The article describes MCP as an open protocol proposed by Anthropic with a
  client-server architecture of server, client and host, and says the core problem it addresses is
  flexibility and dynamic tool discovery. A hardcoded set of functions limits an agent's ability to
  adapt to new requests but makes it easier to secure; with MCP the agent queries the server at
  runtime for available tools. The author judges the added complexity justified for some
  applications, such as LLM-based IDEs or code generation tools that must keep up with the latest
  APIs, and illustrates the idea with a simple HTTP server and client for the shopping agent.
- **Conclusion.** Function calling introduces new risks when user input can ultimately trigger
  sensitive functions or APIs; the article advises starting with low-risk operations and extending to
  more critical ones as safety mechanisms mature.
