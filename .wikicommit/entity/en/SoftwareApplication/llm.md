---
title: "LLM"
type: "schema:SoftwareApplication"
lang: en
tags: [cli-tools, llm-tool-use, agent-tooling]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/May/27/llm-tools/'
    hash: sha256:a2f0dcf34a578fc6603991e91422876e38f9d81009a3891d641eb6b221e19cde
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A command-line tool and Python library by Simon Willison for running prompts against large language models from many vendors and local runtimes, extended through plugins; since version 0.26 it can also give models tools written as Python functions."
  applicationCategory: "Command-line tool and Python library"
  author: "Simon Willison"
---

LLM is a command-line tool and, at the same time, a Python library for working with large language
models, created by Simon Willison. It talks to models from several vendors — the release post for
version 0.26 names OpenAI, Anthropic and Gemini — and to local models served through Ollama, with
support for many of them supplied by plugins such as `llm-anthropic`, `llm-gemini` and `llm-ollama`.
Its author describes it as similar in shape to his other project, sqlite-utils, in being both a CLI
tool and a library.

## Capabilities

The tool is installed with ordinary Python tooling (the release post suggests `pip`, `pipx` or `uv`),
stores API keys per vendor with `llm keys set`, has a configurable default model, and selects another
model with `-m`.

Version 0.26 added tool support, which its author calls the biggest new feature since he started the
project. In that version:

- `--tool`/`-T` exposes a named tool to the model and can be repeated; LLM ships simple demo tools such
  as `llm_version` and `llm_time`.
- Tool plugins add capabilities to whichever model is in use. The author's first four are
  `llm-tools-simpleeval` (simple expression evaluation, for example mathematics),
  `llm-tools-quickjs` (a sandboxed QuickJS JavaScript interpreter whose state persists between calls),
  `llm-tools-sqlite` (read-only SQL against a local SQLite database) and `llm-tools-datasette` (SQL
  queries against a remote Datasette instance). The Datasette plugin is what he calls a "toolbox": a
  plugin holding several tools, configured through a constructor.
- `--functions` takes a block of literal Python code and makes every function defined in it available
  to the model as a tool.
- `--td` (`--tools-debug`) prints each tool call and its response.
- In the Python library, `model.chain()` works like `model.prompt()` but executes the tool calls a
  response requests and prompts the model again with the results; an `after_call` argument lets the
  caller observe each call. Tools can be sync or async functions, and when a model requests several
  async tools at once they run concurrently.

## Adoption & Ecosystem

The project is extended mainly through plugins, and at the time of 0.26 its author said he was most
excited about the potential of tool plugins, keeping a cookiecutter template for writing them and
documenting how model plugins add tool support. He also named acting as a
[[DefinedTerm/model-context-protocol]] client as clearly on the agenda, so that MCP servers could serve
as additional sources of tools. He presents the tool-support release as making LLM a way to build
"agents" in the sense of tools in a loop (see [[DefinedTerm/ai-agent]] and
[[DefinedTerm/function-calling]]); the release itself is described in
[[BlogPosting/large-language-models-can-run-tools-in-your-terminal-with-llm-0-26]].
