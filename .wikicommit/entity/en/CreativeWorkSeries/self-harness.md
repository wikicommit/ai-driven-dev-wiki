---
title: "self-harness"
type: "schema:CreativeWorkSeries"
lang: en
tags: [agents, agent-architecture, context-engineering, agentic-engineering]
sources:
  - type: url
    url: 'https://github.com/datawhalechina/self-harness'
    hash: sha256:1cbe56dd3adc95cae9abae32a6356996fc03b56f4bdeb88b44cae256d918dd66
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  about: "[[DefinedTerm/harness-engineering]]"
  author: "Datawhale"
  url: "https://datawhalechina.github.io/self-harness/"
  creativeWorkStatus: "Alpha"
---

self-harness is an open-source Chinese-language tutorial on
[[DefinedTerm/harness-engineering]], published by the Datawhale community as a numbered
series of chapters with an accompanying practice project. Its stated aim is to help
developers understand how to build a robust underlying runtime architecture for complex,
long-running AI agents.

The series organises the field as a progression rather than a set of alternatives: from
[[DefinedTerm/prompt-engineering]], through [[DefinedTerm/context-engineering]] as dynamic
information management, to harness engineering at the system level. That framing is the
tutorial's own organising claim, and it supplies the sequence the chapters follow.

It is written for AI application developers, people interested in large-model technology,
and Python developers with basic programming ability. The outcomes it states for a reader
are understanding how context engineering differs from prompt engineering, handling dynamic
context management, designing an extensible AI skill system, and building a minimal
system of the kind [[SoftwareApplication/claude-code]] represents.

## Scope & Structure

The tutorial is split into a theory part and a practice part. The theory chapters introduce
prompt engineering's concepts, methods and limitations; context engineering's concepts and
methods; harness design for agents that must run a long time without going wrong; and the
progression connecting the three. The practice part is built around
[[SoftwareApplication/minimaster]], a minimal harness implementation whose code ships in the
same repository, and which the tutorial uses to show how harness theory lands in an actual
agent system.

The series is read online at <https://datawhalechina.github.io/self-harness/>, and the
chapters live as Markdown in the repository alongside the practice code.

## Status

The project is marked Alpha. Its own notice states that the content is still being improved
and may contain errors or omissions, and invites readers to file issues. The repository's
outstanding-work list names one item: an analysis of agent products built on mainstream
harness systems, giving NanoBot and OpenHarness as its examples.

The work is licensed under Creative Commons Attribution–NonCommercial–ShareAlike 4.0
International.
