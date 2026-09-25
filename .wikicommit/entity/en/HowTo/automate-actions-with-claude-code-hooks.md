---
title: "Automate actions with Claude Code hooks"
type: "schema:HowTo"
lang: en
tags: [agent-tooling, agent-safety, anthropic]
sources:
  - type: url
    url: 'https://docs.claude.com/en/docs/claude-code/hooks-guide'
    hash: sha256:1e1b341c0362a8a274438e23e4a7f3d064318776299d9cf9ccbda07b62a868c9
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Anthropic's documented procedure for adding a hook to Claude Code — a handler, usually a shell command, that Claude Code runs at a fixed point in its lifecycle — by writing it into a settings file, confirming it with the /hooks browser, and triggering the event to test it."
---

This procedure adds a hook to [[SoftwareApplication/claude-code]]: a user-defined handler, most often a
shell command, that Claude Code runs at a specific point in its lifecycle, so that an action always
happens rather than depending on the model choosing to run it (see [[DefinedTerm/agent-hooks]]).
Anthropic's guide walks it through with a desktop notification that fires whenever Claude is waiting for
the user's input.

## Prerequisites

- Claude Code, and write access to one of the settings files that can hold hooks: `~/.claude/settings.json`
  for all of your projects, `.claude/settings.json` for a project and shareable through the repository,
  or `.claude/settings.local.json` for a project but not shared. Hooks can also come from managed policy
  settings, a plugin's `hooks/hooks.json`, or a skill's or subagent's frontmatter.
- For the guide's command examples that parse the hook's JSON input, `jq`.
- A hook script called from the command must be executable on macOS and Linux (`chmod +x`).

## Steps

1. Open the settings file for the scope you want and add a `hooks` block. Each event name is a key
   inside the single `hooks` object, holding a list of groups with an optional `matcher` and the
   handlers to run; for the notification example that is a `Notification` event with an empty matcher
   and a `command` handler that calls the platform's notification command (`osascript` on macOS,
   `notify-send` on Linux, a PowerShell dialog on Windows). If the file already has a `hooks` key, add
   the new event as a sibling rather than replacing the object. Claude can also be asked to write the
   hook.
2. Narrow when it fires, if needed. Without a matcher a hook fires on every occurrence of its event;
   a matcher filters on a field that depends on the event — the tool name for tool events (for example
   `Edit|Write`), the notification type for `Notification`, how the session started for `SessionStart`.
   On tool events an `if` field using permission-rule syntax, such as `Bash(git *)`, filters by tool
   name and arguments together.
3. Type `/hooks` to open the hooks browser, select the event, and confirm the new hook appears with its
   matcher, type, source file and command. The menu is read-only; changes are made in the settings JSON.
4. Test it by triggering the event. For the notification example, switch Claude Code to manual mode with
   `Shift+Tab`, ask for something that needs permission, switch away from the terminal, and wait for the
   notification.

## Notes

- A command hook receives the event's data as JSON on stdin and answers through its exit code and
  output. Exit 0 reports no objection (for `PreToolUse` it does not approve the call; the normal
  permission flow still applies). Exit 2 blocks the action, with stderr as the reason. Alternatively, a
  hook can exit 0 and print a JSON object for structured control, such as a `PreToolUse`
  `permissionDecision` of `allow`, `deny` or `ask` nested inside `hookSpecificOutput`.
- Besides `command`, a hook's `type` can be `http` (POST the event data to a URL), `mcp_tool`,
  `prompt` (a single-turn evaluation by a Claude model, Haiku by default) or `agent` (a subagent that
  can use tools to verify a condition; described as experimental).
- The guide's worked examples include auto-formatting files after edits with a `PostToolUse` hook,
  blocking edits to protected files with a `PreToolUse` script that exits 2, re-injecting critical
  context after [[DefinedTerm/compaction]] with a `SessionStart` hook on the `compact` matcher, logging
  configuration changes, reloading environment variables when the working directory changes, and
  auto-approving a specific permission prompt with a `PermissionRequest` hook — which the guide warns
  to keep narrowly matched.
- When several hooks match one event they all run, in parallel, before results are combined; for
  `PreToolUse` the most restrictive decision wins. A `PreToolUse` deny blocks the tool in every
  [[DefinedTerm/permission-modes]] setting, including `bypassPermissions`, but a hook returning `allow`
  cannot override deny rules from settings — hooks can tighten restrictions but not loosen them.
- If a hook does not fire, check that it appears under the right event in `/hooks` and that the matcher
  matches the tool name exactly (matchers are case-sensitive). If JSON output has no effect, look for
  shell-profile `echo` lines being prepended to stdout, or fields placed at the wrong level. A `Stop`
  hook that keeps blocking is overridden after eight consecutive blocks without progress, so it should
  exit early when the `stop_hook_active` input field is true.
