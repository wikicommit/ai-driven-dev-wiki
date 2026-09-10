---
title: "NeoLabHQ"
type: "schema:Organization"
lang: en
tags: [agents, coding-tools]
sources:
  - type: url
    url: https://github.com/NeoLabHQ/context-engineering-kit
    hash: sha256:3a00d5fa6029f48343ba32101feda4acd0f31870b7ff74ef954be99d4e04a584
    license: GPL-3.0
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "The publisher of Context Engineering Kit — a software development company that builds tooling for AI coding agents out of its own production practice, and that also releases the Agent Sandbox container image and the Agent Eslint Config ruleset."
  url: "https://github.com/NeoLabHQ"
---

NeoLabHQ is the GitHub organisation that publishes [[SoftwareApplication/context-engineering-kit]],
a marketplace of context-engineering plugins for AI coding agents. It describes itself as a company
whose developers work on real production projects, and presents that practice as the source of what
it releases: the marketplace, it says, is based on prompts its own developers have used daily over a
long period, and the reliability figures it publishes for the kit are drawn from more than a year of
its own development usage rather than from an external benchmark.

## Activities & Products
Alongside the kit, the organisation releases two projects it presents as companions to it, both of
which it says also work independently:

- **Agent Sandbox** — a development sandbox image for agents, built on Microsoft's official
  devcontainers images and intended to work out of the box with most languages and agents.
- **Agent Eslint Config** — an ESLint configuration written for AI agents rather than for people,
  which the organisation calls overly opinionated and describes as forcing agents toward
  low-complexity, readable code. It bundles SonarJS, Unicorn and over a hundred rules aimed at
  security and cognitive complexity.

Documentation for the kit is published separately from the repository, at
[neolab.gitbook.io/cek](https://neolab.gitbook.io/cek).
