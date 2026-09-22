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
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The practice of designing an automated system — scheduled automations, isolated worktrees, skills, connectors, and a maker/checker split between sub-agents — that prompts and checks a coding agent on your behalf, rather than prompting the agent directly turn by turn. A second account frames it as the control plane one level above the harness: the harness is everything around the model, and loop engineering is designing that harness to keep running itself against a stopping condition or a scheduler."
---

Loop engineering is the practice of designing a system that prompts a coding agent on your behalf, rather than prompting the agent directly, turn by turn. Where ordinary agent use has a person type an instruction, read the result, and type the next instruction, a loop is a small system that finds the work, hands it to the agent, checks what came back, records what was done, and decides the next step — with the person designing that system once rather than operating it continuously. It is described as sitting one level above [[DefinedTerm/harness-engineering]]: a harness shapes the environment a single agent runs inside, and a loop runs that harness on a schedule, spawning helper agents and feeding itself new work. A second account puts the same relation in terms of the harness itself — everything around the model other than the model, meaning the system prompt, tools, permissions, context management, verification loops and logs — and describes loop engineering as a control plane one level up that designs that harness to keep going autonomously against stopping conditions or a scheduler. The shift it names is the same in both: you stop prompting the model yourself and start designing the loop that prompts it.

## Usage

A loop is built from five recurring pieces plus a place to remember state: automations that run on a schedule to discover and triage work; worktrees (isolated working directories on their own branch) so agents running in parallel don't edit the same files; skills that record project-specific knowledge so the agent doesn't have to re-derive it every session; plugins and connectors, generally built on MCP, that let the loop reach real tools such as an issue tracker or a chat channel; and sub-agents split so that the one who writes the work is not the one who checks it, since a model grading its own output tends to be too lenient. The sixth piece is external memory — a markdown file or a Linear board that lives outside any single conversation — since the underlying model forgets everything between runs and this state has to live on disk instead. Both the Codex app and Anthropic's Claude Code are described as now shipping all five pieces, under different names, which is presented as evidence that loop engineering has become a property of the products themselves rather than something each team has to hand-build.

A worked instance outside coding work is reported in [[BlogPosting/loop-engineering-prompt-tuning]], where the loop being automated is prompt tuning for a vision-language model. Its construction method is stated as decomposing what the person was already doing by hand and assigning each step its own component — looking at the failures, diagnosing the cause, rewriting the prompt, re-evaluating, and recording what helped, with the re-evaluation step falling to a plain script and the rest to sub-agents — and a skill file acting purely as orchestrator, a single policy file holding the improvement priorities, accept/reject rules and stopping conditions that every sub-agent follows, and a lessons file the loop appends to after each iteration as the deliberate equivalent of a human tuner's accumulating memory. That account reports the automated loop matching or slightly exceeding hand tuning on the one task where a comparison existed, and cutting the surrounding evaluation cycle from about 3.5 weeks to about one week, from a single run rather than a repeated measurement.

## When It Applies

It applies to recurring or long-running work that would otherwise require a person to keep re-prompting the agent each cycle — triage, scheduled discovery, or work that continues unattended. It assumes a stopping condition that can actually be checked (e.g. by a verifying model) and durable external state the loop can read and write between runs, since the underlying model itself retains nothing across them. Verification is described as remaining a human responsibility even once the loop is running well: an unattended loop still makes mistakes unattended, and the practice is described as making two other problems sharper rather than solving them — a person's understanding of the shipped code can rot faster if they stop reading what the loop produces, and a well-running loop can tempt someone into accepting its output uncritically. It is presented as a synthesis of practices independently described by other practitioners (Peter Steinberger and Boris Cherny are both quoted describing the same shift toward designing loops rather than prompting agents directly); the five-piece enumeration above is Steinberger's list, and the author's own contribution is to map it onto both the Codex app and Claude Code and work through each piece in turn.

The prompt-tuning account adds two cautions of its own, both about what an unattended loop does when it is working. Because each iteration re-ran inference over the whole dataset, API charges accumulated, and it notes that a badly designed loop can keep inferring in the background and drive costs up unexpectedly, recommending that a change be tried on a small sample first and evaluated over the full dataset only when that run looks promising. And because the loop optimizes against whatever it is scored on, the artifact it was editing grew steadily longer as accuracy rose; that account names overfitting as the thing it watched most closely, on the stated reasoning that the more the wording leans toward the training data the higher the overfitting risk becomes, and recommends holding out a test split at minimum.

## Related Terms

[[DefinedTerm/harness-engineering]], [[DefinedTerm/agent-harness]], [[DefinedTerm/sub-agent-architecture]], [[SoftwareApplication/claude-code]]
