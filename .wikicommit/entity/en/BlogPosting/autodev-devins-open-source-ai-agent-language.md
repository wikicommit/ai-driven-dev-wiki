---
title: "AutoDev DevIns —— 开源 AI 智能体语言，构建 AI 驱动的自动编程"
type: "schema:BlogPosting"
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
  description: "A March 2024 Chinese-language blog post by Phodal Huang introducing DevIns (Development Instruction), a language for AutoDev that sits between natural language and instruction text, is compiled by AutoDev into instructions for agents and the IDE, and can write files, apply patches, run tests and commit code."
  author: ["Phodal Huang"]
  datePublished: "2024-03-17"
---

This post, written in Chinese by Phodal Huang, announces [[ComputerLanguage/devins]], a new AI agent
language built into [[SoftwareApplication/unit-mesh-auto-dev]]. It follows a previous AutoDev release that
had added custom agents, letting users build their own agents to assist with software development tasks.
DevIns is presented as a way for users to describe development tasks more quickly while also automatically
processing what an AI agent returns — for example, a `/write:README.md` instruction followed by a code block
is translated by AutoDev into writing that content to `README.md`.

The post explains the motivation, what the language is, how to use it in the IDE, why it was renamed, and
what the authors plan next.

## Key Points

- The author reports that, as more and more agents were built in AutoDev, all interaction with the model
  turned out to happen through instruction text: the user interacts with an agent through instructions, and
  the agent returns content and operates on the editor or IDE. A custom prompt such as "explain the selected
  code: `$selection`" is given as an example in which "explain" can be read as an instruction.
- From this the authors asked whether users could interact with agents in natural language, with the model
  replying in instruction text that operates the editor or IDE.
- DevIns is defined in the post as an interaction language between natural language and instruction text:
  natural language describes the development task, and instruction text is used to interact with agents and
  the IDE. The post calls it interactive, compilable and executable.
- Beyond reading file contents, code changes and custom variables, the post lists agent instructions:
  `/write` to operate on code at a path, `/run` to run the corresponding tests, `/patch` to apply a patch from
  the AI's output, and `/commit` to commit code.
- The authors say they drew on their IDE-development experience to give DevIns intelligent completion and
  hints, so that users need not worry about the complexity of the instructions.
- To try it, the post says to install version 1.7.2 of the AutoDev plugin, create a `hello.devins` file,
  write DevIns instructions and click run.
- The language was first called DevIn, from "AutoDev Input Language". When it was close to release, a
  similarly named Devin AI project published a demo video, so the authors renamed it DevIns (Development
  Instruction). Because of JetBrains' review process, the default file extension was still `.devin` at the
  time of writing.
- Planned next steps are strengthening how DevIns interacts with agents (the post wonders whether something
  like Jupyter Notebook fits), building more agents with AutoDev's custom-agent capability, designing richer
  DevIns instructions, and building a cross-platform DevIns compiler.

## Context

The post is the author's own announcement of a feature of the open-source tool he works on, and its claims
describe that feature as designed at the time rather than any measured result.
