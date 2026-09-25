---
title: "FastRender"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, multi-agent, long-running-agents]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Jan/19/scaling-long-running-autonomous-coding/'
    hash: sha256:48a495e26b74c84e49f7d78e3e149aa586889c3c0150caeddaa6ec6089c62816
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An experimental web browser built from scratch by a large fleet of autonomous coding agents in a Cursor experiment on scaling long-running agents; reported to span over a million lines of code across 1,000 files."
  applicationCategory: "Web browser (experimental)"
---

FastRender is an experimental web browser written almost entirely by autonomous coding agents,
produced as the test case for an experiment at [[SoftwareApplication/cursor]] into how far a large
fleet of concurrently running coding agents could be pushed. Cursor's own description, as quoted by
Simon Willison, says it pointed the system at the goal of building a web browser from scratch, and
that the agents ran for close to a week, writing over a million lines of code across 1,000 files.
The source code is published on GitHub.

The agents were organised with planners and sub-planners creating tasks, workers executing them, and
a judge agent deciding at the end of each cycle whether the project was complete — a structure
Willison likened to the way [[SoftwareApplication/claude-code]] uses sub-agents, and which is
described in more detail under [[DefinedTerm/planner-worker-model]].

## Capabilities

Willison built and ran FastRender on macOS following the build instructions in the repository's
README, and got a working browser window. His screenshots of google.com and his own blog show pages
that were legible and mostly correct but with obvious rendering glitches, such as unstyled buttons,
a garbled tab name and a misplaced decorative quotation mark; he took those glitches as evidence
that the project was not simply wrapping an existing rendering engine. The repository includes
various WhatWG and CSS-WG specifications as Git submodules, which he described as a smart way of
making sure the agents had the reference material they might need.

## Adoption & Ecosystem

The initial announcement was met with skepticism, particularly once it emerged that the project's
GitHub Actions CI was failing and the repository had no build instructions; build instructions were
added shortly afterwards. Willison, who had predicted that someone would build a full web browser
mostly with AI assistance by 2029, wrote that FastRender was close to the quality of result he had in
mind, while not expecting projects of this kind to compete with Chrome, Firefox or WebKit any time
soon. He noted it was the second attempt he had seen within two weeks at building a full browser
with AI-assisted coding.
