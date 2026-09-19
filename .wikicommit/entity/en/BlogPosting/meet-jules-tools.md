---
title: "Meet Jules Tools: A Command Line Companion for Google's Async Coding Agent"
type: "schema:BlogPosting"
lang: en
sources:
  - type: url
    url: 'https://developers.googleblog.com/en/meet-jules-tools-a-command-line-companion-for-googles-async-coding-agent/'
    hash: sha256:0b83d567fc4fa88e7bd204dbcc5bc820c22c75850e726f73afb880c915bc0f0f
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [agents, coding-tools, cli, agent-tooling]

properties:
  description: "Google Labs' announcement of Jules Tools, a command line interface for its asynchronous coding agent Jules, and the hybrid local/remote workflow it argues for."
  author: ["Jiahao Cai", "AK Kulkarni"]
  datePublished: "2025-10-02"
  publisher: "[[Organization/google]]"
---

A Google for Developers post, written by two engineers on the Google Labs team,
announcing that [[SoftwareApplication/google-jules]], Google's asynchronous coding agent,
can now be driven from the command line through a new CLI called
[[SoftwareApplication/jules-tools]]. The stated motivation is that developers had until
then interacted with Jules primarily in a web browser, while — in the authors' words —
developers live in the terminal, where they test, build, debug and ship.

The post's argument is that a command line surface changes what the agent is rather than
only where it is reached from: it makes Jules programmable, scriptable and customizable,
so it can be wired into a developer's own automations rather than operated as a separate
destination. The authors describe the result as both a dashboard and a command surface
for a coding agent, and argue in a "Looking ahead" section that the future of development
tools is hybrid.

## Key Points

- The post describes Jules as an asynchronous coding agent that integrates with existing
  repositories, understands a project's full context, and performs tasks such as writing
  tests, building features, providing audio changelogs, fixing bugs and bumping dependency
  versions.
- It states how a task runs: Jules spins up a temporary VM, does the work there, and sends
  back a pull request, with nothing running until the developer asks it to.
- The CLI installs with `npm install -g @google/jules` and is built around commands, which
  tell Jules what to do, and flags, which adjust its behaviour — the post's examples are
  `jules remote list --task` and `jules --theme light`.
- Because it is scriptable, the post shows it composed with other command line tools:
  listing connected repositories, creating a remote session against a named repository,
  looping a TODO file into multiple sessions, piping a GitHub issue title from `gh` into a
  new session, and using the Gemini CLI to pick the most tedious issue and hand it to
  Jules.
- Jules Tools also offers a TUI for interactive use, where commands such as `/remote` give
  a dashboard view of tasks and `/new` walks through creating one — which the post presents
  as the same control as the web UI, faster and closer to where the developer works.
- The authors state a "hybrid by design" position along two axes: local plus remote — use
  your own machine when you want, spin up multiple VMs when you need scale — and
  do-it-yourself plus delegation, staying hands-on with code while offloading work to the
  agent.

## Context

This is a first-party product announcement written by two of the product's own staff, so its claims about what Jules does and why a terminal surface
matters are the vendor's own. It reports no usage data or evaluation.

The post's "hybrid by design" framing — keeping the developer hands-on while delegating
in parallel — is a position about how much autonomy to hand an agent, adjacent to
[[DefinedTerm/human-in-the-loop]] and the [[DefinedTerm/supervised-agency-spectrum]]. Its
emphasis on making the agent scriptable and composable with existing CLI tools places it
alongside other work on the [[DefinedTerm/outer-loop]] and on
[[DefinedTerm/long-running-agent]] workflows.
