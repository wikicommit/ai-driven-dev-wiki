---
title: "OpenCode"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-agents, coding-tools, cli, open-source]
sources:
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/vibe-coding/opencode/'
    hash: sha256:3cd1ec82817b79f22b6e50da9384b8f2ac1a6884b066eed6a1d9f4ad3e9fba97
  - type: url
    url: 'https://github.com/sst/opencode'
    hash: sha256:32149c4fdfab8d1624e1097f54b94cf8321178e8e1d31a37b5127d4071b779d7
  - type: url
    url: 'https://opencode.ai/docs/rules/'
    hash: sha256:7cd8c6d50ef202d91e43e65062c29cdda2d416ea578da276ae9ee84503315a7d
  - type: url
    url: 'https://opencode.ai/docs/'
    hash: sha256:a089d588869c390fcc98738c0a7686e55af8afc9c7c862f5d27d6b95bfb76732
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An open-source, end-to-end AI coding agent whose primary interface is the terminal, built to work with models from many providers as well as local models, with separate agents for planning and for changing code."
  applicationCategory: "AI coding agent (terminal)"
  featureList: "Native terminal user interface (TUI); support for 75+ model providers through Models.dev, including local models; Language Server Protocol (LSP) integration; parallel sessions and session sharing; a Plan agent that plans without editing and a Build agent that makes changes; a general subagent for complex searches and multistep tasks; a desktop application in beta; an IDE extension; undo and redo of agent changes; shareable conversation links"
---

OpenCode is an open-source, end-to-end AI coding agent that uses the terminal as its main interface,
helping developers write code, fix errors and understand code in their local environment. A chapter of
Jimmy Song's online handbook 智能体构建指南 describes it as one of the important open-source projects in
AI programming, and presents it as an important open-source alternative to closed-source coding
assistants such as [[SoftwareApplication/claude-code]].

The project's own README introduces it simply as "the open source AI coding agent". It is installed through an install script or a wide range of package managers across
macOS, Linux and Windows, and is also offered as a desktop application, marked as beta, for macOS,
Windows and Linux. The README asks related community projects that use "opencode" in their names to
state that they are not built by or affiliated with the OpenCode team.

On that chapter's account the project's design goal is to move beyond the "user asks, platform answers"
pattern of conventional AI coding assistants, which it criticises for lacking project-level context,
fitting poorly into development workflows, being tied to a single model provider, and running opaquely
in a way that is hard to combine with other tools. OpenCode is instead framed as a long-running agent
system that keeps sessions and context, integrates several LLMs and system tools, and exposes extensible
execution channels. Because it is not tied to any vendor, the chapter says, developers keep full control
over the runtime and the context, which it presents as better for privacy and auditability.

## Capabilities

The handbook chapter lists OpenCode's main features as a responsive, native terminal user interface
(TUI); support for more than 75 model providers, cloud or local, through Models.dev, with models from
OpenAI, Anthropic, Google and local models all selectable; integration with the Language Server
Protocol so the model better understands code structure; and parallel sessions with sharing, for
collaboration and debugging.

It describes the architecture as three layers. A terminal interaction layer (TUI plus CLI) keeps the
developer in the terminal rather than switching into a browser or IDE. An agent runtime maintains session
context, model adaptation, tool composition and permission control, parses the user's intent, calls
models and tools, and audits output; this is where the division of labour between a **Plan agent** and a
**Build agent** lives. An extension tool layer covers local file-system access, LSP-based code analysis
and external toolchains such as [[DefinedTerm/model-context-protocol]] servers, which is what lets the
agent act rather than only generate text.

The README describes the built-in agents concretely. Two are switched between with the Tab key:
**build**, the default, a full-access agent for development work; and **plan**, a read-only agent for
analysis and code exploration, which denies file edits by default, asks permission before running bash
commands, and is suggested for exploring unfamiliar codebases or planning changes. A third, the
**general** subagent, handles complex searches and multistep tasks; it is used internally and can be
invoked by writing `@general` in a message.

In use, the chapter says, the Plan agent is responsible for understanding and planning safely and does
not modify code directly, while the Build agent makes the actual changes, subject to review or
confirmation; other models or agents can take supporting roles such as analysis or calling external
tools. Its typical workflow has the agent output a plan first, a human review it, and only then the
change carried out, before testing and review lead into delivery.

### Getting started and everyday use

OpenCode's documentation introduces it as an open source AI coding agent available as a terminal-based
interface, a desktop app, or an IDE extension. Using it in the terminal needs a modern terminal emulator
and API keys for the LLM providers to be used; it is installed through an install script or with npm,
Bun, pnpm, Yarn, Homebrew, pacman and paru on Arch Linux, Chocolatey, Scoop, Mise or Docker, and the
documentation recommends the Windows Subsystem for Linux for the best experience on Windows. Any LLM
provider can be used by configuring its API key; for newcomers the documentation points to OpenCode Zen,
which it describes as a curated list of models tested and verified by the OpenCode team, connected
through the `/connect` command. Running `/init` in a project has OpenCode analyze it and create an
`AGENTS.md` file at the project root.

The documentation's suggested workflow for adding a feature is to plan first. A *Plan mode*, toggled with
the Tab key, disables OpenCode's ability to make changes and has it suggest *how* it would implement the
feature instead; the user iterates on the plan, can drag images into the terminal to add them to the
prompt, and then switches back to *Build mode* with Tab to have the changes made. It advises giving the
agent plenty of detail, and to talk to it like a junior developer on the team; simpler changes can be
requested directly without reviewing a plan first. The `@` key fuzzy-searches for project files to
reference in a prompt. `/undo` reverts the agent's changes and restores the original message so the
prompt can be tweaked and retried, and can be run repeatedly, while `/redo` reapplies them. `/share`
creates a link to the current conversation for a team; conversations are not shared by default.

### Rules and custom instructions

OpenCode's own documentation describes how project-specific instructions reach the model: through an
[[DefinedTerm/agents-md]] file whose contents are included in the LLM's context, which the
documentation likens to Cursor's rules. The `/init` command scans the important files in a repository,
may ask a couple of targeted questions when the codebase cannot answer them, and creates or updates
`AGENTS.md` with concise project-specific guidance — build, lint and test commands, architecture and
structure not obvious from filenames, project conventions and setup quirks, and references to existing
instruction sources such as Cursor or Copilot rules. An existing file is improved in place rather than
replaced, and the documentation recommends committing the project's `AGENTS.md` to Git.

Rules can live in two places: an `AGENTS.md` at the project root, which applies when working in that
directory or its sub-directories, and a global `~/.config/opencode/AGENTS.md`, applied across all
OpenCode sessions and recommended for personal rules because it is not committed or shared. For users
migrating from [[SoftwareApplication/claude-code]], OpenCode falls back to Claude Code's conventions — a
project `CLAUDE.md` when no `AGENTS.md` exists, `~/.claude/CLAUDE.md` when no global OpenCode file
exists, and skills under `~/.claude/skills/` — and each of these fallbacks can be switched off with an
environment variable. At startup it looks first for local files by traversing up from the current
directory, then the global file, then the Claude Code file, and the first match wins in each category,
so `AGENTS.md` is used over `CLAUDE.md` when both are present.

Further instruction files can be listed in the `instructions` field of `opencode.json`, including glob
patterns and remote URLs (fetched with a 5 second timeout), and all of them are combined with the
`AGENTS.md` files. OpenCode does not automatically parse file references written inside `AGENTS.md`;
the documentation recommends the `instructions` field instead, or explicit instructions in `AGENTS.md`
telling the agent to load referenced files only when a task needs them. For monorepos it calls the
glob-pattern approach more maintainable than manual instructions.

Because the architecture does not lock in a model, the chapter describes three model strategies: cloud
models, local models run on a local inference framework for private, low-cost inference, and a hybrid in
which tasks are routed to models by their needs. It notes that the OpenCode team also publishes a list
of models it has verified for coding, OpenCode Zen. And it corrects what it calls a common
misunderstanding: OpenCode does not "provide free models"; rather, its architecture allows community,
local, low-cost or free models to be brought in and combined across several model services, so that
developers without a paid API can still get most coding work done.

## Adoption & Ecosystem

The handbook chapter describes **Oh My OpenCode** as a user-level convention layer built around
OpenCode. Its argument is that OpenCode is a runtime rather than a set of conventions, and that in large
projects or teams, without agreed behaviour and engineering paths, an agent's behaviour becomes hard to
predict. Oh My OpenCode is said not to replace OpenCode but to standardise ways of using it that work:
defining how agent roles such as the Plan and Build agents cooperate, standardising prompt structure and
constraints for more consistent output, providing composable workflow templates and strategies, and
agreeing a structure for context files such as [[DefinedTerm/agents-md]] so that project knowledge
accumulates over time. The chapter calls this a "developer convention layer" that makes agent use
portable, auditable and suitable for teams, and says its design direction is incremental rather than
aiming for perfection in one step: estimate the current state, probe and propose in stages, make
controlled changes, and adjust the next step from feedback.

The chapter's own engineering advice for using OpenCode on real projects is to define an agent context
file such as `AGENTS.md` at the project root so the agent has clear boundaries of project knowledge; to
route by task, sending quick responses and small completions to small local or lightweight cloud models
and complex reasoning to stronger ones; to adopt a plan-then-execute pattern in which the Plan agent may
only view and suggest, the Build agent alone makes changes, and key changes require explicit
confirmation and logging; and to connect external tools such as code search, test frameworks and CI/CD
systems through MCP or an equivalent extension mechanism to close the automation loop. These are
recommendations from the handbook's author rather than documented behaviour of the tool.
