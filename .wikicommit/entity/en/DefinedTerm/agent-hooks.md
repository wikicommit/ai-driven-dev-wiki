---
title: "Agent Hooks"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agent-safety, tool-use]
sources:
  - type: url
    url: 'https://ai.google.dev/gemini-api/docs/agent-hooks'
    hash: sha256:f79707693b6ab1cdff0b59d925597d980c9bf9c441da28a1505c1a9f80407641
  - type: url
    url: 'https://dev.to/aws/ai-agent-guardrails-rules-that-llms-cannot-bypass-596d'
    hash: sha256:d321340a9dfb2556bc45605cd43311d6f886dd3c139f618c6380e18345aa7a1a
  - type: url
    url: 'https://ranthebuilder.cloud/blog/agentic-coding-hooks-deterministic-ai-guardrails/'
    hash: sha256:b03d933cae09c988639708be54c8b08e5373a0ebad3eb20a54c3369babab0a3e
  - type: url
    url: 'https://www.anthropic.com/engineering/claude-code-best-practices'
    hash: sha256:9aae24f8b850a5f9c8a6f561be1fecf54f29e1ddc4658d00ecded22bccb82b82
  - type: url
    url: 'https://toss.tech/article/52631'
    hash: sha256:8e01a448bd2676b5a47e3ed4d8360ee248c40091ecec973ede57f55edea8cba1
  - type: url
    url: 'https://claude.com/blog/steering-claude-code-skills-hooks-rules-subagents-and-more'
    hash: sha256:bb67b24e7e743610aadc45e492a9035d66952bb3cadff52ef8301bc773391708
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A mechanism that lets a developer run custom logic — an external script, an HTTP callback, or an in-process framework callback — immediately before or after an AI agent executes a tool call, so the call can be approved, blocked, or followed up on."
---

Agent hooks let a developer intercept an AI agent's tool calls, running custom logic right before or right after a call executes so that the call can be approved, blocked, or followed up on. The mechanism appears both as external configuration a runtime reads and as an in-process callback API an agent framework exposes; Google's Gemini API implements the first as a `hooks.json` configuration that groups event definitions under named rules, matched against tool names using standard RE2 regular expressions, while [[SoftwareApplication/strands-agents]] implements the second as callbacks registered against framework lifecycle events.

What the mechanism is *for* is stated most directly in [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]]: because the runtime rather than the model decides whether a hook runs, a rule enforced in a hook holds every time, where the same rule written into a prompt or a context file is a suggestion the model may or may not follow on a given turn. That post presents hooks as the deterministic counterweight to an agent's probabilistic instruction-following, and reserves them for the small set of rules that must not depend on how the model reads its context.

## Usage

In Google's Gemini API, a hook fires on one of two lifecycle events: `pre_tool_execution`, which runs before a tool call and can approve (`allow`) or block (`deny`) it before it runs — when blocked, the model sees the rejection reason and can adapt — or `post_tool_execution`, which runs after a call completes and can only perform follow-up work such as formatting code, running tests, or logging telemetry, since it cannot undo or block an action that already happened. Each rule group names a `matcher` (a regular expression matched against tool names such as `code_execution`, `read_file`, or `write_file`) and an ordered list of `hooks` to run when it matches; a hook is either a `command` (runs inside the sandbox, reading the event as JSON on stdin and writing its decision to stdout) or an `http` handler (posts the event to an external HTTPS endpoint through the sandbox's egress proxy, which can inject authentication headers on outgoing requests so secrets never need to be stored in the hook configuration itself). If a command script crashes, an HTTP hook returns a non-2xx status, or a hook times out or returns unrecognized output, the runtime treats it as an approval rather than blocking the call, so a broken hook never deadlocks the agent. In Gemini API's implementation, hooks are scoped to the sandbox's own built-in tools (code execution and filesystem operations) and do not fire for custom function-calling tools or external MCP-server tools handled outside the container.

The same pre-execution interception appears as an in-process API in [[SoftwareApplication/strands-agents]], where a `HookProvider` registers a callback against `BeforeToolCallEvent` through a `HookRegistry`. The callback receives the pending call's name and input and blocks it by assigning a message to `event.cancel_tool`, which the framework returns to the model in place of the tool's result. What the post describing it draws from that arrangement is an argument about where enforcement belongs: because the callback runs outside the model, a rule evaluated there is not something the model can reinterpret, unlike the same rule written into a prompt or a tool docstring. That use is developed under [[DefinedTerm/neurosymbolic-validation]].

[[SoftwareApplication/claude-code]] is described in [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] as having shipped hooks ahead of its competitors and as still having the deepest implementation among AI coding agents, with a reference documenting thirty events in total, covering permission requests, subagent lifecycle, context compaction, configuration changes, and file-watching. That post groups them by cadence: some fire once per session (`SessionStart`, `SessionEnd`), some once per conversation turn (`UserPromptSubmit`, `Stop`), and the ones it treats as most useful fire on every tool call inside the agentic loop — `PreToolUse` before a tool executes, `PostToolUse` after it succeeds. A `PreToolUse` hook receives the tool call as JSON on `stdin`, including the exact command or file path about to be touched, and can allow the call, deny it with a reason fed back to the model, escalate to a permission prompt, or rewrite the tool input before it runs.

Claude Code's two decision mechanisms are documented in that post as alternatives that fail in opposite directions. A hook may signal through its exit code — `exit 2` blocks the call and feeds `stderr` back to the model as the reason, `exit 0` reports no decision — or it may `exit 0` and print a `hookSpecificOutput` block carrying a `permissionDecision` of `allow`, `deny`, or `ask`. Since the JSON is only read when the script exits `0`, a malformed deny is never parsed and the call proceeds, so the JSON path fails open, while `exit 2` blocks whatever `stdout` contains and so fails closed. The post's own practice is to use `exit 2` for the cases where a command must never run, and the JSON form where a clear message or a softer outcome matters more; it also cautions that `exit 2` means different things on different events.

Anthropic's own Claude Code documentation states the same enforcement argument in one line —
CLAUDE.md instructions are advisory, hooks are deterministic and guarantee the action happens — and
describes using hooks to gate when a turn is allowed to *end*. A `Stop` hook
runs a check as a script and, in that documentation's words, blocks the turn from ending until it
passes — putting a test suite or build between the agent and declaring itself done. How firm that
is depends on which of this page's sources is asked:
[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] cautions that a blocked `Stop`
feeds the reason back to the model and asks it to continue, and calls it a strong nudge rather than
an absolute guarantee. The documentation also records a ceiling: Claude Code overrides the hook and
ends the turn after eight consecutive blocks. The same
documentation notes that hooks can be written by the agent itself on request.

An Anthropic post dated June 18, 2026, [[BlogPosting/steering-claude-code]], places hooks among the seven ways of
instructing Claude Code and explains their position there by context cost rather than by enforcement
alone. It describes hooks as user-defined commands, HTTP endpoints or LLM prompts, registered in
`settings.json`, in managed policy settings, or in a skill's or subagent's frontmatter, and lists five
types — command, HTTP, `mcp_tool`, prompt and agent. All are triggered deterministically; the first
three also execute deterministically, while prompt and agent hooks use Claude's judgment rather than a
set of rules to determine their output. Because a hook's configuration lives outside the main
context window — the harness runs the handler for command, HTTP and `mcp_tool` hooks, and makes model
calls in separate windows for prompt and agent hooks — the post counts hooks as low in context cost and
as bypassing [[DefinedTerm/compaction]] entirely. The corollary it draws is that most hook output never reaches the
main context unless the configuration returns it: a blocking hook's standard error is kept so Claude
knows why a call was denied, but if a `PreCompact` hook backs up the chat history to a file, Claude
would not know which file holds it.

A use that neither decides nor blocks anything is described in
[[BlogPosting/making-ai-follow-team-rules]], where hooks carry team coding conventions into the
agent rather than policing its tool calls. The plugin that post describes,
[[SoftwareApplication/pfmls-stylepack]], hooks two moments inside the agent loop: immediately after
the agent writes a file, where it reads that file's body and injects at most two matching
convention rules as text, and again as the agent tries to finish, where it reads the whole change
as a `git diff` and injects at most four. It hooks session start as well, though for a different
job — injecting team-wide context chosen by the repository's language environment, and pulling the
current rules from a central repository in the background. The text injected at the second point says of itself that it is a reminder to review
rather than a hard failure, and the agent decides what to do with it. That post's argument for the
placement is positional rather than about enforcement: rules supplied once at the start of a
session stop being applied as the session lengthens, which it attributes to
[[DefinedTerm/lost-in-the-middle]], so the rule is re-supplied next to the code it applies to. It
also reports a constraint that follows from hooking every file write — the hook has to return
immediately, so rule selection is done with filename patterns and regular expressions, an earlier
model-based relevance check having cost about ten seconds per request.

## When It Applies

Hooks apply where an outcome must be impossible rather than merely discouraged. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] names the recurring cases as destructive shell commands, access to `.env` files, secrets and production configuration, and the one or two CI/CD standards an organisation depends on; the most common hook in practice, it reports, is the least dramatic one — a `PostToolUse` formatter and linter run after every file edit.

In the same post, placement is the scope of the policy: user settings for a personal, machine-wide safety net, the project's committed `.claude/settings.json` for a team standard, and administrator-controlled managed policy settings for an organisational guardrail. That placement is also a security question, the post argues. A hook is code the runtime executes automatically with the user's permissions, and a `SessionStart` hook runs the moment a project is opened, before anything is typed — so anything that can write to a settings file can plant code that runs. The post cites an April 2026 PyPI worm that planted a malicious `SessionStart` hook in repository settings, and advises treating settings files the way CI configuration is treated: review every change, and review a cloned repository's `.claude` folder before opening it.

The post also argues against over-use on cost grounds — hooks run inside the agent loop, so every matching tool call pays for spawning the script — and holds that everything outside the critical few belongs in prompts and skills, where an occasional miss is annoying rather than dangerous. How well-established the practice is can be read from its spread: the post reports that Cursor shipped hooks in version 1.7 keeping the same exit-code semantics, that Gemini CLI and GitHub Copilot CLI shipped their own hook systems, and that OpenAI Codex added experimental hooks behind a feature flag with five events mirroring Claude Code's naming — with Claude Code's JSON-on-`stdin` and `exit 2`-to-block design becoming the de facto convention.

[[BlogPosting/steering-claude-code]], the Anthropic post on where Claude Code instructions belong, turns
the enforcement argument into a placement rule. An instruction phrased "every
time X, always do Y" in [[DefinedTerm/claude-md]] belongs in a hook instead, because the model
choosing to run a formatter is different from the formatter running automatically; and "never do
this" is the wrong job for an instruction at all, since under pressure, in a long session, in an
ambiguous situation or through a prompt injection in a file it reads, the model can fail to follow a
prompted rule. That post names hooks and permissions as the enforcement methods, and managed settings —
admin-deployed and not overridable by a user's local configuration — as the only way to enforce a
deterministic organisation-wide guardrail.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/guardrails]], [[DefinedTerm/neurosymbolic-validation]], [[DefinedTerm/tool-use-design-pattern]], [[SoftwareApplication/strands-agents]], [[SoftwareApplication/claude-code]], [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]], [[SoftwareApplication/pfmls-stylepack]], [[DefinedTerm/lost-in-the-middle]], [[DefinedTerm/claude-md]], [[BlogPosting/steering-claude-code]]
