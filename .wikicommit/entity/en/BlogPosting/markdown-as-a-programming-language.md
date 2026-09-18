---
title: "Spec-driven development: Using Markdown as a programming language when building with AI"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, agents, coding-tools, ai-assisted-programming]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/generative-ai/spec-driven-development-using-markdown-as-a-programming-language-when-building-with-ai/'
    hash: sha256:26b458e8ba4b8790a046f37bf816d79131b0b7612d69de3ff26ec16690387bb7
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A firsthand account of treating a Markdown specification file as an application's actual source code and having a coding agent compile it into Go, reported after a few months of running the workflow on one personal project."
  author: "Tomas Vesely"
  datePublished: "2025-09-30"
  publisher: "GitHub"
---

A post on the GitHub Blog in which the author reports writing an application entirely in Markdown
and having [[SoftwareApplication/github-copilot]] compile it into Go. The starting problem he
describes is context loss in the usual iterative workflow with coding agents: an agent asked to
"write app A that does X" and then fed successive feature and bug requests eventually loses track
of the app's purpose and past decisions, asking for things already explained or proposing changes
that contradict earlier choices. Custom instructions files such as Copilot's
`copilot-instructions.md` exist to hold that context, but the author found he forgot to update the
file after asking the agent to do things, and that putting the same information into both the chat
prompt and the instructions file felt redundant.

His response was to stop treating the Markdown file as instructions accompanying the code and
start treating it as the code. On his own pet project — an experimental MCP server for summarizing
GitHub discussions, issues and pull requests — he writes the application in `main.md` and invokes a
prompt file to generate `main.go`, and reports that he rarely edits or views the Go code directly.
The post presents this as an experimental workflow rather than a recommendation, and its evidence
is the author's own experience of a few months on a single project.

## Key Points

- The application is organized around four files: a `README.md` of user-facing documentation, a
  `main.md` holding the specification, a `compile.prompt.md` that instructs the agent to generate
  code from the specification, and the generated `main.go`.
- `README.md` is included by reference into `main.md` rather than duplicated, so that documentation
  and implementation stay in sync — adding an argument alias means editing the README alone.
- The author characterizes writing `main.md` as programming in Markdown and plain English: it
  stores variables, loops and logical conditions, offers the usual keywords such as `if`, `foreach`
  and `continue`, blends structural and declarative styles, and uses Markdown links as imports. The
  database schema is written in the same file, as tables with primary keys and indexes.
- The compile prompt is deliberately minimal — update the app to follow the specification, build
  with the editor's tasks, fetch each library's home page for documentation — on the reasoning that
  the real information belongs in the specification and a simple prompt stays portable to other
  agents.
- The development loop is: edit the specification, ask the agent to compile it, run and test, and
  update the spec when something does not work.
- Specifications can be linted as code is: a second prompt file asks the agent to optimize the
  specification for clarity and conciseness, treat English as a programming language, minimize
  synonyms by sticking to one term per concept, and remove duplication while preserving detail.
- Writing `main.md` is sometimes harder than writing Go directly, because it requires describing
  precisely what is wanted — which the author calls possibly the hardest part of software
  development. He uses Copilot to help write the specification itself, and reports it suggesting
  pagination style and parameter names.
- Compilation slows as the generated file grows; the author's stated next step is to have the spec
  instruct the agent to break each section into its own module.
- He had not added tests at the time of writing, and states that testing remains essential even in
  spec-driven workflows because a spec describes intended behavior while tests verify it.

## Context

The post is a firsthand instance of [[DefinedTerm/spec-driven-development]] taken to the point where
the specification is the only artefact the developer edits directly and the code is generated from
it — a position the post arrives at by practice rather than by arguing for it. The author frames the
technique as agent-agnostic and language-agnostic in principle, using VS Code, Copilot and Go only
as the examples he happens to work in, and closes by noting an untried experiment: discarding the Go
code entirely and regenerating the application in another language to see whether it works first
time. GitHub's own [[SoftwareApplication/github-spec-kit]] is promoted within the post as a
structured route to the same practice, in an inset separate from the author's own account.
