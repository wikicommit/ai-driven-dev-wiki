---
title: "Are Harnesses Worth the Cost?"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, coding-agents, verification, contract-testing]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/are-harnesses-worth-the-cost.html'
    hash: sha256:3baedf6f6c5150f062e0a3c5f7a5c6d8a88fe3edce290137be55d057888a85dc
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "An experiment, published on martinfowler.com in the Exploring Gen AI series, comparing coding agents building the same API service with and without a behavioral harness, which found the harness added only overhead for a frontier model but turned a cost-optimized model's 3-in-10 success into 10-for-10 at lower cost than the unharnessed frontier model."
  author: ["Naresh Jain"]
  datePublished: "2026-10-13"
  publisher: "martinfowler.com"
---

The article reports an experiment testing whether a behavioral harness — in the author's framing,
borrowed from Birgitta Böckeler, a combination of [[DefinedTerm/guides-and-sensors]] — makes coding
agents more reliable. The author expected the harness to help an agent meet requirements more reliably,
save tokens and prevent wasted work. Using Codex, agents built the same backend-for-frontend (BFF)
service for product discovery from a detailed application brief, with and without the harness, in
isolated Docker containers with fresh state for each attempt. The service had to expose an HTTP API,
validate requests and downstream responses, call an Order API, publish the first returned product to
Kafka, and follow specified behaviour for timeouts and failures, including a deferred `202` workflow
with a pollable monitor link.

Development and evaluation were separated into two loops. In the inner loop, harnessed agents received
OpenAPI and AsyncAPI specifications, request-response examples and an API-development skill as guides,
and contract checks, API tests and assertions on side effects — downstream mock calls and Kafka
publication — as sensors, which the agent invoked through the project's test command. The author
implemented this harness with Specmatic, noting that equivalent contract-testing and service
virtualization tools could do the same. In the outer loop, an evaluation harness the agents never saw
ran 178 automated acceptance checks against every finished application. The results contradicted the
author's expectation for the frontier model, and led him to a revised, conditional hypothesis about
when sensors should run.

## Key Points

- With GPT-6 Sol at low reasoning effort, all 10 runs passed all 178 acceptance checks both with and
  without the harness; the harness used about 10.5 times as many tokens, took nearly 3 times as long
  and cost about 7 times more, with no observed improvement.
- With GPT-6 Luna, a cost-optimized model, at low reasoning effort, 3 of 10 unharnessed runs succeeded
  against all 10 harnessed runs; the harness added about 3.9 times the tokens, but a harnessed Luna run
  cost about 33% less than an unharnessed Sol run ($0.273 against $0.406), with the same 10-for-10
  result.
- In exploratory runs, Claude Sonnet 4.6, Claude Opus 4.6 and Gemini 3.8 Flash also completed the task
  unassisted on the first try.
- Unharnessed Luna runs passed 94.8% of the functional checks, and the failed applications still
  passed at least 144 of the 178; their failures clustered at protocol boundaries, resiliency paths
  and integration seams — the deferred-creation timeout workflow, Kafka wire-contract details, exact
  HTTP error contracts and a mismatched configuration name.
- To keep guides and sensors from contradicting each other, the harness validated the example
  payloads against the specifications before any test ran, and the agent was told to preserve the
  supplied contracts and examples and fix the implementation rather than weaken the expectations, so
  that verification had a source independent of the implementing agent's own interpretation.
- The author interprets the harness as [[DefinedTerm/executable-attention]]: feedback that brings a
  requirement the agent was given, but dropped during implementation, back into focus when a sensor
  goes red.
- The same sensors, the article argues, serve two purposes: steering construction during development
  and providing the basis for accepting the work at completion.
- Its practical recommendation is to run a behavioral harness throughout development for
  cost-optimized models with inconsistent results, to run the same tests once as a deterministic final
  verification gate for frontier models, and to invest in clear specifications and examples, since the
  checks can enforce only the expectations humans encode.
- The cost figures are API-equivalent estimates covering only autonomous generation; they exclude the
  effort of authoring and maintaining the contracts and harness, and of diagnosing and repairing failed
  results.

## Context

The author is explicit about the experiment's limits: 10 paired runs per model on one greenfield Java
service, both models at low reasoning effort, and a brief detailed enough to favour an unaided agent.
He has not tested legacy code, other languages or reasoning settings, or vague requirements; the
experiment cannot separate the contributions of guides from those of sensors, and the small sample
cannot establish long-run reliability or the total cost of reaching an acceptable application. He
proposes as next steps measuring a "final gate only" condition for frontier models, varying the quality
of the brief, and testing on existing codebases, other languages and locally run open-weights models.
The article draws its vocabulary of guides and sensors, and of computational versus inferential
controls, from [[BlogPosting/harness-engineering-for-coding-agent-users]].
