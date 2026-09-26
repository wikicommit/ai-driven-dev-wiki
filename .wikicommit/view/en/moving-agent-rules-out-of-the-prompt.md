---
title: "Moving agent rules out of the prompt into deterministic enforcement"
lang: en
kind: pattern
review_status: pending
generated_at: "2026-09-26"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails.md
    source_commit: 4f77e325763ffd426899b2d1578846aeec73017c
  - path: .wikicommit/entity/en/BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass.md
    source_commit: 4f77e325763ffd426899b2d1578846aeec73017c
  - path: .wikicommit/entity/en/BlogPosting/claude-code-hooks-complete-guide.md
    source_commit: 74c6840463d960cf5b82c76818ec6b07f5f7233d
  - path: .wikicommit/entity/en/BlogPosting/steering-claude-code.md
    source_commit: f98378c1c0274db465979eeb9b19989edbed4da1
  - path: .wikicommit/entity/en/BlogPosting/making-ai-follow-team-rules.md
    source_commit: 4f77e325763ffd426899b2d1578846aeec73017c
  - path: .wikicommit/entity/en/BlogPosting/verify-ai-agent-coding-rules-with-archunit.md
    source_commit: 4f77e325763ffd426899b2d1578846aeec73017c
  - path: .wikicommit/entity/en/DefinedTerm/deterministic-quality-gate.md
    source_commit: 4f77e325763ffd426899b2d1578846aeec73017c
  - path: .wikicommit/entity/en/DefinedTerm/agent-hooks.md
    source_commit: 74c6840463d960cf5b82c76818ec6b07f5f7233d
  - path: .wikicommit/entity/en/SoftwareApplication/agent-governance-toolkit.md
    source_commit: 4f77e325763ffd426899b2d1578846aeec73017c
  - path: .wikicommit/entity/en/BlogPosting/writing-a-good-claude-md.md
    source_commit: 8e44cc8042b43f8d5552cfe8212a0f427fe92366
---

Several pages in this wiki describe the same move. A rule that an AI agent is meant to follow starts out as text in its context: a line in [[DefinedTerm/claude-md]], a Markdown rule document, a tool docstring, a system prompt. Each account then finds that the text is not reliably followed. The rules that have to hold every time are moved out of the context and into a mechanism the model does not get to decide whether to run: a hook, a permission rule, a CI check, a test, or a policy engine in application code. This page describes that recurring shape, the reasons the pages give for it, and the limits they record.

## The shape, and where it appears

Nine of the ten pages behind this view state the shape directly, and one describes a variation on it:

1. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]]: everything supplied through the context window "is a suggestion, not a guarantee". Hooks are presented as the deterministic layer because the runtime, not the model, decides whether they run.
2. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]]: business rules in docstrings or system prompts are context the model interprets and re-decides on every call. A framework-level hook that cancels the call is presented as the enforcement.
3. [[BlogPosting/claude-code-hooks-complete-guide]]: "A system prompt is a request. A hook is a guarantee."
4. [[BlogPosting/steering-claude-code]]: "every time X, always do Y" belongs in a hook, and "never do this" is the wrong job for an instruction. Hooks and permissions are named as the deterministic enforcement methods.
5. [[BlogPosting/writing-a-good-claude-md]]: "Claude is not a linter". Deterministic formatters and linters, run for example from a `Stop` hook, do that job instead of instructions in the file.
6. [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]]: coding rules written as Markdown for an agent are compiled, where they can be expressed structurally, into ArchUnit tests run as a required CI gate.
7. [[DefinedTerm/deterministic-quality-gate]]: after pull requests were merged with tests not passing, tests are run by a `SubagentStop` hook and a GitHub Action instead of being a step in the agent's own workflow.
8. [[SoftwareApplication/agent-governance-toolkit]]: prompt-level safety is described as "a polite request to a stochastic system". Policy is enforced in deterministic application code that intercepts every tool call, message and delegation.
9. [[DefinedTerm/agent-hooks]]: this page collects the argument from several of the pages above, so it restates their evidence rather than adding a separate case. What it adds is a record of Anthropic's Claude Code documentation saying in one line that CLAUDE.md instructions are advisory while hooks are deterministic.
10. [[BlogPosting/making-ai-follow-team-rules]] is the variation described in the last section. It moves team rules out of the start of the session and into hooks, but what the hooks deliver is still text the agent may act on or ignore.

The pages come from different kinds of source: an AWS post on DEV Community, practitioner blogs, Anthropic's own guidance about its product, a HumanLayer post, engineering posts from ZOZO and Toss, one engineer's post from two infrastructure projects, and a Microsoft repository. Several of them centre on [[SoftwareApplication/claude-code]], and the hook conventions they describe are largely that tool's.

## Why the pages treat instructions as suggestions

The pages agree that an instruction in context is not binding. They give different reasons for it:

- **Degradation over a session.** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] says compliance tends to drop as sessions grow longer, because CLAUDE.md conventions, skills and prompts compete for the model's attention. [[BlogPosting/making-ai-follow-team-rules]] reports that the agent followed rules in the root instruction file early in a session and stopped later, and attributes this to [[DefinedTerm/lost-in-the-middle]].
- **Too many instructions.** [[BlogPosting/writing-a-good-claude-md]] argues that models follow only a limited number of instructions consistently, and that adding more makes instruction-following worse across all of them. [[BlogPosting/steering-claude-code]] says an unowned, growing CLAUDE.md dilutes adherence to the instructions that matter.
- **The model reinterprets the rule on every call.** [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] gives a worked example: an agent read a docstring saying payment must be verified first, confirmed the booking anyway, and reported success.
- **Pressure, ambiguity and injection.** [[BlogPosting/steering-claude-code]] lists pressure, long sessions, ambiguous situations and a prompt injection in a file the model reads as ways a prompted rule can fail. [[SoftwareApplication/agent-governance-toolkit]] points to prompt-injection guidance and adaptive-attack results as evidence that model-layer defences stay probabilistic.
- **Load on reviewers.** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] makes a different argument. Agents produce code quickly, so violations arrive at the same rate, and checking by eye makes the reviewer's load grow without limit. Its claim is that executable rules let verification keep pace with generation. [[DefinedTerm/deterministic-quality-gate]] likewise reports that reviewers no longer needed to confirm by hand that tests had passed.

## Where the rule moves to

Across the pages, the destination varies with where in the workflow the rule has to hold:

- **Before a tool call.** A `PreToolUse` hook in Claude Code or a `BeforeToolCallEvent` hook in [[SoftwareApplication/strands-agents]] sees the pending call and can block it. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] credits most of a hook's guardrail value to this point. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] notes that cancelling before execution leaves nothing to roll back.
- **At the end of a turn or subagent.** `Stop` and `SubagentStop` hooks put a test suite, a build or a linter between the agent and finishing ([[DefinedTerm/deterministic-quality-gate]], [[BlogPosting/writing-a-good-claude-md]], [[DefinedTerm/agent-hooks]]).
- **In the permission system and managed settings.** [[BlogPosting/steering-claude-code]] names managed settings as the only way to enforce an organisation-wide guardrail. [[BlogPosting/claude-code-hooks-complete-guide]] describes the layers as "`CLAUDE.md` persuades, permissions filter, hooks enforce-and-react", with a hardened setup running all three.
- **In CI.** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] makes the rule-checking job a required status check so a violating pull request cannot merge. [[DefinedTerm/deterministic-quality-gate]] runs the tests in a GitHub Action before merge.
- **In application middleware.** [[SoftwareApplication/agent-governance-toolkit]] wraps tool functions with a YAML policy that is evaluated on every call. It writes each decision to an audit trail and raises an exception when the policy denies the action.

The destinations also differ in who owns the rule. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] treats a hook's placement as its scope: user settings for a personal safety net, the project's settings for a team standard, and managed policy settings for an organisational guardrail.

## What the pages record as its limits

None of the pages presents the move as total. They record these limits:

- **Only a few rules are moved.** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] reserves hooks for destructive commands, secrets, sensitive paths and one or two CI/CD standards, because every matching tool call pays for spawning the script. [[BlogPosting/claude-code-hooks-complete-guide]] lists over-hooking preferences whose occasional miss would cost little as a pitfall. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] scopes its recommendation to high-stakes operations.
- **Not every rule can be mechanised.** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] says plainly that its method covers constraints about package structure and class relationships, not every natural-language rule. It lets each rule document state which of its constraints are already tested and which still rely on review. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] notes that its rules are boolean and cannot express fuzzy logic.
- **A deterministic check can itself be wrong.** In [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]], the obvious encoding of a rule against reflection also caught generated code that never called a reflection API, and it had to be rewritten. The same page describes the rule document, the test and the code drifting apart, and records keeping them consistent as an open problem.
- **Enforcement can fail open.** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] and [[DefinedTerm/agent-hooks]] describe how, in Claude Code, a hook that answers with malformed JSON is never parsed, so the call goes through, while `exit 2` blocks the call. [[BlogPosting/claude-code-hooks-complete-guide]] lists a guard that exits `1` among its pitfalls, because it lets the action through. [[DefinedTerm/agent-hooks]] records that Gemini API treats a crashed or timed-out hook as an approval.
- **Not every hook is a hard stop.** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] calls a blocked `Stop` a strong nudge rather than a guarantee, since it feeds a reason back and asks the model to continue. [[DefinedTerm/agent-hooks]] records Anthropic's documentation that Claude Code ends the turn anyway after eight consecutive blocks. [[DefinedTerm/agent-hooks]] also records that prompt and agent hook types use the model's judgment to decide their output. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] calls that kind of handler non-deterministic by nature.
- **The mechanism is an attack surface.** A hook is code that runs automatically with the user's permissions. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] cites a PyPI worm that planted a malicious `SessionStart` hook. [[BlogPosting/claude-code-hooks-complete-guide]] treats hooks in a cloned repository like a `Makefile` or `postinstall` script, and calls its own regex-based guard defence in depth rather than a complete boundary.
- **Enforcement sits where the code sits.** [[SoftwareApplication/agent-governance-toolkit]] notes that it enforces at the application middleware layer, not the OS kernel, so the policy engine and the agents it governs share a process.

Several pages also keep a role for instructions. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] says better instructions help and that domain expertise in context remains high-impact. [[BlogPosting/claude-code-hooks-complete-guide]] has CLAUDE.md, permissions and hooks cover the same requirement together.

## A variation: hooks that deliver rules instead of enforcing them

[[BlogPosting/making-ai-follow-team-rules]] starts from the same observation: rules in a root instruction file stop being followed as a session lengthens. It reaches for the same mechanism, [[DefinedTerm/agent-hooks]], but uses it differently. Its plugin, [[SoftwareApplication/pfmls-stylepack]], hooks the point right after a file is written and the point where the agent tries to finish. At each point it injects a few matching convention rules as text next to the code they apply to. It does not block anything, and the end-of-loop text calls itself a reminder to review rather than a hard failure. The page frames its problem as one of *when* and *how many* rules to surface. What moves here is where the rule enters the context, not who decides whether it holds.

The page runs into two of the limits above. Its hooks select rules with filename patterns and regular expressions because a model-based relevance check added about ten seconds per request. It also reports a loosely triggered rule that fired in 21 sessions without leading to a single code change, and argues that wrong feedback teaches the agent to disregard the rules.

## How strong the evidence is

Most of the evidence is one team's or one author's account. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] reports its result on a purpose-built example of two invalid cases and one valid one, and describes it as a worked illustration rather than independent evidence. [[DefinedTerm/deterministic-quality-gate]] is one engineer's report from two projects. [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] reports no measured before-and-after, and the figures in [[BlogPosting/making-ai-follow-team-rules]] come from that team's own logging. [[BlogPosting/steering-claude-code]] is Anthropic's guidance about its own product. What makes this a pattern is how often the same shape recurs across separately authored sources ([[DefinedTerm/agent-hooks]] is the exception, since it is compiled from several of the others), not measured evidence that moving the rules works.
