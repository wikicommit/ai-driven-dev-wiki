---
title: "comprehension debt"
type: "schema:DefinedTerm"
lang: en
tags: [code-quality, verification, ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://nyosegawa.com/en/posts/coding-agent-workflow-2026/'
    hash: sha256:bb7d36388cc5d0dc91fc90185585f6fff68833b1b198e732c6e2d6d41a285f45
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The debt that accumulates when code enters a codebase faster than anyone comes to understand it, leaving a team responsible for behaviour it cannot explain."
  termCode: ""
  inDefinedTermSet: ""
---

Comprehension debt is the gap that opens when generated code enters a codebase faster than any human comes to understand it. [[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] names the root cause as a five- to sevenfold difference between generation speed and comprehension speed, and lists it among the failure modes that define maturity in agent use rather than among ordinary quality problems.

## Usage

The survey's illustration is a first-person account it attributes to Addy Osmani: "tests passed, glanced over it, merged, three days later I couldn't explain how it works." It also relays research finding a 17% drop in skill acquisition among developers using AI assistance.

The countermeasure it names has two halves. First, have the agent generate a **linear walkthrough** of the code it produced — a pattern that survey attributes to Simon Willison. Second, reserve time for a human to actually read and understand it, which is a scheduling decision rather than a tooling one.

Its closing observation on the term is the ironic one: to stop being the code writer and become the supervisor, reading skill becomes *more* important rather than less.

## Related Terms

Comprehension debt is adjacent to [[DefinedTerm/verification-debt]] and the [[DefinedTerm/verification-bottleneck]], but names a different shortfall — not that the code went unchecked for correctness, but that nobody built a working model of what it does. Its skill-atrophy half connects it to the developer-experience moderating variable in the [[DefinedTerm/productivity-reliability-paradox]].
