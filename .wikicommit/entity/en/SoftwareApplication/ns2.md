---
title: "NS2"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-architecture, orchestration, verification, multi-agent]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.17799'
    hash: sha256:98d0e3aebf3d1c5ab551f46a6c1f719389e820d2be1490bfefd669d87c107e69
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An open-source, issue-driven system harness that runs a four-tool agent loop under a stack of deterministic and agent-arbitrated checks, using GitHub issues as its coordination primitive."
  applicationCategory: "System harness for agentic software engineering"
  featureList: "Issue-driven task decomposition; isolated per-issue implementation sessions; reviewer, test-quality, smoke-testing and pull-request-building agents; layered inner-, middle- and outer-loop verification"
---

NS2 is an issue-driven [[DefinedTerm/system-harness]] that runs a four-tool agent loop under a stack of deterministic and agent-arbitrated checks. It was built and open-sourced by the authors of [[ScholarlyArticle/coding-benchmarks-are-misaligned-with-agentic-software-engineering]], who publish it at <https://github.com/drufball/ns2> and draw on it throughout that paper as a concrete reference. They state that building and operating it surfaced many of the benchmark misalignments the paper articulates.

Its organising idea is that GitHub issues are the coordination primitive. A product-manager agent decomposes a feature issue into vertical-slice child issues; software-engineering agents implement those issues in isolated sessions; and reviewer, test-quality, smoke-testing and pull-request-building agents consume issue and pull-request events to decide whether work should move forward, be revised, or be described for review. The paper places NS2 among the harnesses that treat the issue tracker as the durable state machine for work and spawn a separate agent session per task.

## Capabilities

NS2 is presented as a worked instance of a layered verification stack rather than a single checker. Max-pedantic lint, a coverage threshold and dependency-graph unit tests act as inner-loop strict verifiers — the fast, blocking checks that run inside a single change attempt. Mutation testing, LCOM cohesion checks, and daily agentic architecture and test-quality reviews serve as middle-loop feedback, aggregating over a wider slice of work than any one change. Friction reports from a smoke-testing agent, post-merge revert signals and production incidents act as outer-loop feedback.

Some of those components are evaluation targets for others: the paper notes that in NS2 mutation testing evaluates the quality of a unit-test suite, and an agentic linter-quality review evaluates the lint configuration — what it calls a stack of verifiers-of-verifiers. The paper also states that the agent writes and maintains the lint rules and rubrics that constrain it.

## Adoption & Ecosystem

NS2 is the authors' own harness, published as open source, and the paper names it alongside Symphony and GasCity as recent work operating at the level of the system harness rather than the individual agent harness. It integrates with GitHub issues and pull requests as its coordination surface, with a lint configuration, a coverage threshold, dependency-graph unit tests and mutation testing as checks, and with post-merge revert signals and production incidents as feedback.
