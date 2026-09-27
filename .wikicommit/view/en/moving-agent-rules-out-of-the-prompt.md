---
title: "Moving agent rules out of the prompt into deterministic enforcement"
lang: en
kind: pattern
review_status: pending
generated_at: "2026-09-27"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"
derived_from:
  - path: .wikicommit/entity/en/BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/BlogPosting/claude-code-hooks-complete-guide.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/BlogPosting/steering-claude-code.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/BlogPosting/writing-a-good-claude-md.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/BlogPosting/skill-issue-harness-engineering-for-coding-agents.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/BlogPosting/verify-ai-agent-coding-rules-with-archunit.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/DefinedTerm/deterministic-quality-gate.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/SoftwareApplication/agent-governance-toolkit.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/ScholarlyArticle/agentspec.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/DefinedTerm/fides.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/BlogPosting/entering-the-software-3-0-era.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/DefinedTerm/security-context-file.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/BlogPosting/custom-code-review-rules-for-codex.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/DefinedTerm/agent-hooks.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/DefinedTerm/claude-md.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/DefinedTerm/neurosymbolic-validation.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/DefinedTerm/guides-and-sensors.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/BlogPosting/making-ai-follow-team-rules.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
  - path: .wikicommit/entity/en/BlogPosting/build-zero-trust-ai-agents-that-judge-intent.md
    source_commit: 3acdc9ade6f447fb5a86d75bc16afdb9f5f7d5fa
---

Many pages in this wiki describe the same move. A rule that an AI agent is meant to follow starts out as text in its context: a line in [[DefinedTerm/claude-md]] or [[DefinedTerm/agents-md]], a Markdown rule document, a tool docstring, a system prompt. Each account then finds that the text is not reliably followed. The rules that have to hold every time are moved out of the context and into a mechanism the model does not get to decide whether to run: a hook, a permission rule, a CI check, a test, a script, or a policy engine in application code. This page describes that recurring shape, the reasons the pages give for it, which rules they move and which they leave in place, and the limits they record.

## The shape, and where it appears

Twenty-one pages sit behind this view. Fifteen state the shape from their own source:

1. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]]: everything supplied through the context window "is a suggestion, not a guarantee". Hooks are presented as the deterministic layer because the runtime, not the model, decides whether they run.
2. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]]: business rules in docstrings or system prompts are context the model interprets and re-decides on every call. A framework-level hook that cancels the call is presented as the enforcement.
3. [[BlogPosting/claude-code-hooks-complete-guide]]: "A system prompt is a request. A hook is a guarantee."
4. [[BlogPosting/steering-claude-code]]: "every time X, always do Y" belongs in a hook, and "never do this" is the wrong job for an instruction. Hooks and permissions are named as the deterministic enforcement methods.
5. [[BlogPosting/writing-a-good-claude-md]]: "Claude is not a linter". Deterministic formatters and linters, run for example from a `Stop` hook, do that job instead of instructions in the file.
6. [[BlogPosting/skill-issue-harness-engineering-for-coding-agents]]: written after a year of watching coding agents ignore instructions, it gives hooks the job of deterministic control flow. Its example hook runs a formatter and type checks when Claude stops and returns exit code 2 on failure, so the harness makes the agent fix the errors.
7. [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]]: coding rules written as Markdown for an agent are compiled, where they can be expressed structurally, into ArchUnit tests run as a required CI gate.
8. [[DefinedTerm/deterministic-quality-gate]]: after pull requests were merged with tests not passing, tests are run by a `SubagentStop` hook and a GitHub Action instead of being a step in the agent's own workflow.
9. [[SoftwareApplication/agent-governance-toolkit]]: prompt-level safety is described as "a polite request to a stochastic system". Policy is enforced in deterministic application code that intercepts every tool call, message and delegation.
10. [[ScholarlyArticle/agentspec]]: a domain-specific language whose rules are evaluated by an enforcement layer that hooks the agent's decision loop. The paper contrasts it with NVIDIA's NeMo, which applies natural-language constraints at the dialogue level, and with GuardAgent, which relies on an LLM to interpret the constraints; AgentSpec keeps enforcement external to the model.
11. [[DefinedTerm/fides]]: a Microsoft architecture decision record rejects prompt-engineering defences against prompt injection as non-deterministic and bypassable, and proposes labels enforced by middleware that checks policy before a call executes.
12. [[BlogPosting/entering-the-software-3-0-era]]: deterministic logic such as a branch-naming convention should be moved into scripts, so the model runs a script instead of interpreting the convention and spending tokens on it each time.
13. [[DefinedTerm/security-context-file]]: a file of security rules loaded into every session is paired with SAST, credential scanning and infrastructure validation that must pass before deployment, "with no reliance on prompt instructions alone".
14. [[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]]: after measuring how coding agents handle the AI-contribution rules that open-source communities write down, the authors recommend enforcing bans and human-approval rules outside the agent: a CI check that blocks the merge, required human review, or a bot that closes AI-authored pull requests.
15. [[BlogPosting/custom-code-review-rules-for-codex]]: repository rules in `AGENTS.md` are positioned as complementing tests and linters, not replacing them. Deterministic and mechanical checks stay in those tools and in CI, and tests, branch protections and required approvals continue to provide hard enforcement.

Three pages compile the shape from several sources, so they restate evidence rather than add separate cases:

16. [[DefinedTerm/agent-hooks]] gathers the argument from several of the pages above. What it adds is Anthropic's Claude Code documentation saying in one line that CLAUDE.md instructions are advisory while hooks are deterministic.
17. [[DefinedTerm/claude-md]] draws on [[BlogPosting/steering-claude-code]], [[BlogPosting/writing-a-good-claude-md]] and Claude Code's memory documentation. What it adds from that documentation is that CLAUDE.md is loaded as context rather than as enforced configuration, and that an instruction which must run at a fixed point, such as before every commit, should be written as a hook instead.
18. [[DefinedTerm/neurosymbolic-validation]] names the pattern in [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] and is drawn from that one post.

The remaining three relate to the shape without stating it:

19. [[DefinedTerm/guides-and-sensors]] supplies a vocabulary for it, described in the section on which rules move.
20. [[BlogPosting/making-ai-follow-team-rules]] is a variation, described in its own section below. It moves team rules out of the start of the session and into hooks, but what the hooks deliver is still text the agent may act on or ignore.
21. [[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] records where deterministic controls stop, described in the section on enforcement outside the model.

The pages come from different kinds of source: practitioner blogs, an AWS post on DEV Community, Anthropic's and OpenAI's own guidance about their products, HumanLayer posts, two teams' posts about their own practice (one from Toss Bank), one engineer's post from two infrastructure projects, a Microsoft repository and a Microsoft architecture decision record, a Google Cloud post, an ICSE 2026 paper and an empirical study from Peking University. Several of them centre on [[SoftwareApplication/claude-code]], and the hook conventions they describe are largely that tool's.

## Why the pages treat instructions as suggestions

The pages agree that an instruction in context is not binding. They give different reasons for it:

- **How the instruction is delivered.** [[DefinedTerm/claude-md]] records Claude Code's documentation explaining that CLAUDE.md content is delivered as a user message after the system prompt, so there is no guarantee of strict compliance, especially for vague or conflicting instructions. [[BlogPosting/writing-a-good-claude-md]] reports that the file is injected with a system reminder saying it may or may not be relevant, so Claude ignores content it judges irrelevant to the current task.
- **Degradation over a session.** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] says compliance tends to drop as sessions grow longer, because CLAUDE.md conventions, skills and prompts compete for the model's attention. [[BlogPosting/making-ai-follow-team-rules]] reports that the agent followed rules in the root instruction file early in a session and stopped later, and attributes this to [[DefinedTerm/lost-in-the-middle]].
- **Too many instructions.** [[BlogPosting/writing-a-good-claude-md]] argues that models follow only a limited number of instructions consistently, and that adding more makes instruction-following worse across all of them. [[BlogPosting/steering-claude-code]] says an unowned, growing CLAUDE.md dilutes adherence to the instructions that matter.
- **The model reinterprets the rule on every call.** [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] gives a worked example: an agent read a docstring saying payment must be verified first, confirmed the booking anyway, and reported success. [[BlogPosting/entering-the-software-3-0-era]] gives a cost version of the same point: interpreting a convention spends tokens every time.
- **The agent never reads the rule.** In [[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]], the repository's policy file was opened in 12 of 347 non-anchor unaided runs, and 242 of 248 unaided violations happened without it ever being opened.
- **Some rules are resisted even when read.** The same study found that quoting a ban verbatim in `AGENTS.md` left refusal at 0% for three of four agents and moved the fourth to 10%, and one round of feedback naming the violation raised refusal to at most 23%. Its authors summarise the pattern as agents following instructions that extend their work but resisting instructions that undo it.
- **Pressure, ambiguity and injection.** [[BlogPosting/steering-claude-code]] lists pressure, long sessions, ambiguous situations and a prompt injection in a file the model reads as ways a prompted rule can fail. [[SoftwareApplication/agent-governance-toolkit]] points to prompt-injection guidance and adaptive-attack results as evidence that model-layer defences stay probabilistic. [[DefinedTerm/fides]] rejects prompt-engineering defences as bypassable, and [[DefinedTerm/security-context-file]] says prompts can be overridden, misunderstood or ignored.
- **Load on reviewers.** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] makes a different argument. Agents produce code quickly, so violations arrive at the same rate, and checking by eye makes the reviewer's load grow without limit. Its claim is that executable rules let verification keep pace with generation. [[DefinedTerm/deterministic-quality-gate]] likewise reports that reviewers no longer needed to confirm by hand that tests had passed.

## Where the rule moves to

Across the pages, the destination varies with where in the workflow the rule has to hold:

- **Before a tool call.** A `PreToolUse` hook in Claude Code or a `BeforeToolCallEvent` hook in [[SoftwareApplication/strands-agents]] sees the pending call and can block it. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] credits most of a hook's guardrail value to this point. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] and [[DefinedTerm/neurosymbolic-validation]] note that cancelling before execution leaves nothing to roll back.
- **At the end of a turn or subagent.** `Stop` and `SubagentStop` hooks put a test suite, a build, a type check or a linter between the agent and finishing ([[DefinedTerm/deterministic-quality-gate]], [[BlogPosting/writing-a-good-claude-md]], [[BlogPosting/skill-issue-harness-engineering-for-coding-agents]], [[DefinedTerm/agent-hooks]]).
- **In the permission system and managed settings.** [[BlogPosting/steering-claude-code]] names managed settings as the only way to enforce an organisation-wide guardrail. [[BlogPosting/claude-code-hooks-complete-guide]] describes the layers as "`CLAUDE.md` persuades, permissions filter, hooks enforce-and-react", with a hardened setup running all three.
- **In a script.** [[BlogPosting/entering-the-software-3-0-era]] moves deterministic logic into a script the model runs. The logic stops being interpreted, but in this account it is still the model that runs the script.
- **In CI and the merge.** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] makes the rule-checking job a required status check so a violating pull request cannot merge. [[DefinedTerm/deterministic-quality-gate]] runs the tests in a GitHub Action before merge. [[DefinedTerm/security-context-file]] puts scanning gates before deployment, and [[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]] recommends a merge-blocking CI check, required human review, or a bot that closes AI-authored pull requests.
- **In application middleware or a runtime enforcement layer.** [[SoftwareApplication/agent-governance-toolkit]] wraps tool functions with a YAML policy that is evaluated on every call, writes each decision to an audit trail, and raises an exception when the policy denies the action. [[DefinedTerm/fides]] checks policy in middleware before a call executes. [[ScholarlyArticle/agentspec]] hooks the agent's iteration step before an action executes, after it produces an observation, and when the agent completes its task.

The destinations also differ in who owns the rule. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] treats a hook's placement as its scope: user settings for a personal safety net, the project's settings for a team standard, and managed policy settings for an organisational guardrail. [[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] argues that enforcing checks in the platform moves their ownership to a platform or security administrator, separate from the agent developer.

## Which rules move, and which stay

None of the pages moves every rule. Several of them draw the line explicitly, and they draw it in different places:

- **By what a miss costs.** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] reserves hooks for destructive commands, secrets, sensitive paths and one or two CI/CD standards, and leaves everything else to prompts and skills. [[BlogPosting/claude-code-hooks-complete-guide]] lists over-hooking preferences whose occasional miss would cost little as a pitfall. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] scopes its recommendation to high-stakes operations such as bookings, payments and cancellations.
- **By whether the rule can be checked mechanically.** [[BlogPosting/custom-code-review-rules-for-codex]] keeps formatting and other mechanical checks in CI, and uses `AGENTS.md` rules for the judgment that is harder to encode, such as compatibility requirements and data boundaries. [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] compiles only constraints about package structure and class relationships, and lets each rule document state which of its constraints are already tested and which still rely on review.
- **By what kind of rule it is.** [[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]] recommends keeping disclosure and verification rules in the file an agent reads at session start, with a feedback loop, because one round of feedback lifted Verify to 90–100% and Disclose to 81–97% for three of four agents. Bans and human-approval rules, which feedback barely moved, are the ones it sends outside the agent.
- **By when a defect becomes visible.** [[BlogPosting/making-ai-follow-team-rules]] turns defects recognisable from the shape of the code into triggered rules, and leaves defects that appear only at runtime, such as N+1 queries, in always-loaded context.

[[DefinedTerm/guides-and-sensors]] gives a vocabulary that fits these lines. It sorts harness controls into guides, which steer before the agent acts, and sensors, which observe afterwards, and sorts each into computational (deterministic: tests, linters, type checkers) or inferential (AI review, LLM-as-a-judge). Conventions in `AGENTS.md` are its example of an inferential guide, and a hook running ArchUnit tests is its example of a computational sensor. Its account holds that both kinds are needed: feedback alone yields an agent that keeps repeating the same mistakes, and feedforward alone yields one that encodes rules but never finds out whether they worked. [[DefinedTerm/security-context-file]] uses the same terms: the file is an inferential guide, and the deterministic checks and deployment gates must still catch what the agent fails to follow.

Several pages also keep a role for instructions alongside enforcement. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] says better instructions help and that domain expertise in context remains high-impact. [[BlogPosting/claude-code-hooks-complete-guide]] has CLAUDE.md, permissions and hooks cover the same requirement together.

## What the pages record as its limits

The pages record these limits on the move itself:

- **A deterministic rule is only as good as its encoding.** In [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]], the obvious encoding of a rule against reflection also caught generated code that never called a reflection API, and it had to be rewritten. The same page describes the rule document, the test and the code drifting apart, and records keeping them consistent as an open problem. In [[ScholarlyArticle/agentspec]], rules generated by an LLM were sometimes over-rigid for vague requirements; one banned pouring entirely, including watering a houseplant.
- **Boolean rules cannot express everything.** [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] and [[DefinedTerm/neurosymbolic-validation]] note that the rules are boolean, cannot express fuzzy or probabilistic logic, and need a rule written for each protected operation. [[ScholarlyArticle/agentspec]] notes that it enforces at discrete checkpoints and does not reason about the long-term consequences of a sequence of actions.
- **Deterministic checks only catch what was specified in advance.** [[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] starts from this limit: a polite, syntactically valid refund request passes every deterministic gate, and a multi-turn exploit made of individually allowed refunds is invisible to checks that evaluate one request at a time.
- **Enforcement can fail open.** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] and [[DefinedTerm/agent-hooks]] describe how, in Claude Code, a hook that answers with malformed JSON is never parsed, so the call goes through, while `exit 2` blocks the call. [[BlogPosting/claude-code-hooks-complete-guide]] lists a guard that exits `1` among its pitfalls, because it lets the action through. [[DefinedTerm/agent-hooks]] records that Gemini API treats a crashed or timed-out hook as an approval.
- **Not every hook is a hard stop.** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] calls a blocked `Stop` a strong nudge rather than a guarantee, since it feeds a reason back and asks the model to continue. [[DefinedTerm/agent-hooks]] records Anthropic's documentation that Claude Code ends the turn anyway after eight consecutive blocks.
- **The mechanism has costs.** Every matching tool call pays for spawning a hook script ([[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]]). [[DefinedTerm/fides]] lists added latency on every tool call, policies configured by hand, and label propagation that may be overly conservative. [[ScholarlyArticle/agentspec]], by contrast, reports its overhead in milliseconds against agent runs of seconds.
- **The mechanism is an attack surface.** A hook is code that runs automatically with the user's permissions. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] cites a PyPI worm that planted a malicious `SessionStart` hook. [[BlogPosting/claude-code-hooks-complete-guide]] treats hooks in a cloned repository like a `Makefile` or `postinstall` script, and calls its own regex-based guard defence in depth rather than a complete boundary.
- **Enforcement sits where the code sits.** [[SoftwareApplication/agent-governance-toolkit]] notes that it enforces at the application middleware layer, not the OS kernel, so the policy engine and the agents it governs share a process.

## Outside the model is not always deterministic

The pages mostly treat two properties as one: the rule is evaluated outside the model's own decision, and the evaluation is deterministic. A few pages record mechanisms that have the first property without the second:

- [[DefinedTerm/agent-hooks]] records that Claude Code's prompt and agent hook types are triggered deterministically but use the model's judgment to decide their output. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] reports that Cursor added prompt-based hooks in which a fast model evaluates a natural-language condition, and calls an LLM prompt hook non-deterministic by nature, which it says a guardrail cannot afford.
- [[ScholarlyArticle/agentspec]] lists LLM self-examination among its predefined enforcements, alongside user inspection, a predefined action and stopping.
- [[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] adds an LLM-based natural-language policy engine at the gateway, which evaluates each proposed tool call against plain-text business rules before it runs. It presents this as defence in depth alongside the deterministic controls from an earlier post in its series, not as a replacement for them. Its claims are the vendor's own descriptions, demonstrated on a single example transaction.

In these cases the rule returns to natural language, but it is read by a separate check that can stop the call rather than by the agent whose action it governs.

## A variation: hooks that deliver rules instead of enforcing them

[[BlogPosting/making-ai-follow-team-rules]] starts from the same observation: rules in a root instruction file stop being followed as a session lengthens. It reaches for the same mechanism, [[DefinedTerm/agent-hooks]], but uses it differently. Its plugin, [[SoftwareApplication/pfmls-stylepack]], hooks the point right after a file is written and the point where the agent tries to finish. At each point it injects a few matching convention rules as text next to the code they apply to. It does not block anything, and the end-of-loop text calls itself a reminder to review rather than a hard failure. The page frames its problem as one of *when* and *how many* rules to surface. What moves here is where the rule enters the context, not who decides whether it holds.

The page runs into two of the limits above. Its hooks select rules with filename patterns and regular expressions because a model-based relevance check added about ten seconds per request. It also reports a loosely triggered rule that fired in 21 sessions without leading to a single code change, and argues that wrong feedback teaches the agent to disregard the rules.

## How strong the evidence is

Most of the evidence is one team's or one author's account. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] reports its result on a purpose-built example of two invalid cases and one valid one, and describes it as a worked illustration rather than independent evidence. [[DefinedTerm/deterministic-quality-gate]] is one engineer's report from two projects. [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] reports no measured before-and-after, and the figures in [[BlogPosting/making-ai-follow-team-rules]] come from that team's own logging. [[BlogPosting/steering-claude-code]] is Anthropic's guidance about its own product, and the 98% versus 58.3% figure in [[BlogPosting/custom-code-review-rules-for-codex]] is OpenAI's internal evaluation of rules that guide a review, not of rules moved out of the prompt. [[DefinedTerm/fides]] is an architecture decision record with the status *proposed*, and [[DefinedTerm/guides-and-sensors]] is one author's mental model.

Two pages report measurements, and each covers only part of the pattern. [[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]] measures the premise: how often four agent–model pairs follow AI-contribution rules left in a repository's files, on simple issues. It does not measure the CI checks, reviews or bots it recommends. [[ScholarlyArticle/agentspec]] measures runtime enforcement: it reports intercepting risky code executions in over 90% of cases, reducing hazardous tasks for an embodied agent to 0% while safe-task completion fell from 58.62% to 54.26%, and 100% compliance in the tested driving scenarios. Those results concern safety constraints on code, embodied and driving agents rather than a team's coding rules.

What makes this a pattern is how often the same shape recurs across separately authored sources ([[DefinedTerm/agent-hooks]], [[DefinedTerm/claude-md]] and [[DefinedTerm/neurosymbolic-validation]] are the exceptions, since each is compiled from others), not measured evidence that moving the rules works in general.
