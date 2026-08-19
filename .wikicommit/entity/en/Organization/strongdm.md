---
title: "StrongDM"
type: "schema:Organization"
lang: en
tags: [agentic-coding, ai-assisted-programming, spec-driven-development]
sources:
  - type: url
    url: 'https://sddbook.blob.core.windows.net/downloads/spec-driven-development.pdf'
    hash: sha256:7f897827f00db69ac4a15f3acea3826e5504b1600d0b785cdce210d5414f1eea
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A company running a fully autonomous software operation — a Dark Factory — since July 2024, shipping production software with three engineers and no humans writing or reviewing code. Its two documented architectural innovations are external scenarios and digital twins of the services it integrates with."
---

StrongDM is cited in [[Book/spec-driven-development-ai-native-software-engineering]] as the clearest existing example of a [[DefinedTerm/dark-factory]] — a software operation in which agents build, test and ship the software and humans neither write nor review code. It shipped production software in 2025 with three engineers: no standups, no sprints, no Jira. The engineers specified what needed to exist and evaluated whether the output met the specification. Its AI compute bill ran to a thousand dollars per engineer per day, which the company considered a bargain.

[[Person/kevin-ryan]] dates the operation to July 2024 and argues that the interesting part is not the automation itself but two architectural innovations that generalise to anyone trying to move up the stack.

## History

The source ingested here does not cover StrongDM's founding or corporate history; it documents the company's autonomous engineering operation from July 2024 onward.

## Activities & Products

The first innovation is [[DefinedTerm/external-scenarios]]. Traditional tests live inside the codebase, where an AI can see them and — whether by design or optimisation pressure — build code that passes the tests without exhibiting the intended behaviour, the same problem as teaching to the test. StrongDM moved evaluation outside the codebase entirely, so the agent never sees the success criteria and cannot game them; Ryan compares the principle to a holdout set in machine learning.

The second is the use of [[DefinedTerm/digital-twin]] environments. StrongDM integrates with dozens of external services — Okta, Jira, Slack, Google Drive — and an autonomous agent cannot be allowed to make authenticated calls to production APIs during development. The company therefore built behavioural clones of every service, so agents develop against simulated environments that behave like reality but touch no real data.
