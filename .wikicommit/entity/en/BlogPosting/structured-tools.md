---
title: "Structured Tools"
type: "schema:BlogPosting"
lang: en
tags: [tool-use, agent-frameworks]
sources:
  - type: url
    url: 'https://blog.langchain.com/structured-tools/'
    hash: sha256:e4617b3533e7c5a963a20bc2b7e5763d3a2a4cfe73dd16914c5abd6772686b08
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A May 2023 LangChain blog post introducing structured tools — tools that accept any number of typed inputs rather than a single string — together with an agent class built to use them."
  author: ["The LangChain Team"]
  datePublished: "2023-05-02"
  publisher: "LangChain"
---

This post from the LangChain team announces [[DefinedTerm/structured-tool]]s in
[[SoftwareApplication/langchain]]: a new tool abstraction that lets a tool take an arbitrary number of
inputs of arbitrary types, where earlier LangChain tools took a single string. It pairs the abstraction
with a new agent class, `StructuredChatAgent`, designed to work with such tools.

The post places the change in the history of LangChain's agents. Tool use in the early days was
simplistic — a model generated a tool name and one input string, which confined an agent to one tool per
turn — and the post attributes that restriction mainly to what models of the time could reliably do.
It credits more capable models such as `text-davinci-003`, `gpt-3.5-turbo` and `gpt-4` with raising
that floor, which prompted the team to revisit the limits on tool usage.

## Key Points

- When LangChain launched in November 2022, agent and tool use were central to its design, and the team
  built one of the first chains based on the ReAct paper.
- Earlier in 2023 LangChain had introduced a "multi-action" agent framework in which an agent can plan
  several actions per step; structured tools remove the single-string input constraint on top of that.
- A structured tool wraps any function so that an agent can call it, and is defined by a `name`, a
  `description`, an `args_schema` (a Pydantic `BaseModel` that both tells the agent what inputs are
  required and validates them before execution) and `_run`/`_arun` functions holding the tool's logic.
- The post advises that a tool's name should communicate unambiguously what it does — "if a tool's name
  isn't clear to you, it probably isn't clear to the agent either" — and that names can also hint at how
  tools relate to one another.
- `StructuredTool.from_function()` builds a tool from a callable and infers its `args_schema` from the
  function's signature; subclassing `BaseTool` gives more control over the definition.
- Two new toolkits were released on the new class: file management (write, grep, move, copy, list
  directories, find) and a stateful PlayWright browser toolkit for visiting websites, clicking,
  submitting forms and querying data.
- Structured tools with more than one argument do not work with LangChain's earlier agent types without
  customization, whereas tools that take a single string still work with existing agents, and older
  string tools work with the new agent.

## Context

The post is the vendor's own feature announcement, and its account of why earlier tools were limited to a
single string — the constraints of the models of the time — is the team's own explanation.
