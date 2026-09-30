---
title: "Large Language Models can run tools in your terminal with LLM 0.26"
type: "schema:BlogPosting"
lang: en
tags: [llm-tool-use, agent-tooling, cli-tools]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/May/27/llm-tools/'
    hash: sha256:a2f0dcf34a578fc6603991e91422876e38f9d81009a3891d641eb6b221e19cde
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "Simon Willison's release post for LLM 0.26, which adds tool support to his LLM command-line tool and Python library, walks through tools from plugins, ad-hoc Python functions and the Python API, and explains why he waited for model vendors to converge before building it."
  author: ["Simon Willison"]
  datePublished: "2025-05-27"
---

This post announces version 0.26 of [[SoftwareApplication/llm]], Simon Willison's command-line tool
and Python library for working with large language models, and the feature its author calls the
biggest since he started the project: support for tools. With it, models from OpenAI, Anthropic and
Gemini, and local models run through Ollama, can be given access to any tool that can be represented
as a Python function, and new tools can be installed as plugins.

Most of the post is a walkthrough. It starts with trivial built-in demo tools, moves on to plugins
that give a model a safe expression evaluator, a sandboxed JavaScript interpreter or SQL access to a
local SQLite database or a remote Datasette instance, then shows ad-hoc tools defined by passing
literal Python code on the command line, and finally the Python API. Along the way it shows models
recovering from their own mistakes through tool feedback — retrying a calculation after a function
turned out not to exist, and fetching a database schema after a guessed SQL query failed.

The closing sections step back. The author explains why tool support took him so long, gives his view
of the term "agents", and lists what comes next, including acting as a
[[DefinedTerm/model-context-protocol]] client.

## Key Points

- LLM 0.26 lets the CLI and the Python library grant models access to tools written as Python
  functions, across OpenAI, Anthropic, Gemini and Ollama-served local models.
- Tools can come from plugins, loaded by name with `--tool`/`-T`; a "toolbox" is the author's name for
  a plugin that holds several tools and is configured through a constructor, such as a Datasette
  toolbox pointed at a particular instance.
- The `--functions` option accepts a block of Python code and exposes every function it defines to the
  model as a tool — which the author calls "such a hack", demonstrating it with a four-line blog-search
  tool that returns raw HTML.
- The Python API gains `model.chain()`, which spots tool call requests in a response, executes them and
  prompts the model again with the results, potentially across many responses.
- The author argues, from his own experience of tracking the area, that tool use has become the single
  most effective way to extend the abilities of language models, and that the underlying trick is
  simple: tell the model which tools exist, let it output special syntax requesting one and stop, run
  the tool, and prompt again with the result.
- He says he held off because building an abstraction that works across many models needed vendors to
  agree on how tool use should work, and that there is now a very definite consensus among them.
- On terminology, he still does not like the word "agents", but observes that the field appears to be
  converging on "tools in a loop" — which, he says, is what this release provides.

## Context

The post is written by the tool's own author and reports his own demonstrations, so its claims about
what works are one developer's hands-on account rather than a measured comparison. It treats tool use
as the same pattern whether a vendor calls it tool usage or [[DefinedTerm/function-calling]], and it
frames the release as the step that makes LLM usable for building what others call agents
([[DefinedTerm/ai-agent]]). The author links his earlier interest in the idea to the
[[DefinedTerm/react-prompting]] pattern, of which he had once built a small implementation himself.
