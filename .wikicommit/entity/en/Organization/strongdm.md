---
title: "StrongDM"
type: "schema:Organization"
lang: en
tags: [coding-agents, agents, security, software-process]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Feb/7/software-factory/'
    hash: sha256:f037b61ef74329e98d22e3f5e86498585708d651d71581e420890095020b0ad3
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A company whose AI team published the first public account of their software factory — non-interactive development in which agents write code that no human writes or reviews — and which built the tooling that arrangement depends on, including a universe of agent-built clones of their third-party dependencies."
---

StrongDM is known here through its AI team, which published the first public description of the
working arrangement they call a [[DefinedTerm/software-factory]]: non-interactive development in
which specifications and scenarios drive agents, under the team's stated rules that code must not be
written by humans and must not be reviewed by humans. The software this team was building manages
user permissions across a suite of connected services, which
[[BlogPosting/how-strongdms-ai-team-build-serious-software-without-even-looking-at-the-code]]
singles out as notable: security software is the last thing one would expect to be built from
unreviewed agent-written code.

The team is a distinct and recent part of the company rather than the whole of it. It was founded in
July 2025 on the rule of no hand-coded software, and consisted of three people at the time it was
first seen working. Its own account of why it formed when it did points at a transition observed in
late 2024: with the second revision of Claude 3.5, the team state, long-horizon agentic coding
workflows began to compound correctness rather than error, and by December 2024 the model's
long-horizon coding performance was unmistakable to them.

## History
What is recorded here is the AI team's history rather than the company's. It was founded in July 2025
and had been running three months when it demonstrated its work to a small group of invited guests in
October 2025 — by which point, on that visitor's account, it already had a working coding agent
harness, clones of half a dozen third-party services, and a swarm of simulated test agents running
through scenarios. That was before the model releases at the end of 2025 that the same account
credits with making agentic coding significantly more reliable. The public write-up followed in early
February 2026.

## Activities & Products
The team's distinctive engineering output is the apparatus that makes unreviewed agent-written code
tolerable to them. The [[DefinedTerm/digital-twin-universe]] is their set of agent-built behavioural
clones of the third-party services their software depends on — twins were built for Okta, Jira,
Slack, Google Docs, Google Drive and Google Sheets — which they use to run thousands of scenarios per
hour without rate limits or API costs. Alongside it they use scenarios held outside the codebase as a
holdout set, and a probabilistic measure they call satisfaction in place of a green test suite.

Two pieces of software were released with the write-up.
[[SoftwareApplication/attractor]] is the non-interactive coding agent at the heart of the
arrangement, published in an unconventional form: the repository contains no code, only markdown
files specifying the software and a note telling the reader to feed those specifications into their
own coding agent. [[SoftwareApplication/cxdb]] is a conventional release — an AI context store
holding conversation histories and tool outputs in an immutable DAG. The team also publish a set of
named techniques, among them gene transfusion, semports and pyramid summaries.
