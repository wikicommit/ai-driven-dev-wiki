---
title: "Loop Engineering"
type: "schema:BlogPosting"
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
  description: "An argument that the shift in working with coding agents is moving from prompting them turn-by-turn to designing automated loops — systems of scheduled automations, isolated worktrees, skills, connectors, and verifying sub-agents — that prompt and check the agent on your behalf."
  author: "Addy Osmani"
  datePublished: "2026-06-07"
---

This post argues that working with coding agents is shifting from directly prompting them turn by turn to designing "loops" — small systems that discover work, hand it to an agent, check the result, record what was done, and decide the next step, without a person prompting each turn. It frames this as one level above "harness engineering" (designing the environment a single agent runs inside): a loop runs the harness on a schedule, spawning helper agents and feeding itself. The post argues this has become less of a bespoke, hand-maintained thing and more something built into products themselves, since OpenAI's Codex app and Anthropic's Claude Code now ship comparable primitives for it.

## Key Points

- A loop needs five pieces plus a place to remember state: scheduled automations that discover and triage work, worktrees that isolate parallel agents from colliding, skills that codify project knowledge so the agent doesn't have to re-derive it each run, plugins/connectors (built on MCP) that connect the agent to real tools, and sub-agents that separate the one who writes work from the one who checks it — plus durable external memory (a markdown file or a project-management board) so state survives between runs, since the model itself forgets everything between them.
- Both Codex and Claude Code are reported to now offer all five primitives, under different names: Codex's Automations tab and `/goal` versus Claude Code's scheduled tasks/cron, `/loop`, `/goal`, and hooks; built-in worktree support versus `git worktree`/`--worktree`/`isolation: worktree`; Agent Skills in both; MCP-based connectors and plugins in both; TOML-defined subagents in `.codex/agents/` versus subagents in `.claude/agents/` and agent teams.
- `/goal` keeps an agent working across turns until a verifiable stopping condition holds; in Claude Code, this is checked after each turn by a separate model rather than the agent that did the work, described as the maker/checker split applied to the stop condition itself.
- Splitting the agent that writes from the agent that checks is described as the single most useful structural piece, because a model grading its own work is judged too lenient; a verifier with different instructions (and sometimes a different model) is what lets a loop run unattended.
- The post gives a worked example of one loop shape: a daily automation triages CI failures, issues, and commits into a state file; each finding worth acting on gets its own worktree, a drafting sub-agent, and a reviewing sub-agent; connectors then open the PR and update the tracking ticket, with anything the loop can't handle routed to a human triage inbox.
- Loop engineering is presented as changing, not removing, three problems that get sharper as loops improve: verification remains the human's job even though a loop makes mistakes unattended too; understanding of the shipped code can rot faster if the person stops reading what the loop produced; and the ease of a working loop tempts a poster toward "cognitive surrender" — accepting whatever it returns without an opinion.

## Context

The post positions itself as building on public remarks by Peter Steinberger ("You should be designing loops that prompt your agents") and Boris Cherny, head of Claude Code at Anthropic ("I have loops running that prompt Claude... My job is to write loops"), and as one entry in a series of the author's own posts on adjacent ideas (agent harness engineering, the factory model, long-running agents, the orchestration tax, intent debt, comprehension debt, cognitive surrender). The author frames loop design as harder than prompt engineering rather than easier, and stresses that the same loop built by two different people can produce opposite outcomes depending on whether it is used to work faster on well-understood work or to avoid understanding the work at all.
