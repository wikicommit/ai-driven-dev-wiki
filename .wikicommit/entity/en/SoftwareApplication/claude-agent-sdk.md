---
title: "Claude Agent SDK"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-tooling, agent-safety, human-oversight, agent-architecture]
sources:
  - type: url
    url: 'https://docs.claude.com/en/api/agent-sdk/permissions'
    hash: sha256:c4534377b28cb19c1b4d96673f98b2d47028ae3535bb6eda233c73d3933d9f61
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
    hash: sha256:26ce4c203cbb030f31253f1eb174b46b2c0203c9b44576aa4654b89b4d7be777
  - type: url
    url: 'https://claude.com/blog/building-agents-with-the-claude-agent-sdk'
    hash: sha256:895d1a97d551333d37c154b093d44ddda469401d6c2596c7a363373e974754a4
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Anthropic's SDK for building agents on Claude, available in TypeScript and Python, renamed from the Claude Code SDK because the harness that powers Claude Code can power other kinds of agent. Its documented permission system evaluates every tool request through a fixed six-step order — hooks, deny rules, ask rules, permission mode, allow rules, then a runtime callback."
  applicationCategory: "Agent development SDK"
  featureList: "Six-step permission evaluation; six permission modes; allow/deny/ask rules from options or settings.json; canUseTool runtime callback; PreToolUse and PermissionRequest hooks; subagent permission inheritance; subagents with isolated context windows; automatic compaction; custom tools; MCP integration"
  author: "[[Organization/anthropic]]"
---

The Claude Agent SDK is Anthropic's toolkit for building agents on Claude, offered in both
TypeScript and Python. It was previously the Claude Code SDK: Anthropic renamed it, in
[[BlogPosting/building-agents-with-the-claude-agent-sdk]], on the grounds that the agent harness that
powers [[SoftwareApplication/claude-code]] can power many other types of agent too. That post's key
design principle for the SDK is to give agents a computer — bash commands and the ability to create,
edit and search files — so that they can work the way humans do, and it names finance,
personal-assistant, customer-support and deep-research agents among the things it can be used to build.

The permission documentation takes up the other end of the SDK: the controls that decide what an agent
may do with its tools. The documentation's framing is that permission modes and rules define what is
allowed automatically, while a runtime callback named `canUseTool` handles everything else as it
happens.

Rules are declared in SDK options or in a project settings file, and the documentation specifies
the order in which each kind of rule takes effect and what can and cannot override it.

## Capabilities

The renaming post organises the SDK's features around a feedback loop it says agents often operate
in — gather context, take action, verify work, repeat. For gathering context it points to
[[DefinedTerm/agentic-search]] over the file system, subagents (supported by default, and useful for
running tasks in parallel and for keeping context isolated, since each returns only relevant
information to the orchestrator), and a compact feature that automatically summarises previous
messages as the context limit approaches, built on Claude Code's `/compact` command (see
[[DefinedTerm/compaction]]). For taking action it lists custom tools, bash and scripts, code
generation, and [[DefinedTerm/model-context-protocol]] servers for integrations with external
services. For verification it describes rule-based feedback such as linting, visual feedback from
screenshots or renders, and [[DefinedTerm/llm-as-a-judge]], which it calls generally not very robust.
These are the vendor's own descriptions of its product, offered as best practices from its teams'
deployments.

Every tool request passes through six steps in a fixed order. **Hooks** run first and may deny a
call outright or pass it on; a hook returning an allow does not skip the deny and ask rules that
follow. **Deny rules** are checked next and block the tool even in the most permissive mode; a
bare-name deny such as `Bash` removes the tool from the model's context entirely before evaluation
begins, so only scoped rules like `Bash(rm *)` are checked at this step. **Ask rules** send the call
to the callback for confirmation, again even in the most permissive mode. The **permission mode**
then applies, followed by **allow rules** — where a call the tool approves on its own, such as a
read-only shell command or a file read inside a working directory, also resolves with no rule
needed. Anything still unresolved reaches the **`canUseTool` callback**.

Six modes are documented: `default`, which adds no mode-based approvals; `dontAsk`, which denies
anything that would otherwise prompt and never calls the callback; `acceptEdits`, which
auto-approves file edits and filesystem operations; `bypassPermissions`, which skips checks apart
from documented exceptions; `plan`, which routes file edits to the callback so writes cannot be
auto-approved while planning; and `auto`, in which a model classifier approves or denies prompts.

The documentation is direct about two properties that are easy to get wrong. Auto-approved tools
never reach the callback, so permission checks placed only there are silently bypassed for those
tools — for checks that must run on every call it directs the reader to a `PreToolUse` hook instead,
since hooks run before every other step and a hook denial applies even in `bypassPermissions`. And
`allowed_tools` does not constrain `bypassPermissions`: listing only `Read` alongside that mode
still approves every tool, because unlisted tools match no allow rule and fall through to the mode.
The documentation also refers to a set of actions that no mode auto-approves, and separately notes
that tools requiring user interaction always fall through to the callback, even in
`bypassPermissions`, and are denied in `dontAsk`.

Rules may be scoped. `Edit(path)` rules govern all built-in file-writing tools, and path anchoring
is explicit — a doubled leading slash denotes an absolute filesystem path, while a single one
anchors at the rule's source. Tool-name globs are accepted in deny rules, and in allow rules only
after a literal, glob-free MCP server prefix, with an unanchored entry ignored and a startup warning
emitted. Subagents inherit the parent session's mode, except that a subagent may use its own
`permissionMode` from its definition when the parent is in `default`, `dontAsk` or `plan`; the
documentation also states that `bypassPermissions` is never applied to a subagent unless the parent
session itself runs in it.

## Adoption & Ecosystem

The permission mode can be set once when a query is created or changed mid-session, which the
documentation offers as a way to start restrictive and loosen as trust builds. Rules can also be
declared in a project settings file, read when the project setting source is enabled. The
documentation notes several behaviors as requiring particular minimum versions of
[[SoftwareApplication/claude-code]], which is the runtime the SDK's permission behavior is described
against. For the underlying safety posture, see [[DefinedTerm/deny-first-permission-evaluation]] and
[[DefinedTerm/permission-modes]].

Another Anthropic source describes the SDK from the opposite end — not what it restricts, but what
it is capable of and where that capability runs out.
[[BlogPosting/effective-harnesses-for-long-running-agents]] characterises it as a powerful,
general-purpose agent harness adept at coding as well as at other tasks needing a model to use tools
to gather context, plan and execute, with context-management capabilities including
[[DefinedTerm/compaction]] that in principle let an agent work usefully for an arbitrarily long time.
It then reports that this is not sufficient in practice: a frontier model running on the SDK in a
loop across multiple context windows still fell short of building a production-quality web app from a
high-level prompt. It describes two failure patterns — the agent trying to one-shot the app and running
out of context partway through, and a later session seeing progress and declaring the job done — and
notes that the first happens even with compaction, which does not always pass perfectly clear
instructions to the next agent. What the post adds on top of the SDK is therefore not SDK functionality but prompt and
artifact discipline — a differently-prompted first session and a durable progress file, git history
and feature list (see [[DefinedTerm/initializer-agent]]). Accompanying code examples are published as
a quickstart.
