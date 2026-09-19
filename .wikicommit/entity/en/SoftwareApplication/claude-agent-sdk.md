---
title: "Claude Agent SDK"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-tooling, agent-safety, human-oversight]
sources:
  - type: url
    url: 'https://docs.claude.com/en/api/agent-sdk/permissions'
    hash: sha256:c4534377b28cb19c1b4d96673f98b2d47028ae3535bb6eda233c73d3933d9f61
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Anthropic's SDK for building agents on Claude, available in TypeScript and Python. Its documented permission system evaluates every tool request through a fixed six-step order — hooks, deny rules, ask rules, permission mode, allow rules, then a runtime callback — so that what an agent may do is declared rather than left to the model."
  applicationCategory: "Agent development SDK"
  featureList: "Six-step permission evaluation; six permission modes; allow/deny/ask rules from options or settings.json; canUseTool runtime callback; PreToolUse and PermissionRequest hooks; subagent permission inheritance"
  author: "[[Organization/anthropic]]"
---

The Claude Agent SDK is Anthropic's toolkit for building agents on Claude, offered in both
TypeScript and Python. The aspect documented in the source available here is its permission system:
the controls that decide what an agent may do with its tools. The documentation's framing is that
permission modes and rules define what is allowed automatically, while a runtime callback named
`canUseTool` handles everything else as it happens.

What distinguishes the design is that the decision is taken outside the model. Rules are declared in
SDK options or in a project settings file, and the resulting evaluation is deterministic — a point
the documentation makes concrete by specifying exactly where each kind of rule takes effect and what
can and cannot override it.

## Capabilities

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
A set of actions is documented as never auto-approved by any mode, including removals targeting a
critical path and tools that require user interaction.

Rules may be scoped. `Edit(path)` rules govern all built-in file-writing tools, and path anchoring
is explicit — a doubled leading slash denotes an absolute filesystem path, while a single one
anchors at the rule's source. Tool-name globs are accepted in deny rules, and in allow rules only
after a literal, glob-free MCP server prefix, with an unanchored entry ignored and a startup warning
emitted. Subagents inherit the parent session's mode, and the documentation states that
`bypassPermissions` is never applied to a subagent unless the parent session itself runs in it.

## Adoption & Ecosystem

The permission mode can be set once when a query is created or changed mid-session, which the
documentation offers as a way to start restrictive and loosen as trust builds. Rules can also be
declared in a project settings file, read when the project setting source is enabled. The
documentation notes several behaviors as requiring particular minimum versions of
[[SoftwareApplication/claude-code]], which is the runtime the SDK's permission behavior is described
against. For the underlying safety posture, see [[DefinedTerm/deny-first-permission-evaluation]] and
[[DefinedTerm/permission-modes]].
