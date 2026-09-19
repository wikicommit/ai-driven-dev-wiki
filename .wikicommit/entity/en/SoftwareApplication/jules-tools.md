---
title: "Jules Tools"
type: "schema:SoftwareApplication"
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
  description: "A lightweight command line interface and TUI for Google's asynchronous coding agent Jules, making it scriptable and composable with other terminal tools."
  applicationCategory: "Command line interface for a coding agent"
  author: "[[Organization/google]]"
  featureList: "Commands and flags for driving remote Jules sessions; TUI dashboard for tasks; scriptable composition with other CLI tools"
---

Announced in October 2025, Jules Tools is a lightweight command line interface for
[[SoftwareApplication/google-jules]], Google's asynchronous coding agent. Google built it
because developers had previously interacted with Jules
mainly through a web browser, and describes it as a way to spin up tasks, inspect what
Jules is doing and customize the agent without leaving the terminal.

Google presents it as both a dashboard and a command surface for a coding agent. Its
stated significance is not only convenience of access: Google argues the CLI makes Jules
programmable, scriptable and customizable, so it can be integrated into a developer's own
automations or used to steer the agent in real time with short commands.

## Capabilities

Google gives npm as the easiest way to get started:

```
npm install -g @google/jules
```

At its core the CLI is built around **commands**, which tell Jules what to do, and
**flags**, which adjust how it behaves. Google's examples are `jules remote list --task`
to list remote tasks, and `jules --theme light` to switch to a light-themed terminal
interface.

Because it is scriptable, Jules Tools composes with other command line tools. Google's
published examples list the repositories connected to Jules, create a remote session
against a named repository with `jules remote new --repo <repo> --session "<task>"`, loop
a `TODO.md` file into one session per line, pipe a GitHub issue title from `gh` straight
into a new session, and use the Gemini CLI to pick the most tedious issue from a list and
hand it to Jules.

For interactive use the tool also offers a TUI. Google states that commands such as
`/remote` give a dashboard view of tasks while `/new` walks through creating one step by
step, and characterizes this as the same control as the web UI, faster and closer to where
the developer already works locally.

## Adoption & Ecosystem

Google positions the tool within a "hybrid by design" view of development tooling: local
plus remote, using the developer's own machine when wanted and spinning up multiple VMs
when scale is needed; and do-it-yourself plus delegation, staying hands-on with code while
offloading work to the agent. The announcement and its worked examples are described in
[[BlogPosting/meet-jules-tools]].
