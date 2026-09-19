---
title: "Agentic Coding Hooks: Deterministic AI Guardrails"
type: "schema:BlogPosting"
lang: en
tags: [agents, agent-safety, guardrails, tool-use, coding-tools]
sources:
  - type: url
    url: 'https://ranthebuilder.cloud/blog/agentic-coding-hooks-deterministic-ai-guardrails/'
    hash: sha256:b03d933cae09c988639708be54c8b08e5373a0ebad3eb20a54c3369babab0a3e
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A practitioner post arguing that everything fed to a coding agent through its context window is a suggestion rather than a guarantee, and that hooks — code the runtime executes, not the model — are the layer to use for the small set of rules that must hold every time."
  author: ["Ran Isenberg"]
  datePublished: "2026-06-23"
---

The post's organising claim is that agent instructions are probabilistic. The author writes that
`CLAUDE.md` conventions, skills, and prompts compete for the model's attention, and that compliance
tends to drop as sessions grow longer — acceptable for code style preferences, and not acceptable when the
instruction is what protects a secrets folder, a production configuration file, or a CI/CD standard.
The author is explicit that better instructions help and that encoding domain expertise into the
agent's context remains high-impact, but holds that no prompt is deterministic.

From that the post draws a division of labour. [[DefinedTerm/agent-hooks]] are code the runtime
executes at fixed points in the agent's lifecycle, so the model does not get to decide whether they
run; that makes them a deterministic counterweight to the agent's non-deterministic nature. The
treatment is centred on [[SoftwareApplication/claude-code]], which the author describes as having the
deepest hooks implementation available; a later section surveys how the same idea has spread across
other agents and IDEs, and the post ends by arguing for using hooks sparingly.

## Key Points

- Everything supplied to an agent through its context window is a suggestion, not a guarantee, and compliance tends to degrade over a long session.
- Hooks are the deterministic layer because the runtime, not the model, decides whether they run; a hook is ordinary code and behaves identically every time.
- Of the three handler kinds, the author argues shell scripts are the right tool: an HTTP endpoint depends on a network call that can time out, and an LLM prompt hook is non-deterministic by nature, which is exactly what a guardrail cannot afford.
- `PreToolUse` carries most of the guardrail value, because it receives the full tool call as JSON before anything executes and can allow it, deny it with a reason fed back to the model, escalate to a permission prompt, or rewrite the tool input.
- A denied `PreToolUse` is a hard stop since the call never executes, whereas a blocked `Stop` feeds the reason back to the model and asks it to continue — a strong nudge rather than a guarantee.
- The two `PreToolUse` decision mechanisms fail in opposite directions: malformed JSON on `stdout` is never parsed and the call slips through (fails open), while `exit 2` blocks regardless of what `stdout` contains (fails closed). The author reserves `exit 2` for the critical few.
- Where a hook is placed is the scope of the policy: user settings for a personal safety net, the project's `.claude/settings.json` for a team standard, managed policy settings for an organisational guardrail.
- A hook is code the runtime executes automatically with the user's permissions, and a `SessionStart` hook runs on opening a project — so whoever can write to a settings file controls what runs on that machine. The author cites an April 2026 PyPI worm that planted a malicious `SessionStart` hook in repository settings, and advises reviewing the `.claude` folder of a cloned repository before opening it.
- The author advises against wrapping every action in a hook: hooks run inside the agent loop and every matching tool call pays the cost of spawning the script. The stated rule of thumb is to reserve them for destructive commands, secrets and sensitive paths, and the one or two CI/CD standards that must always hold.
- The post's framing of the purpose: a hook is not there to control the agent but to make a handful of unwanted outcomes impossible, so the agent can be allowed to move fast.

## Notes

The post reports two incidents as evidence that the file-access cases are not theoretical — a
developer who published a collection of safety hooks after the agent attempted `rm -rf ~/`, and
another who found the agent had copied production credentials into a file that was committed. Both
are described as community reports rather than the author's own experience.

On convergence across the ecosystem, the post reports that Cursor introduced hooks in version 1.7
with `preToolUse` and `beforeReadFile` events, kept the same exit-code semantics, and will load an
existing Claude Code hook configuration; that Cursor also added prompt-based hooks in which a fast
model evaluates a natural-language condition, an idea the author notes is sometimes called semantic
hooks; that OpenAI Codex added experimental hooks behind a feature flag, with five events
mirroring Claude Code's naming; and that Gemini CLI and GitHub Copilot CLI shipped hook systems of
their own. The author's reading is that Claude Code's design — JSON on `stdin`, `exit 2` to block —
has become the de facto convention.
