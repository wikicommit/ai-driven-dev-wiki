---
title: "Loop Engineering"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/loop-engineering/'
    hash: sha256:aa188c2fd5951b4662d056122bce224b571a90019a5babf31589c75238b358e1
  - type: url
    url: 'https://techblog.zozo.com/entry/loop-engineering-prompt-tuning'
    hash: sha256:880fb71e74e5d9aa9b6c299e1c29e88f42a7f80015910db287c39b2a378226b4
  - type: url
    url: 'https://arxiv.org/pdf/2608.21884'
    hash: sha256:56268a33af13d85aafed774b47a06d244855bbba6f3a42fd54400c1a78c0c418
  - type: url
    url: 'https://github.com/cobusgreyling/loop-engineering'
    hash: sha256:df92990337d4e1373522192c1477d3c64cc7549531858bec90092f054ee4a84b
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The practice of designing an automated system — scheduled automations, isolated worktrees, skills, connectors, and a maker/checker split between sub-agents — that prompts and checks a coding agent on your behalf, rather than prompting the agent directly turn by turn. A second account frames it as the control plane one level above the harness: the harness is everything around the model, and loop engineering is designing that harness to keep running itself against a stopping condition or a scheduler. An academic review of the practitioner discourse defines it as designing automated control structures that repeatedly invoke coding agents on a schedule or on events, with each run bounded by a machine-checkable stop condition."
---

Loop engineering is the practice of designing a system that prompts a coding agent on your behalf, rather than prompting the agent directly, turn by turn. Where ordinary agent use has a person type an instruction, read the result, and type the next instruction, a loop is a small system that finds the work, hands it to the agent, checks what came back, records what was done, and decides the next step — with the person designing that system once rather than operating it continuously. It is described as sitting one level above [[DefinedTerm/harness-engineering]]: a harness shapes the environment a single agent runs inside, and a loop runs that harness on a schedule, spawning helper agents and feeding itself new work. A second account puts the same relation in terms of the harness itself — everything around the model other than the model, meaning the system prompt, tools, permissions, context management, verification loops and logs — and describes loop engineering as a control plane one level up that designs that harness to keep going autonomously against stopping conditions or a scheduler. The shift it names is the same in both: you stop prompting the model yourself and start designing the loop that prompts it.

An exploratory academic study, [[ScholarlyArticle/loop-engineering-building-blocks-adoption-and-impact]], consolidates the practitioner discourse into a working definition: loop engineering is the practice of designing automated control structures that repeatedly invoke coding agents, triggered on a schedule or by events, with each run bounded by a machine-checkable stop condition — and a well-engineered loop additionally persists state across runs, verifies results independently of the implementing agent, bounds inference costs, restricts what an unattended run may change without approval, and defines when humans should intervene. That study frames the lineage as four layers distinguished by their unit of concern: prompt engineering (one instruction), context engineering (one model call), harness engineering (one agent run) and loop engineering (recurring runs). It also separates this level of iteration from the agent loop inside a single run, the model's repeated cycle of calling tools and acting on the results.

## Usage

A loop is built from five recurring pieces plus a place to remember state: automations that run on a schedule to discover and triage work; worktrees (isolated working directories on their own branch) so agents running in parallel don't edit the same files; skills that record project-specific knowledge so the agent doesn't have to re-derive it every session; plugins and connectors, generally built on MCP, that let the loop reach real tools such as an issue tracker or a chat channel; and sub-agents split so that the one who writes the work is not the one who checks it, since a model grading its own output tends to be too lenient. The sixth piece is external memory — a markdown file or a Linear board that lives outside any single conversation — since the underlying model forgets everything between runs and this state has to live on disk instead. Both the Codex app and Anthropic's Claude Code are described as now shipping all five pieces, under different names, which is presented as evidence that loop engineering has become a property of the products themselves rather than something each team has to hand-build.

A worked instance outside coding work is reported in [[BlogPosting/loop-engineering-prompt-tuning]], where the loop being automated is prompt tuning for a vision-language model. Its construction method is stated as decomposing what the person was already doing by hand and assigning each step its own component — looking at the failures, diagnosing the cause, rewriting the prompt, re-evaluating, and recording what helped, with the re-evaluation step falling to a plain script and the rest to sub-agents — and a skill file acting purely as orchestrator, a single policy file holding the improvement priorities, accept/reject rules and stopping conditions that every sub-agent follows, and a lessons file the loop appends to after each iteration as the deliberate equivalent of a human tuner's accumulating memory. That account reports the automated loop matching or slightly exceeding hand tuning on the one task where a comparison existed, and cutting the surrounding evaluation cycle from about 3.5 weeks to about one week, from a single run rather than a repeated measurement.

A practitioner-maintained pattern library, the `cobusgreyling/loop-engineering` repository on
GitHub, gives the practice a catalogue of named, ready-to-install loops. It describes itself as a
pattern library "for operating agents around a codebase", explicitly not a button for rewriting a
module, and sums the practice up as "Stop prompting. Design the loop. Get a score." — designing a
system that discovers work, hands it to agents, verifies results and persists state. Its patterns
include daily triage, a thin loop run from GitHub Actions without a state file, a pull-request
babysitter, CI and dependency sweepers, a changelog drafter, post-merge cleanup and issue triage, each
listed with a cadence (from every five to fifteen minutes up to daily) and a relative cost. Each
pattern also names a starting autonomy level, and the library's rollout rule is to move from L1
(report only) to L2 (assisted) to L3 (unattended) only after the verifier has been right for a week;
its tooling weights recent runs over the files on disk when judging readiness, so a month-old
`STATE.md` does not count as L3. A CLI (`npx @cobusgreyling/loop`) initialises a pattern for Claude
Code, Codex, Grok or OpenCode, checks a set-up, and estimates cost, and the repository keeps pages on
failure modes, anti-patterns and safety alongside stories of both wins and failures. Among its
sources it lists Addy Osmani's post ([[BlogPosting/loop-engineering]]), an article of the same title by
its maintainer, and [[ScholarlyArticle/loop-engineering-building-blocks-adoption-and-impact]], and it
states that it is the community reference that study reviewed. Its own warnings match the ones below:
loop engineering amplifies judgment, token costs can explode, and unattended loops make unattended
mistakes.

Evidence on how widely the practice is actually adopted comes from the same study's mining of 36,710 engineered open-source repositories. It confirmed autonomous agent loops in 217 of them, almost all started by GitHub Actions workflows and most running on repository events (typically reviewing each newly opened pull request) rather than on a schedule, with the scheduled loops being mostly issue triage. The committed configuration of these loops was visible, but almost none of the repositories committed the state files the practitioner sources prescribe; the authors observe that in most of the confirmed loops there was either nothing to persist between runs or the issue tracker already held that state.

## When It Applies

It applies to recurring or long-running work that would otherwise require a person to keep re-prompting the agent each cycle — triage, scheduled discovery, or work that continues unattended. It assumes a stopping condition that can actually be checked (e.g. by a verifying model) and durable external state the loop can read and write between runs, since the underlying model itself retains nothing across them. Verification is described as remaining a human responsibility even once the loop is running well: an unattended loop still makes mistakes unattended, and the practice is described as making two other problems sharper rather than solving them — a person's understanding of the shipped code can rot faster if they stop reading what the loop produces, and a well-running loop can tempt someone into accepting its output uncritically. It is presented as a synthesis of practices independently described by other practitioners (Peter Steinberger and Boris Cherny are both quoted describing the same shift toward designing loops rather than prompting agents directly); the five-piece enumeration above is Steinberger's list, and the author's own contribution is to map it onto both the Codex app and Claude Code and work through each piece in turn.

The prompt-tuning account adds two cautions of its own, both about what an unattended loop does when it is working. Because each iteration re-ran inference over the whole dataset, API charges accumulated, and it notes that a badly designed loop can keep inferring in the background and drive costs up unexpectedly, recommending that a change be tried on a small sample first and evaluated over the full dataset only when that run looks promising. And because the loop optimizes against whatever it is scored on, the artifact it was editing grew steadily longer as accuracy rose; that account names overfitting as the thing it watched most closely, on the stated reasoning that the more the wording leans toward the training data the higher the overfitting risk becomes, and recommends holding out a test split at minimum.

How new the practice is remains disputed. In the discourse that study reviewed, critics describe loops as renamed cron jobs or as event-driven automation with a non-deterministic worker, while others expect explicit loops to be absorbed into built-in tool features such as recurring and goal-driven commands. The study's own reading supports parts of both positions: schedulers, event triggers and self-managing control loops predate the term, and what it treats as new is adoption as a developer practice — placing a non-deterministic worker behind natural-language goal conditions and verification-governed termination, which moves the engineering effort into bounding it with guardrails, budgets, verifiers and escalation policies. It also reports that the claimed benefits rest largely on self-reports and anecdotes, that the reviewed sources catalogue failure modes such as runaway costs, infinite fix loops and verifiers that approve without real checks, and that the staged-adoption advice common across those sources — design an independent verification step first, then move from report-only to unattended operation — is, to the authors' knowledge, untested.

## Related Terms

[[DefinedTerm/prompt-engineering]], [[DefinedTerm/context-engineering]], [[DefinedTerm/harness-engineering]], [[DefinedTerm/agent-harness]], [[DefinedTerm/sub-agent-architecture]], [[SoftwareApplication/claude-code]]
