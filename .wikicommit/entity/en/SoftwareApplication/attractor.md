---
title: "Attractor"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, agents, spec-driven-development]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Feb/7/software-factory/'
    hash: sha256:f037b61ef74329e98d22e3f5e86498585708d651d71581e420890095020b0ad3
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The non-interactive coding agent at the centre of StrongDM's software factory, released in an unconventional form: the repository contains no code at all, only markdown files specifying the software and an instruction to feed them to a coding agent of the reader's choice."
  applicationCategory: "Non-interactive coding agent"
  author: "[[Organization/strongdm]]"
---

Attractor is the non-interactive coding agent at the heart of [[Organization/strongdm]]'s
[[DefinedTerm/software-factory]] — the component that runs the arrangement in which agents write
code without a human writing or reviewing it. It was released publicly alongside the team's first
account of how they work.

What is notable about the release is its form rather than its function. The repository contains no
code at all: just three markdown files describing the specification for the software in meticulous
detail, and a note in the README saying that the reader should feed those specifications into their
coding agent of choice. The distributed artefact is therefore the specification, and the executable
is whatever the reader's own agent produces from it.

## Capabilities

Only the agent's role is established here. The team describe their arrangement as one in which
specifications plus scenarios drive agents that write code, run harnesses and converge without human
review, under their stated rules that code must not be written by humans and must not be reviewed by
humans — that is the sense in which this agent is called non-interactive, and the source offers no
other gloss on the word. No version is recorded, and the source describes no interface,
flags or configuration — consistent with a release whose whole content is the specification a reader
is expected to build from.

## Adoption & Ecosystem

Attractor is used by the team that wrote it, as the engine of the arrangement described in
[[BlogPosting/how-strongdms-ai-team-build-serious-software-without-even-looking-at-the-code]]; no
adoption outside that team is recorded. It sits alongside the team's other release,
[[SoftwareApplication/cxdb]], and the scenarios that drive it are, on the team's account, often kept
outside the codebase.

The release form is itself a claim about how software is distributed under this way of working, and
is treated that way by the post that reports it — a repository of specifications rather than of
build output. That reading is the reporter's framing of an unusual publishing decision, not a stated
intention of the team's.
