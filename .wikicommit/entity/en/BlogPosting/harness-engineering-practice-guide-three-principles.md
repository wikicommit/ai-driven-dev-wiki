---
title: "Harness Engineering 实践指南：落地探索的三大原则"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, coding-agents, feedback-loops, guardrails]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/harness-engineering/'
    hash: sha256:c7eb3fe986b891735c956a0430dbd40b0a73c9b4a1a3852ef3f9063202490339
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A March 2026 Chinese-language blog post by Phodal Huang presenting Harness Engineering as the redesign of software engineering systems from human-first to agent-aware. It organises the practice into three capabilities — system legibility, defensive constraints and automated feedback — illustrated with Stripe's agent loop and the Routa.js project."
  author: ["Phodal Huang"]
  datePublished: "2026-03-10"
---

This post, written in Chinese by Phodal Huang, starts from a problem he says teams meet once AI takes
on more work in real projects: AI writes code far faster than a team can keep the system's complexity
under control. Generated code may not understand the architecture, past design decisions or domain
rules, and without engineering constraints it can bypass existing structure, add new dependencies or
quietly move system boundaries. He argues that the problem lies not in the model but in the software
engineering system itself, whose code structure, tools and processes were built around human developers
who understand context, follow conventions and catch problems in review.

His response is [[DefinedTerm/harness-engineering]], which he presents as the practice of turning a
"human-first system" into an "agent-aware system" — an engineering system redesigned so that machines
can understand it, call it and verify against it. The post organises this into what it calls the
Harness Engineering Capability Model and closes by describing software development as a loop run
jointly by humans and agents, with Harness Engineering as that system's engineering infrastructure.

## Key Points

- The Harness Engineering Capability Model has three capabilities that build on one another: the
  system must first be legible enough for AI to understand its structure and context; it must then
  provide clear boundaries that limit what AI can do; and it must continuously feed back to AI so it
  can correct its behaviour.
- Legibility means making tacit knowledge explicit: system structure, architectural principles and
  domain concepts expressed in machine-readable form, so the repository works as a navigable knowledge
  map that AI can enter from high-level architecture documents. The author recommends disclosing
  context progressively according to the task (see [[DefinedTerm/progressive-disclosure]]) rather than supplying all documentation at once, and
  exposing system capabilities through CLIs or APIs rather than interfaces built for humans.
- Defence means narrowing AI's space of action. Mechanisms teams already use in continuous delivery —
  static analysis, automated tests, architecture validation — become, in his framing, part of the
  system's boundary rather than only quality assurance: "physical laws" AI can explore within but not
  break, enforced continuously by automation.
- Feedback means every change AI makes receives a signal at once: static analysis and tests in the
  development environment, CI results after commit, and monitoring data and logs after release. When
  these signals are collected and given back to AI, development shifts from a linear process to a
  loop, which he likens to continuous delivery running on a shorter cycle.
- As examples he describes Stripe's agent engineering practice, in which engineers trigger tasks from
  Slack or a CLI, an agent writes code and runs tests, a failing CI run sends the work into an automatic
  repair loop, and a pull request is raised only once basic quality is met, leaving humans mainly the
  final review; and [[SoftwareApplication/routa]], a multi-agent platform whose codebase is both the agents'
  working environment and developed with the agents' own participation, whose practices the post sorts
  under the same three capabilities.
- He cites Kief Morris's view that future development runs in two loops — a human-led loop about why
  to build something and an increasingly AI-run loop about how — and concludes that the developer's
  role shifts toward designing systems, setting rules and managing these loops.

## Context

The post is the author's practitioner framing of Harness Engineering rather than a report of
measurements; its Stripe and Routa.js examples are described qualitatively. Its conclusion is that breakthroughs in AI coding tend to come from the engineering system
rather than from model capability alone.
