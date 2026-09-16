---
title: "Loop Engineering"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/loop-engineering/'
    hash: sha256:aa188c2fd5951b4662d056122bce224b571a90019a5babf31589c75238b358e1
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The practice of designing an automated system — scheduled automations, isolated worktrees, skills, connectors, and a maker/checker split between sub-agents — that prompts and checks a coding agent on your behalf, rather than prompting the agent directly turn by turn."
---

Loop engineering is the practice of designing a system that prompts a coding agent on your behalf, rather than prompting the agent directly, turn by turn. Where ordinary agent use has a person type an instruction, read the result, and type the next instruction, a loop is a small system that finds the work, hands it to the agent, checks what came back, records what was done, and decides the next step — with the person designing that system once rather than operating it continuously. It is described as sitting one level above [[DefinedTerm/harness-engineering]]: a harness shapes the environment a single agent runs inside, and a loop runs that harness on a schedule, spawning helper agents and feeding itself new work.

## Usage

A loop is built from five recurring pieces plus a place to remember state: automations that run on a schedule to discover and triage work; worktrees (isolated working directories on their own branch) so agents running in parallel don't edit the same files; skills that record project-specific knowledge so the agent doesn't have to re-derive it every session; plugins and connectors, generally built on MCP, that let the loop reach real tools such as an issue tracker or a chat channel; and sub-agents split so that the one who writes the work is not the one who checks it, since a model grading its own output tends to be too lenient. The sixth piece is external memory — a markdown file or a Linear board that lives outside any single conversation — since the underlying model forgets everything between runs and this state has to live on disk instead. Both the Codex app and Anthropic's Claude Code are described as now shipping all five pieces, under different names, which is presented as evidence that loop engineering has become a property of the products themselves rather than something each team has to hand-build.

## When It Applies

It applies to recurring or long-running work that would otherwise require a person to keep re-prompting the agent each cycle — triage, scheduled discovery, or work that continues unattended. It assumes a stopping condition that can actually be checked (e.g. by a verifying model) and durable external state the loop can read and write between runs, since the underlying model itself retains nothing across them. Verification is described as remaining a human responsibility even once the loop is running well: an unattended loop still makes mistakes unattended, and the practice is described as making two other problems sharper rather than solving them — a person's understanding of the shipped code can rot faster if they stop reading what the loop produces, and a well-running loop can tempt someone into accepting its output uncritically. It is presented as a synthesis of practices independently described by other practitioners (Peter Steinberger and Boris Cherny are both quoted describing the same shift toward designing loops rather than prompting agents directly), building further on those quotes with the author's own five-piece breakdown.

## Related Terms

[[DefinedTerm/harness-engineering]], [[DefinedTerm/sub-agent-architecture]], [[SoftwareApplication/claude-code]]
