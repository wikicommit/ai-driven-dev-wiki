---
title: "DevIns"
type: "schema:ComputerLanguage"
lang: en
tags: [coding-agents, coding-tools, open-source]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/autodev-devins-the-ai-agent-language/'
    hash: sha256:c697ad04281f2e84e44e08ada86b237fd585e5165e98e7f5fd7a0b814b3acc4c
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An AI agent language in AutoDev, short for Development Instruction, that sits between natural language and instruction text: natural language describes a development task and instructions such as /write, /run, /patch and /commit let the agent act on files, tests and version control in the IDE."
  alternateName: "Development Instruction"
---

DevIns (Development Instruction) is an AI agent language built into
[[SoftwareApplication/unit-mesh-auto-dev]], introduced in
[[BlogPosting/autodev-devins-open-source-ai-agent-language]]. Its author describes it as an interaction
language between natural language and instruction text: natural language describes a software development
task, and instruction text is used to interact with agents and with the IDE. He calls it interactive,
compilable and executable — when a DevIns script is run, the DevIns compiler generates instruction text from
the instructions it contains and sends it to the agent, whose result is then applied to the editor or IDE.

The language grew out of the observation, in AutoDev, that every interaction with the model went through
instruction text. DevIns aims to let users describe development tasks more quickly and to process what an
AI agent returns automatically, rather than leaving the user to apply it by hand.

It was first named DevIn, from "AutoDev Input Language", and renamed to DevIns shortly before release
because a similarly named Devin AI project had just published a demo video; at the time of the announcement
its default file extension was still `.devin` because of JetBrains' plugin review process.

## Details

A DevIns file mixes a natural-language request with instructions that pull in context. In the post's
example, "explain code" followed by a `/file:` instruction naming a Java source file is compiled by AutoDev,
together with the surrounding context, into an instruction that reads that file's contents.

Besides reading files, code changes and custom variables, DevIns has instructions that act: `/write` writes
code to a path (optionally a line range), `/run` runs the corresponding tests, `/patch` applies a patch from
the AI's output, and `/commit` commits code. A `/write:README.md` instruction followed by a code block, for
example, writes that block into `README.md`. The IDE provides completion and hints for the instructions.

In AutoDev plugin version 1.7.2, a user creates a `hello.devins` file, writes instructions and clicks run.
The authors' stated next steps were to strengthen how the language interacts with agents, add richer
instructions, combine it with AutoDev's custom agents, and build a cross-platform DevIns compiler.
