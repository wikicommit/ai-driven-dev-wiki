---
title: "2026年のAI Coding Agent活用 ── スピードと安全性を両立させる"
type: "schema:BlogPosting"
lang: en
tags: [security, agents, guardrails, sandboxing]
sources:
  - type: url
    url: 'https://zenn.dev/team_zenn/articles/ai-agent-security'
    hash: sha256:2be721cd73612dfe7c91c26ac50fcee96d54da09dcbaa9bd625325d049417502
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A survey of the security risks of working with AI coding agents — credential exposure, dependency supply chain, prompt injection, insecure output — paired with the guardrails the author uses against each, and an argument that exhaustive output checking by vendors is not technically possible so verification falls to the user."
  author: "dyoshikawa"
  datePublished: "2026-01-29"
  publisher: "Zenn Tech Blog"
---

Based on a talk the author gave in January 2026, this post sets out the security risks that come with
AI coding agents and the guardrails available against them, and argues throughout that the two must
be traded off deliberately rather than resolved. Its organizing claim is that nobody else can do the
verification for you: the author works through a combinatorial estimate of how many input–output
pairs a model can produce and concludes that exhaustive checking by the vendor is not technically
achievable, so the responsibility for validating what an agent produces sits with whoever uses it.

The risks it treats are credential exposure, vulnerable or malicious dependencies, prompt injection,
and the generation of insecure or malicious code, each mapped onto an entry in a published list of
LLM application risks. Against each the post gives concrete measures, of which
[[DefinedTerm/sandboxing]] gets the fullest treatment: three approaches compared on effort,
stability, choice of editor and ease of integrating outside tooling.

Its final section argues that guardrails do not remove the need for human supervision, and takes
issue with the position that implementation code can be treated as a black box provided the tests
are reviewed.

## Key Points

- The author reports a personal productivity gain of roughly 1.5 to 3 times from working with AI
  coding agents, stated as a case-by-case impression rather than a measurement.
- Exhaustive verification of model output by the vendor is argued to be technically unreachable, on a
  worked estimate of the number of possible input–output combinations; the conclusion drawn is that
  output must be verified on the user's side. The estimate itself is attributed in the post to a
  model the author asked to compute it.
- Vulnerabilities and malicious code are said to be detectable-in-principle but not by test coverage:
  the post states plainly that full coverage can still miss both, which is the basis for its later
  argument against treating implementation as a black box.
- On dependencies the post names a specific trade-off: an agent's knowledge cutoff pushes it toward
  installing outdated versions carrying known vulnerabilities, while unconditionally installing the
  newest version exposes a project to supply-chain compromise. Its suggested middle path is a
  release-age delay, using the cooldown settings package managers and dependency bots now provide.
- The recommended permission posture is to curate `permissions.allow` and `permissions.deny` and then
  use an automatic-approval mode, with harmless operations actively added to the allow list. The
  reasoning is that too many prompts produce [[DefinedTerm/approval-fatigue]] — people approving
  without reading, which the post says lowers security rather than raising it.
- Skipping permissions entirely is described as unsuitable for work development; the author reports
  using it only for open-source work inside an isolated container.
- Three sandboxing approaches are compared. Dev Containers give network restriction and host
  isolation at medium effort but complicate secret retrieval, hook notifications and sharing user
  settings; a built-in agent sandbox needs only a settings file and is reported to cut permission
  prompts substantially, at the cost of a less mature runtime that is hard to debug when it
  misbehaves; a cloud IDE is quick to start and isolated but fixes the choice of editor.
- The post is explicit that the guardrails are not a checklist to complete: erring too far toward
  safety trades away speed, which it calls a business risk in its own right, and doing all of them
  still does not reduce risk to zero.
- Against the position that only tests need review, the post argues that reviewing a full-coverage
  test suite attentively is not realistic, and that the workable approach combines understanding the
  implementation with covering it by tests rather than choosing one.
- On how completely a reviewer must understand AI-written code the author declines to give an answer,
  observing that aiming at complete understanding costs disproportionately more than aiming at most
  of it, and suggesting review intensity be scaled to how mission-critical the code is.

## Context

The post is written from the perspective of someone using one specific agent, and says so: it notes
that its examples lean on [[SoftwareApplication/claude-code]] while holding that much of the argument
generalizes. Where the author states their own configuration — a built-in sandbox for closed-source
work, a container plus unrestricted permissions for open source — it is offered as one practitioner's
settled position rather than a recommendation.

Several of the concrete incidents and figures the post uses are drawn from elsewhere and cited as
such, including the supply-chain and prompt-injection cases it tabulates and the reduction in
permission prompts it attributes to a vendor's own engineering write-up.
