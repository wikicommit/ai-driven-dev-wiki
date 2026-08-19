---
title: "agent hooks"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, automation, code-quality]
sources:
  - type: url
    url: 'https://kiro.dev/blog/introducing-kiro/'
    hash: sha256:83f496f2e0d7f844907485218708133937302b71468f8cc11cabc239a5753da9
  - type: url
    url: 'https://code.claude.com/docs/en/best-practices'
    hash: sha256:92807ef3d58f63fbea435ea928df49e2f3341e118eb8c40db08800c100a4c4c5
  - type: url
    url: 'https://code.claude.com/docs/en/hooks-guide'
    hash: sha256:155e5ab620eab496f8385a3e87ca54687af20c5b57321f14baee4017a74188b1
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Configuration that runs something automatically at defined points in an agent's workflow — on a file event or at a step in the loop — so that an action happens every time rather than depending on the model choosing to take it."
  termCode: ""
  inDefinedTermSet: ""
---

Hooks are configuration that runs something automatically at defined points in an agent's workflow, rather than leaving the action to the model's discretion. Anthropic's Claude Code documentation frames the value of the mechanism as determinism: instructions in a context file are advisory, whereas hooks are deterministic and guarantee the action happens, which the documentation offers as the reason to use hooks for actions that must happen every time with zero exceptions. Concrete implementations differ substantially in what fires and in what runs.

## Usage

**Claude Code** implements hooks as user-defined commands that run at specific points in the agent's lifecycle. Its documentation contrasts them directly with `CLAUDE.md` instructions: those are advisory, while hooks are deterministic and guarantee the action happens. They are configured in `.claude/settings.json`, can be browsed with `/hooks`, and can be written by the agent itself — the documentation's examples are prompts such as "write a hook that runs eslint after every file edit" or "write a hook that blocks writes to the migrations folder." A Stop hook is described separately as a way to run a check as a script and block a turn from ending until it passes, with the caveat that Claude Code overrides the hook and ends the turn after eight consecutive blocks.

**Kiro** implements hooks as event-driven automations that trigger an *agent* to execute a task in the background, on file save, create, or delete, or on manual trigger. Its announcement describes them as acting "like an experienced developer catching things you miss," and the examples given are updating a test file when a React component is saved, refreshing README files when API endpoints change, and scanning for leaked credentials before a commit. Setup takes a plain-language prompt, from which Kiro generates an optimised system prompt and selects the repository folders to monitor; committing the hook to Git then applies the standard across the whole team.

The distinction is worth keeping straight: Claude Code's hooks run a script deterministically, while Kiro's hooks dispatch an agent to perform a task, so the hook's *firing* is deterministic but its *action* is not. Kiro's announcement additionally positions hooks as team-level rather than personal configuration — committed to Git so everyone gets the same checks — and frames them against the mental checklist a careful developer runs before submitting code. The Claude Code documentation makes no equivalent claim about where hook configuration lives organisationally.

### Anatomy of a hook: the Claude Code model

Anthropic's dedicated hooks guide sets out the mechanism in enough detail to show what a mature implementation of the idea involves. A hook registration has three parts: the **event** it listens for, an optional **matcher** narrowing which occurrences of that event fire it, and one or more **handlers** that actually run.

The event list is long and spans the whole session lifecycle rather than file edits alone. It covers session boundaries (`SessionStart`, `SessionEnd`, `Setup`), prompt handling (`UserPromptSubmit`, `UserPromptExpansion`), the tool call cycle (`PreToolUse`, `PermissionRequest`, `PermissionDenied`, `PostToolUse`, `PostToolUseFailure`, `PostToolBatch`), delegation (`SubagentStart`, `SubagentStop`), turn boundaries (`Stop`, `StopFailure`), context management (`PreCompact`, `PostCompact`), configuration and filesystem changes (`ConfigChange`, `CwdChanged`, `DirectoryAdded`, `FileChanged`, `InstructionsLoaded`, `WorktreeCreate`, `WorktreeRemove`), and interaction with MCP servers (`Elicitation`, `ElicitationResult`). What a matcher filters differs per event: tool name for the tool-call events, how the session started for `SessionStart`, notification type for `Notification`, agent type for `SubagentStart`/`SubagentStop`, and so on, with several events supporting no matcher at all. A separate `if` field on an individual handler filters by tool name *and arguments* together using permission-rule syntax, so a hook can be scoped to `Bash(git *)` rather than to all Bash calls — though the documentation notes this filter is best-effort and fails open when a command cannot be parsed, so it should not be used to enforce a hard allow or deny.

Handlers are not limited to shell commands. Five handler types are documented: `command` (a shell command, the common case), `http` (POST the event data to an endpoint, which replies with the same JSON a command hook would print), `mcp_tool` (call a tool on a connected MCP server), `prompt` (a single-turn LLM evaluation, run on Haiku by default), and `agent` (an experimental multi-turn handler that spawns a subagent able to read files and run commands before returning a verdict). The last two are the documentation's answer to decisions that require judgment rather than a deterministic rule, and it gives a clean division of labour between them: use a prompt hook when the event's input data alone is enough to decide, and an agent hook when the decision has to be verified against the actual state of the codebase. Both return `{"ok": ..., "reason": ...}`; a prompt hook can additionally set `"impossible": true` on a `Stop` event to mark a condition that can never be satisfied, which lets the turn end.

Communication with a command hook runs through stdin, stdout, stderr, and the exit code. The event's data arrives as JSON on stdin; exit 0 reports no objection (and, for a few events, injects stdout into the model's context as plain text), exit 2 blocks the action with the stderr message as the reason, and any other exit code is treated as a non-blocking error unless stdout carried a valid JSON object. Printing structured JSON instead of relying on exit codes gives finer control — a `PreToolUse` hook can return `permissionDecision` of `allow`, `deny`, or `ask` with a reason fed back to the model, and a `UserPromptSubmit` hook can inject text through `hookSpecificOutput.additionalContext`. The documentation is explicit that the two styles should not be mixed within one hook.

When several hooks match the same event they all run in parallel and all run to completion — one hook returning `deny` does not suppress a sibling's side effects. Their outputs are then combined, with the most restrictive permission decision winning in the order `deny`, `defer`, `ask`, `allow`, and injected context kept from every hook.

Where a hook is registered determines its scope, and the documented locations span personal settings, project settings, gitignored local settings, organisation-wide managed policy, plugins, and — notably — the frontmatter of an individual [[DefinedTerm/agent-skills]] definition or [[DefinedTerm/subagents]] definition. The two differ in how long the registration lasts: a hook declared in skill frontmatter stays active for the rest of the session once the skill is invoked, while one declared in subagent frontmatter applies only while that subagent is running.

The documentation is also direct about the mechanism's limits. A `PostToolUse` hook cannot undo anything, because the tool has already run. Command hooks can only speak through stdout, stderr, and exit codes — they cannot trigger slash commands or tool calls. And timeouts differ by handler type, with `command`, `http`, and `mcp_tool` hooks defaulting to ten minutes, `prompt` hooks to thirty seconds, and `agent` hooks to sixty.

## Related Terms

Hooks are one of the repository-level configuration mechanisms surveyed under [[DefinedTerm/context-files]] and catalogued for [[SoftwareApplication/claude-code]] and [[SoftwareApplication/kiro]]. As a way of forcing a check to run, they overlap with [[DefinedTerm/backpressure]]; where the check itself is another model invocation rather than a script, see [[DefinedTerm/llm-as-judge]] — the `prompt` and `agent` handler types are that pattern implemented directly inside the hook mechanism.
