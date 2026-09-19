---
title: "Google Jules"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
  - type: url
    url: 'https://blog.google/innovation-and-ai/models-and-research/google-labs/jules/'
    hash: sha256:045d1ff3cfcaebcc5a6d35e296eeef341badab6b59904bfb83b3f3b2424d8912
  - type: url
    url: 'https://developers.googleblog.com/en/meet-jules-tools-a-command-line-companion-for-googles-async-coding-agent/'
    hash: sha256:0b83d567fc4fa88e7bd204dbcc5bc820c22c75850e726f73afb880c915bc0f0f
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An asynchronous, autonomous coding agent from Google Labs that clones a repository into a cloud VM, works on tasks in the background, and returns a plan, its reasoning and a diff."
  applicationCategory: "Autonomous task-oriented agent"
  author: "[[Organization/google]]"
---

Google Jules is an autonomous, asynchronous coding agent from Google Labs. Google describes it as integrating directly with existing repositories: it clones the codebase into a secure Google Cloud virtual machine, takes in the project's full context, and works in the background while the developer does something else, presenting its plan, its reasoning and a diff of the changes on completion. Google's own positioning sets it against completion assistants — in the announcement's words, "[n]ot a co-pilot, not a code-completion sidekick, but an autonomous agent that reads your code, understands your intent, and gets to work."

## Capabilities

The tasks Google lists for it are writing tests, building new features, fixing bugs, bumping dependency versions and producing audio changelogs. It ran on Gemini 2.5 Pro at the time of its public-beta announcement, which Google paired with the cloud VM system to claim it can handle complex, multi-file changes and concurrent tasks.

A later post on Google's developer blog describing the agent's command line companion sets out the shape of a
single task: Jules runs in the background, powering tasks in remote VMs and synchronising with the
user's repositories, and when a task is started it spins up a temporary VM, does the work there and
sends back a pull request — with nothing running until the developer asks it to. That post lists the
agent's tasks as writing tests, building new features, providing audio changelogs, fixing bugs and
bumping dependency versions.

Google's own stated properties for it, as of the public-beta announcement, are that it works on real codebases rather than requiring a sandbox; that tasks running inside the cloud VM allow parallel execution of multiple simultaneous requests; that its workflow is visible, with the plan and reasoning shown before changes are made; that it integrates directly into an existing GitHub workflow with no extra setup; that the presented plan is user-steerable before, during and after execution; and that it offers an audio changelog of recent commits. On privacy Google states that Jules is private by default, does not train on private code, and keeps data isolated within the execution environment. These are the vendor's claims, made in its own announcement, without independent evaluation.

## Adoption & Ecosystem

A survey on AI agentic programming classifies Google Jules, in its comparative taxonomy, as a "Task-oriented" agent that is proactive, multi-turn, tool-using, and adaptive, and characterizes it as able to sandbox repositories, propose diffs and execute verified changes on real projects. Google's own announcement uses the word differently, saying Jules "doesn't need a sandbox" in the sense of a throwaway environment — it runs against the real codebase, inside the isolated cloud VM described above.

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] notes that Google Jules has included a planning step from its inception, contrasting it with Anthropic's [[SoftwareApplication/claude-code]], which only more recently added an on-demand planning mode.

Since October 2025 Jules can also be driven from the terminal through
[[SoftwareApplication/jules-tools]], a command line interface and TUI that Google says makes the
agent programmable, scriptable and customizable, so it can be composed with other command line tools
and wired into a developer's own automations rather than operated only through the web UI (see
[[BlogPosting/meet-jules-tools]]). Google frames that release within a "hybrid by design" position:
local plus remote, and do-it-yourself plus delegation.

Jules was first introduced in Google Labs in the December preceding its public beta, which it entered worldwide without a waitlist on 20 May 2025, in every region where the Gemini model is available (see [[BlogPosting/build-with-jules]]). That announcement frames the moment in general terms, arguing that agentic development is "shifting from prototype to product and quickly becoming central to how software gets built".
