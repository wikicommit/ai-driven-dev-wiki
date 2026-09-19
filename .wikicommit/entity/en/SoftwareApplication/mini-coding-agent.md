---
title: "Mini-Coding-Agent"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, cli, agent-architecture, open-source]
sources:
  - type: url
    url: 'https://github.com/rasbt/mini-coding-agent'
    hash: sha256:d078822f471591972946c2fadd69b08a042b517b82152ebf0b98c85384710017
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A small standalone coding agent written as a single Python file, published as a readable reference implementation of the components a coding agent harness is built from rather than as a production tool. It runs against a locally installed Ollama model and depends on nothing beyond the Python standard library."
  applicationCategory: "Coding agent reference implementation"
  featureList: "Workspace snapshot collection; stable prompt prefix separated from changing turn state; structured tools with input and path validation; approval gates for risky tools; transcript and working-memory persistence with session resume; bounded delegation to subagents"
---

Mini-Coding-Agent is a minimal local agent loop distributed as a single Python file,
`mini_coding_agent.py`, with a `mini-coding-agent` CLI entry point. Its repository describes it as a
readable harness implementation written to explain the core components of coding agents, and its
own notes state plainly that it is intentionally small and optimised for readability rather than
robustness — so it is a teaching artefact as much as a tool.

The project has no Python runtime dependency beyond the standard library, so the script can be run
directly with `python mini_coding_agent.py`; `uv` is offered as an optional way to manage the
environment and provide the CLI entry point. It requires Python 3.10 or later, a local Ollama
installation and a model pulled locally, and the agent reaches the model by sending prompts to
Ollama's `/api/generate` endpoint. The repository is published under the Apache-2.0 license, and the
README links to an accompanying tutorial it describes as detailed.

## Capabilities

The README organises the harness around six building blocks. The first is live repository context:
the agent collects stable workspace facts up front — repository layout, instructions and git state.
The second is prompt shape and cache reuse, a stable prompt prefix held separate from the changing
request, transcript and memory so that repeated model calls can reuse the static parts efficiently.
The third is structured tools with validation and permissions, so the model acts through named tools
with checked inputs and workspace path validation behind approval gates rather than taking free-form
arbitrary actions. The fourth is context reduction and output management: long outputs are clipped,
repeated reads deduplicated and older transcript entries compressed — [[DefinedTerm/compaction]] — to
keep the prompt size under control. The fifth pairs a full durable transcript with a smaller working
memory, so a session can be resumed while the important state survives. The sixth is bounded
delegation, in which scoped subtasks go to helper agents that inherit enough context to be useful
while operating within limits, one arrangement of [[DefinedTerm/sub-agent-architecture]].

Risky tools — shell commands and file writes — run behind an approval mode chosen at startup. `ask`
prompts before each risky action and is both the default and the mode the README recommends;
`never` denies risky actions outright; `auto` allows them automatically, which the README qualifies
as including arbitrary command execution and file writes by the model and advises using only with
trusted prompts and trusted repositories. The choice is a minimal instance of
[[DefinedTerm/permission-modes]], reduced to three positions.

Sessions are saved under the target workspace root and can be resumed either as the most recent one
or by a specific session identifier; resuming work from saved state is the concern
[[DefinedTerm/checkpoint-and-resume]] addresses. Inside the REPL a small set of slash commands is handled by the agent
itself rather than passed to the model: printing the distilled session memory with its current task,
tracked files and notes; printing the path to the saved session file; clearing history and memory
without leaving the REPL; and exiting. Other behaviour is set by flags before the agent starts — the
workspace directory, the Ollama model and server URL, resume behaviour, approval mode, and limits on
how many model and tool turns one request may take and how long each model output may be.

The agent expects the model to emit either a `<tool>` or a `<final>` block. The README notes that
Ollama models vary in how reliably they follow that instruction and suggests moving to a stronger
instruction-following model when one does not.

## Adoption & Ecosystem

The project's model backend is currently Ollama, with `qwen3.5:4b` as the default and larger Qwen
3.5 variants suggested where memory allows — so the agent runs entirely against a locally hosted
model rather than a hosted API. Beyond the tutorial it accompanies, the repository ships an
`EXAMPLE.md` walkthrough as its concrete usage example, and a `tests` directory.
