---
title: "Antigravity CLI"
type: "schema:SoftwareApplication"
lang: en
sources:
  - type: url
    url: 'https://antigravity.google/changelog'
    hash: sha256:b0b3bf8a83113a1801fca60c849755cf0a8bf727c40a344c5d00a49916f1a79c
  - type: url
    url: 'https://antigravity.google/docs/subagents/'
    hash: sha256:5be9ef15339e691ef64f32feff17f95fe5b9fb784ff700b261fe1757ec8ce1a7
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
tags: [agents, coding-tools, cli, human-oversight]

properties:
  description: "The terminal client of the Google Antigravity product family: an interactive text-UI coding agent, invoked as agy, that can also run headless for scripts and CI."
  applicationCategory: "Terminal-based AI coding agent"
  operatingSystem: "macOS, Linux, Windows"
  featureList: "Interactive terminal UI with execution-mode cycling (request-review, accept-edits, plan); headless print mode with text, json and stream-json output; subagents and background tasks; custom agents defined in Markdown; skills, plugins, hooks and MCP servers; terminal sandbox; Remote Control from another device; Vim editing mode"
  author: "[[Organization/google]]"
---

Antigravity CLI is the command-line member of the [[SoftwareApplication/google-antigravity]]
product family, alongside the Antigravity 2.0 desktop app, the Antigravity IDE and the
[[SoftwareApplication/antigravity-sdk]]. It runs a coding agent inside a terminal user
interface and is invoked as `agy`. The product changelog lists its initial public release
as version 1.0.0; it dates 1.0.0 through 1.0.3 January 1, 2026, and the entries then run
from 1.0.4 (June 1, 2026) to 1.2.9 (September 23, 2026).

The CLI shares its configuration with the rest of the family: from 1.0.5 its permissions
merge project-level rules, user settings shared with Antigravity, and the CLI's own
`settings.json`, and customisations such as hooks, plugins and agents live in a shared
`~/.gemini/config/` directory.

## Capabilities

**Execution modes.** From 1.1.0 the default mode, `request-review`, pauses before each
file write to show a line-level diff in which the user can review, accept or reject individual code modifications, and
`Shift+Tab` cycles through `default`, `accept-edits` and `plan`. A `/plan` prefix replaced
the older `/planning` command in the same release. A `proceed-in-sandbox` permission mode
(1.0.1) auto-approves terminal commands that run inside the sandbox and asks only when a
command would leave it.

**Headless use.** Print mode (`-p` / `--print`) runs a single scripted turn. From 1.1.8 it
can emit `text`, `json` or `stream-json` (a typed NDJSON event stream), and `--json-schema`
enforces a schema on the structured result; from 1.1.15 `--input-format stream-json` keeps
one conversation open across newline-delimited prompts on stdin, so a driver program can
hold a session. The changelog frames these as serving CI, evaluation harnesses and scripts.
Several releases tighten headless behaviour: tools needing a permission the run lacks are
refused rather than hanging (1.1.3), refused actions are reported as `denied_actions`
(1.1.27), and from 1.2.6 a failing turn prints a structured `AGY_ERROR` line on stderr and
exits with code 3.

**Delegation.** The agent can hand work to subagents and background tasks, shown in a
status bar below the prompt (1.0.15) and managed from `/agents` and `/tasks` panels.
Custom agents can be defined as Markdown files with YAML frontmatter (1.1.6), selected at
launch with `--agent` (1.1.1), and given their own model tier (1.1.5). From 1.2.9,
an `@` prompt syntax sends a message directly to a subagent conversation, with
autocomplete listing running and completed subagents.

The product documentation describes the CLI's delegation model as asynchronous: rather
than locking the terminal during long builds, large codebase searches or multi-file
edits, the primary agent hands those operations to parallel subagents or background
tasks, so the user can keep prompting and inspecting files meanwhile. The `/agents`
panel lists every background agent with its role, state (running, done, killed or
error) and current step, and opens a detail view with that agent's full reasoning log,
tool calls and outputs; `/tasks` tracks non-agentic background work such as shell
commands and test suites. Custom agents are discovered from `.agents/agents/` in the
workspace and from `~/.gemini/config/agents/` globally. Because subagents may need
approval for a tool call, the CLI adds two shortcuts: `Alt+J` jumps straight to the next
subagent awaiting approval, and `Ctrl+K` approves the pending action shown above the
prompt without switching panels.

**Extension points.** The CLI loads skills, rules, plugins, lifecycle hooks and
[[DefinedTerm/model-context-protocol]] servers; `mcp` subcommands (1.1.16) manage the
server list without hand-editing `mcp_config.json`.

**Other features.** Named in the changelog: a `/btw` command for side questions; `/goal` for long-running goals; a
`/rewind` command that reverts a conversation and its file edits to an earlier step;
`/codesearch` over the workspace; `/voice` dictation; an optional Vim editing mode
(1.1.11); and Remote Control, which lets another device follow and control a running
terminal session; releases from 1.1.19 onward mention it, and 1.2.6 added starting it per
session with `--remote-control` or `/remote-control`.

## Adoption & Ecosystem

Sign-in options broadened over the release series: personal (consumer) accounts, a `GEMINI_API_KEY`
that runs the CLI directly against the Gemini API (1.1.13), Business sign-in for Gemini
Enterprise accounts, Workforce Identity Federation and Application Default Credentials
(1.1.10). A `remote-control` subcommand (1.2.0) registers the CLI with the operating
system's service manager as a background daemon that persists across logouts and reboots.
