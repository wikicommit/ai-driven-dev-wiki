---
title: "Effective harnesses for long-running agents"
type: "schema:BlogPosting"
lang: en
tags: [long-running-agents, harness-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
    hash: sha256:26ce4c203cbb030f31253f1eb174b46b2c0203c9b44576aa4654b89b4d7be777
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An Anthropic engineering post on getting an agent to make consistent progress across many context windows, reporting two observed failure modes and a two-part harness — an initializer agent that sets up the environment once, and a coding agent that advances one feature per session and leaves the repository clean."
  author: ["Justin Young"]
  datePublished: "2025-11-26"
  publisher: "[[Organization/anthropic]]"
---

The post takes as its starting problem that agents working on tasks spanning hours or days must work
in discrete sessions, each beginning with no memory of the last. Its image for this is a software
project staffed by engineers working in shifts where each new engineer arrives remembering nothing of
the previous shift. It reports that [[DefinedTerm/compaction]] alone does not solve this: even a
frontier model running on the [[SoftwareApplication/claude-agent-sdk]] in a loop falls short of
building a production-quality web app from a high-level prompt.

Two failure modes are reported from that experiment. The agent tends to attempt too much at once —
essentially trying to one-shot the app — and runs out of context mid-implementation, leaving the next
session with a half-built, undocumented feature it must then reconstruct. Later in a project the
opposite failure appears: an agent instance looks around, sees that progress has been made, and
declares the job done.

The answer described is two-part. An **initializer agent** runs once and sets up the environment: an
`init.sh` script, a progress log, an initial git commit, and a JSON list of every feature the prompt
implies, each marked as failing. Every subsequent **coding agent** session then reads that state,
picks one unfinished feature, implements and verifies it end-to-end, and leaves the repository
committed and documented. The post's stated key insight is that what makes this work is giving a
fresh context window a fast way to understand the state of the work — the progress file alongside the
git history — and it notes the practices were drawn from what effective software engineers do daily.

## Key Points
- The core challenge of long-running agents is that they work in discrete sessions, each starting with
  no memory of what came before.
- Compaction is reported as insufficient on its own: it does not always pass sufficiently clear
  instructions to the next agent.
- The first observed failure mode is the agent trying to one-shot the application and exhausting its
  context mid-feature, leaving the next session to guess what happened.
- The second, appearing later in a project, is a subsequent agent seeing existing progress and
  declaring the work complete.
- The solution splits into setting up an initial environment that anticipates all the required
  features, and prompting each session to make incremental progress while leaving a clean state.
- "Clean state" is defined as code appropriate for merging to a main branch: no major bugs, orderly
  and well-documented, with no unrelated mess for the next developer.
- The initializer agent writes an `init.sh` script, a progress log file, and an initial git commit
  showing what was added.
- It also writes a comprehensive feature-requirements file expanding on the user's prompt — reported
  as over 200 features for the post's worked example — with every feature initially marked failing.
- Coding agents are permitted to edit that file only by changing a feature's pass status, reinforced
  with strongly-worded instructions against removing or editing tests.
- JSON was chosen over Markdown for that file after experimentation, on the reported grounds that the
  model is less likely to inappropriately change or overwrite a JSON file.
- Working on only one feature at a time is reported as critical to addressing the agent's tendency to
  attempt too much.
- Committing to git with descriptive messages and writing progress summaries is reported as the most
  effective way to elicit a clean end state, and lets the model revert bad changes and recover working states.
- A further failure mode is marking a feature complete without proper testing: absent explicit
  prompting, the agent made changes and ran unit tests or `curl` checks but failed to recognise the
  feature did not work end-to-end.
- Explicitly prompting the agent to use browser automation and test as a human user would is reported
  to have dramatically improved performance for web app work.
- Limits are acknowledged: the model cannot see browser-native alert modals through the tooling used,
  and features relying on those modals tended to remain buggier.
- Each coding session is prompted through a fixed startup sequence: check the working directory, read
  the git log and progress file, read the feature list, and pick the highest-priority unfinished feature.
- Running a basic end-to-end check before starting new work is reported to let the agent detect and fix
  a broken state rather than building on top of it.
- Whether a single general-purpose coding agent or a multi-agent architecture of specialists performs
  better is stated as an open question.
- The demonstration is optimized for full-stack web app development, and generalising it to other
  domains is named as future work.

## Context
The post is a vendor engineering write-up: the harness, the SDK and the model are all Anthropic's, and
the findings are reported from internal experimentation on one worked example — a clone of a chat
application — rather than from measurement across projects. The failure modes and the fixes are
presented as what worked in that setting, with the open questions stated plainly at the end. Its
framing sits alongside this wiki's other accounts of [[DefinedTerm/long-running-agent]] design, and
the recurring move it shares with them is pushing state out of the context window and into durable
artifacts the next session can read.
