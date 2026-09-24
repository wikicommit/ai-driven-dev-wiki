---
title: "Google Antigravity"
type: "schema:SoftwareApplication"
lang: en
sources:
  - type: url
    url: 'https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/'
    hash: sha256:702649e8a757da9007eeda56b0fe7deceaa3aa8140675fe480fce240e9ac2760
  - type: url
    url: 'https://antigravity.google/blog/introducing-google-antigravity'
    hash: sha256:9e5695d0c9b8803cf6a7d846d0be04cb6b60ed142edd674d92f09e2ea98e2f8a
  - type: url
    url: 'https://antigravity.google/changelog'
    hash: sha256:b0b3bf8a83113a1801fca60c849755cf0a8bf727c40a344c5d00a49916f1a79c
  - type: url
    url: 'https://antigravity.google/docs/features/'
    hash: sha256:ba3f1aa139f0c87f6e894e5254a901e4c4c5910b1a1e2f3be4d39ddb72438bf0
  - type: url
    url: 'https://antigravity.google/docs/ide/browser/'
    hash: sha256:de488998aeffcaff120204f17bc55cc1ec1ff8420d08916f50aae8fcd050a794
  - type: url
    url: 'https://antigravity.google/docs/subagents/'
    hash: sha256:5be9ef15339e691ef64f32feff17f95fe5b9fb784ff700b261fe1757ec8ce1a7
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
tags: [agents, coding-tools, agent-architecture, human-oversight]

properties:
  description: "Google's agentic development platform, combining an AI-powered editor with an agent-first Manager surface; its agents plan, execute and verify tasks across the editor, terminal and browser."
  applicationCategory: "Agentic development platform"
  operatingSystem: "macOS, Windows, Linux"
  featureList: "Editor View with tab completion and inline commands; Manager surface for spawning, orchestrating and observing asynchronous agents; agent Artifacts (task lists, implementation plans, walkthroughs, screenshots, browser recordings); inline feedback on Artifacts; knowledge base of saved context and code snippets"
  author: "[[Organization/google]]"
---

Google Antigravity is an agentic development platform published by
[[Organization/google]], announced in November 2025. Google describes it as not just an
editor but a development platform that combines a familiar AI-powered coding experience with an
agent-first interface, from which agents can be deployed to autonomously plan, execute
and verify complex tasks across the editor, terminal and browser.

The design premise Google states for it is that agents should have a dedicated space to
work in rather than occupying a sidebar, and that a developer should be able to operate
at a higher, task-oriented level rather than at the level of individual prompts and tool
calls. Its answer to the
resulting trust problem is to have agents report through reviewable deliverables rather
than through raw tool-call logs. The product team's own launch post
([[BlogPosting/introducing-google-antigravity]]) organises the product around four tenets
— trust, autonomy, feedback and self-improvement — and presents it as the IDE evolving
toward an agent-first future, prompted by models such as Gemini 3 becoming able to run for
longer periods without intervention across multiple surfaces.

The name has since come to cover a product family. The product changelog lists the
original launch as release 1.11.2 on November 18, 2025, and records a second generation,
Antigravity 2.0, launching in May 2026 with an import path from Antigravity 1.0; the changelog lists the Antigravity IDE as its own product line, whose 2.0.1
entry of the same month is described as the first release of the Antigravity IDE, and the family also
includes the [[SoftwareApplication/antigravity-cli]] and the Python
[[SoftwareApplication/antigravity-sdk]]. The overview and capabilities below describe the
platform as launched unless a version is named.

## Capabilities

The platform presents two distinct surfaces. The Editor View is an AI-powered IDE with
tab completions and inline commands, for the synchronous hands-on workflow Google
describes as already familiar; the launch post adds that it carries a fully functioning
agent in the side panel.
The Manager surface is the agent-first interface, where several agents can be spawned,
orchestrated and observed working asynchronously across different workspaces — Google
positions it for dispatching long-running maintenance work or bug fixes in the
background, including tasks that span reproducing an issue, generating a test case and
implementing a fix. The launch post describes it as flipping the paradigm from agents
embedded within surfaces to surfaces embedded into the agent, likening it to a mission
control, and says the team deliberately kept the Manager and the Editor in separate
windows, optimising for instant handoffs between them rather than squeezing both into one.

Agents work across the editor, terminal and browser within one task. Google's worked
example has an agent write code for a feature, use the terminal to launch the
application, then use the browser to test and verify the new component, without
synchronous human intervention.

The product documentation for the Antigravity IDE describes the browser side of this: the
agent can open, read and actuate a local Chrome browser — to test development websites,
read documentation or automate browser tasks — working through a specialised browser
subagent that captures screenshots and saves action videos as artifacts. Browser tools can
be switched off entirely in settings; URL access is controlled by a two-layer denylist and
allowlist, and the agent runs in a separate Chrome profile from the user's own.

Verification is mediated by **Artifacts** — deliverables the agent generates, such as
task lists, implementation plans, walkthroughs, screenshots and browser recordings.
Google's stated rationale is that these let a developer check the agent's logic at a
glance where scrolling raw tool calls would be tedious; the launch post frames this as
presenting agent work at a task-level abstraction, with tool calls grouped within tasks.
Feedback can be left directly on an Artifact, comparably to commenting on a document —
the launch post names Google-doc-style comments on text Artifacts and select-and-comment
feedback on screenshots — and the agent incorporates that input without halting its
execution flow. Google also states the platform treats learning as a core primitive,
allowing agents to save useful context and code snippets to a knowledge base to improve
future tasks; the launch post says that knowledge can also be more abstract, such as the
series of steps that completed a particular subtask.

### Later releases

Among the releases after launch, the changelog records agent Skills arriving in January 2026 (1.14.2), terminal commands
running inside a sandbox — first on macOS (1.15.6), later on Linux (1.21.6) — with file and
network sandboxing on Windows following in the 2.0 line (2.15.1), rules read from `AGENTS.md` as well as `GEMINI.md` (1.20.5), and a
unified agent permissions system (1.22.2, April 2026).

In the Antigravity 2.0 line, the changelog records Remote Control for driving local agent
sessions from any browser (2.9.1), an embedded terminal and Git version control in the
sidebar (2.10.0), inline "generative UI" rendering of HTML artifacts (2.11.0), a `/boost`
command for a multi-agent reasoning pass (2.12.0), and a `/plan` command whose plans can be
read and edited before any code is written, governed by a Plan Review Policy setting
(2.17.0).

### Antigravity 2.0

The product documentation describes how Antigravity 2.0 organises work. Agents work in
**Projects**, where previously in the Agent Manager each agent was mapped to a single
workspace folder. A project can span several folders, supports Git worktrees so agents can
operate in isolated background folders, and carries its own scoped settings and permission
grants — so a trusted project can be given a more permissive security preset than an
untrusted folder. Quick one-off conversations can also run outside any project, in an
isolated local scratch folder.

By default the documentation describes agents as asking for explicit permission before
running terminal commands outside the terminal sandbox on macOS and Linux (or before any
terminal command on Windows), and as able to read and write only within a project's
folders unless the user broadens that setting. Other 2.0 features it lists include
scheduled tasks that send messages to agents on a timer, live voice transcription for
prompts and Artifact comments, JSON hooks that run local shell scripts at points in the
agent's execution cycle, a reworked browser subagent invoked with `/browser` that
integrates with Chrome DevTools MCP, Remote Control of desktop agent sessions from any web
browser, an integrated terminal, and a Git-native version-control panel for reviewing
uncommitted, branch and agent-made diffs.

### Subagents

The documentation for Antigravity 2.0 and the Antigravity CLI describes delegation to
concurrent background subagents. A parent agent spawns one with an `invoke_subagent` tool,
giving it a role and an initial prompt; the subagent starts with a clean context rather
than the parent's conversation history, and can inherit the parent's workspace, get an
isolated Git worktree, or share directory storage. Three subagents come built in —
`research` for codebase exploration, `browser` for interactive browser testing, and `self`,
a clone of the calling agent — and custom ones are defined as Markdown files whose YAML
frontmatter sets their tools, model tier and command-execution policy and whose body is
their system prompt.

A subagent is running, idle (finished and waiting, re-awakened by a message) or killed.
Agents message each other by conversation ID and can read each other's transcripts, and
nesting is capped at ten levels below the primary agent. Subagents inherit the parent's
command allowlist, file-access scopes and sandbox settings, and a request needing user
approval bubbles up to the main interface. On top of this, the documentation describes two
multi-agent orchestrators: `/boost`, a three-tier reasoning hierarchy for hard problems
within an interactive session, and `/teamwork-preview`, which coordinates a team of
specialised agents on larger projects through milestone decomposition, parallel
implementation and independent verification.

## Adoption & Ecosystem

At its announcement the platform was released in public preview, at no cost for
individuals, and cross-platform across macOS, Windows and Linux. Google stated it
offered model optionality: generous rate limits on Gemini 3 Pro, with full support for
Anthropic's Claude Sonnet 4.5 and OpenAI's GPT-OSS. This availability and model list
describe the platform as announced in November 2025.
