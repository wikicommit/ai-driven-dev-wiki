---
title: "Вам не нужен ещё один Claude Code: зачем Pi оставляет сборку агента пользователю"
type: "schema:BlogPosting"
lang: en
tags: [agent-harness, coding-agents, open-source]
sources:
  - type: url
    url: 'https://habr.com/ru/companies/first/articles/1087842/'
    hash: sha256:14f534481b69f23e05689f880a735f18ca402a8de40aaa4197daab0d4f331dc3
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A Russian-language overview on FirstVDS's Habr company blog that compares the minimal coding agent Pi with its batteries-included fork Oh My Pi, framing the difference as how many design decisions a harness makes on behalf of its user."
  author: ["YukinoKingu"]
  publisher: "FirstVDS"
---

This overview argues that discussion of coding agents tends to collapse into a comparison of models, while the layer between the model and the git working tree — the harness that runs the agent loop, assembles context, applies edits and saves sessions — decides much of what an agent can actually do (see [[DefinedTerm/agent-harness]]). It uses two related terminal agents to examine a question it says faces almost every tool developer: how many decisions to leave to the user and how many the product's author should make.

The two agents are [[SoftwareApplication/pi-coding-agent]], which builds its harness from scratch and deliberately keeps few built-in mechanisms, and [[SoftwareApplication/oh-my-pi]], a fork that collects more decisions into one ready-made agent. The post contrasts both with [[SoftwareApplication/claude-code]] and [[SoftwareApplication/openai-codex]], whose ready-made workflows it describes as convenient but carrying their vendors' decisions about planning, delegation and context, along with a degree of vendor lock-in.

## Key Points

- A harness organises the agent's cycle — passing the request to the model, executing the tools it calls and returning results — and the post argues that a model can propose a correct change yet fail to apply it through an awkward edit tool, or lose needed information after context compaction.
- Pi deliberately ships without built-in subagents, plan mode, a task list or permission prompts, leaving them to extensions, third-party packages or externally launched agent instances, on the reasoning that one feature name such as "subagents" hides quite different requirements and any built-in implementation favours one of them.
- The post separates confirming an action from restricting rights: Pi runs with the permissions of the process that launched it and has no built-in isolation, so a dialog in an extension is not a sandbox, and isolation needs a separately configured container or other restricted environment.
- Not every developer wants to assemble a tool: choosing and wiring extensions, checking for duplicated tools and fixing breakage after updates shifts work from the product's developers onto the user. The post argues that a minimal feature set and an implementation open to change are different properties.
- Oh My Pi is presented as the alternative that bundles more — LSP tools, a debugger, persistent code execution, subagents — while keeping the harness's source open to study and change.
- The post suggests the difference between the two is best described by how many decisions have already been made for the user, not by a feature table, and names a tendency it calls the pull of a fork: the more interconnected decisions a fork has of its own, the more later changes must be reconciled with them.
- It cites a third-party benchmark in which, with the same model and task set, Pi completed 20 of 30 tasks, ahead of Oh My Pi, Claude Code, Codex and OpenCode, while stressing that the benchmark was not a coding test, that the configurations were not fully identical, and that the result does not show Pi writes better code — only that extra harness features do not by themselves guarantee better results.

## Context

The post is written on a hosting company's corporate blog and ends with a promotional code for that company's servers. Its recommendation is that Pi suits cases where control over the agent's design matters — an internal assistant, experiments with context, embedding the agent loop in a product — while Oh My Pi is closer to Claude Code, Codex CLI and [[SoftwareApplication/opencode]] as a ready tool for daily coding work.
