---
title: "AI Coding Agent"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/agentic-engineering/ai-coding-agent/'
    hash: sha256:bb64f869221b8e8a098760fd9b5e9036b0ac7f905aa9bbb025d181f3a42e4d9a
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/what-is-agentic-engineering/'
    hash: sha256:5887de1aff52ec544bd35326f452d4de9e1c58a331298d155e4a1c9f23c87af6
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/how-coding-agents-work/'
    hash: sha256:a8be3f0926e2b75d77e83036446bf575cf49b7dff42641018af0909da9d387eb
  - type: url
    url: 'https://arxiv.org/pdf/2508.00083'
    hash: sha256:fa7359ad66622d19e4c575d652a495d4060c511a03ad122023b745174eada4d4
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "Software powered by a large language model that takes autonomous actions on a codebase: reading files, writing or editing code, executing commands, and iterating on the results. A second account fixes the defining line more narrowly at code execution — an agent that can both write and run code."
---

An AI coding agent is software powered by a large language model that can take autonomous actions on a codebase. It reads files, understands the surrounding context, writes or edits code, executes commands, runs tests, and iterates based on the results it observes, rather than only suggesting what a person should type next. A second account narrows the defining line to a single capability: coding agents are agents that can both *write and execute* code, and it is execution that separates them from any other use of a model to produce code.

## Usage

The defining property is autonomy: the agent operates in a loop, taking actions and observing results until a task is done, rather than predicting a single next line of code. It might create a file, notice a missing import, fix it, run the tests, see a failure, and adjust its approach without a person intervening at each step. Tools cited as examples of this category include Claude Code, Cursor, Windsurf, and GitHub Copilot's agent mode; a second source names Claude Code, OpenAI Codex and Gemini CLI as its popular examples.

Coding agents are described as the foundation that agentic engineering is built on: without them, AI assistance is limited to autocomplete-style suggestions, whereas with them, whole tasks can be delegated and returned as working code. The quality of what an agent produces is described as depending heavily on the context it is given — clear specs, scaffolding, and guardrails — with agentic engineering named as the discipline of supplying that direction effectively.

In practice, this takes several shapes: a single-task agent that implements one described feature or fix end-to-end for a human to review; multi-agent setups where several agents work on different parts of a codebase at once; and background agents that run asynchronously on tasks like PR review or dependency updates while a person works on something else.

## How One Is Built

A chapter of [[CreativeWorkSeries/agentic-engineering-patterns]] describes the internals, and its
organising claim is that a coding agent is a **harness** for a language model: software that extends
the model with additional capabilities, powered by prompts the user never sees and implemented as
callable tools. Everything else follows from that separation.

At the centre is the model itself, which completes text and works in integer tokens rather than
words — which matters, the chapter notes, because providers charge by token and are limited in how
many they can consider at once. Interaction with it is expressed as a
[[DefinedTerm/chat-templated-prompt]]: a completion prompt formatted as a labelled conversation.
Because models are stateless, the harness keeps its own state and replays the whole conversation each
turn, so input cost grows as a session lengthens — partly offset by [[DefinedTerm/token-caching]],
which is why agents are built to avoid modifying earlier conversation content.

A **tool** is a function the harness makes available to the model. At prompt level it is described in
a system turn, the model ends its turn by emitting a call, the harness extracts that call — the
chapter's illustration is a regular expression — executes it, and appends the result as a further
turn. The chapter reports that most coding agents define a dozen or more tools, the most powerful
being code execution such as a `Bash()` or `Python()` tool. The hidden **system prompt** carries the
instructions that make the agent behave as it does and can run to hundreds of lines. **Reasoning**,
where the model spends extra tokens working through the problem before replying, is described as
particularly useful for debugging, since it lets the model follow complex code paths and mix in tool
calls; many agents expose a dial for how much of it to spend.

The chapter's conclusion is deliberately deflationary: an LLM plus a system prompt plus tools in a
loop is most of what it takes to build a coding agent, a simple tool loop is achievable in a few
dozen lines on top of an existing API, and it is a *good* tool loop — not the basic mechanics — that
represents the real work.

## How the Research Literature Frames It

[[ScholarlyArticle/a-survey-on-code-generation-with-llm-based-agents]] reaches the same category from
the research side and names it a **code generation agent**, characterising it by three features that
it says distinguish such agents from earlier code generation techniques. The first is *autonomy*: the
ability to independently manage the entire workflow, from task decomposition through coding to
debugging, where traditional code generation models assist a human developer passively through code
completion or function generation. The second is an *expanded task scope*: earlier research typically
involved tasks with clear boundaries and well-defined specifications, such as completing a line from
context or generating a function body from a signature, whereas an agent can cover most of software
development — handling ambiguous requirements, implementing entire projects, testing and refactoring,
and optimising iteratively on real-time feedback. The third is an *enhancement of engineering
practicality*: a shift of research emphasis away from algorithmic accuracy and toward engineering
implementation — agent reliability, complex workflow management, and efficient invocation of external
tools — which that survey describes as moving the problem into territory closer to classical software
engineering.

The survey draws the line between a language model and an agent architecturally rather than by
capability. A model's operation is a single, passive response process that lacks active planning,
state maintenance or continuous interaction with an environment; an agent builds a dynamic workflow
with autonomy, interactivity and iterativity, with the model serving as the reasoning engine that
decides the next action from the current environmental state. That framing puts the same weight on
the loop that the practitioner accounts above do, and adds the claim that what has changed is not
only what the software can do but which part of the job a person is left holding: the survey
describes the developer's role as moving to task definer, process supervisor and final result
reviewer.

## Related Terms

The first source names this term alongside [[DefinedTerm/tool-use]], [[DefinedTerm/plan-act-observe-loop]], [[DefinedTerm/guardrails]], [[DefinedTerm/human-in-the-loop]], and [[DefinedTerm/agentic-engineering]] as related glossary entries, without defining any of them.

- [[DefinedTerm/ai-agent]] — the general category this specialises
- [[DefinedTerm/harness-engineering]] — the discipline of building the scaffolding described above
- [[DefinedTerm/chat-templated-prompt]], [[DefinedTerm/token-caching]] — two mechanisms the internals account turns on
- [[ScholarlyArticle/a-survey-on-code-generation-with-llm-based-agents]] — the academic survey whose framing is summarised above
