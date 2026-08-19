---
title: "digital twin"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, ai-assisted-programming, testing]
sources:
  - type: url
    url: 'https://sddbook.blob.core.windows.net/downloads/spec-driven-development.pdf'
    hash: sha256:7f897827f00db69ac4a15f3acea3826e5504b1600d0b785cdce210d5414f1eea
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "In the agentic-development sense described by Kevin Ryan, a behavioural clone of an external service that an autonomous agent can develop against — a simulated environment that behaves like reality but touches no real data. Attributed to StrongDM, which built one for each of the dozens of services it integrates with."
---

In the sense used in [[Book/spec-driven-development-ai-native-software-engineering]], a digital twin is a behavioural clone of an external service: a simulated environment that behaves like the real service but touches no real data, so that an autonomous coding agent can develop and be tested against it safely. [[Person/kevin-ryan]] attributes the practice to [[Organization/strongdm]], describing it as one of two architectural innovations behind that company's [[DefinedTerm/dark-factory]] operation.

## Usage

The constraint that motivates it is straightforward: StrongDM integrates with dozens of external services — Okta, Jira, Slack, Google Drive are the examples given — and an autonomous agent cannot be allowed to make authenticated calls to production APIs during development. Rather than restricting what the agents could touch, the company built behavioural clones of every service. Ryan summarises the result as safe autonomous execution at speed.

He states that simulated environments, alongside external evaluation, are directly relevant to the methodology his book sets out and recur throughout it. Note that the term "digital twin" has a broader established meaning outside software engineering; the definition recorded here is the narrower agentic-development usage the source describes, and the source does not claim to be defining the term generally.

## Related Terms

Digital twins are one of the two StrongDM innovations Ryan documents; the other is [[DefinedTerm/external-scenarios]]. Both are presented as prerequisites for operating a [[DefinedTerm/dark-factory]], and both belong to what Ryan calls AI-native execution — the machinery that turns a specification into running software and validates the result. See also [[DefinedTerm/agent-execution-environment]].
