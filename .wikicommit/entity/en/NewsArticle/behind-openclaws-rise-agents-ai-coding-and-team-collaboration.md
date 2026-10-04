---
title: "OpenClaw 走红背后：Agent、AI Coding 与团队协作的新问题"
type: "schema:NewsArticle"
lang: en
tags: [qcon, spec-driven-development, enterprise-ai-adoption, agent-safety]
sources:
  - type: url
    url: 'https://www.infoq.cn/article/D8E3q93kBviq8Z8mu0Ao'
    hash: sha256:a19a7c7520ea6086e1939c2775ea090be3cbbe7f9aaa86c470b64ba576357da7
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An edited InfoQ China livestream roundtable, published in March 2026 ahead of QCon Beijing 2026, in which practitioners from Taobao Shangou, NetEase CodeWave and Ping An Technology discuss OpenClaw's rise, its practical limits and risks, and how teams can keep AI coding controllable through spec-driven development, generated tests and shared rules."
  datePublished: "2026-03-30"
  publisher: "InfoQ"
---

The article ("Behind OpenClaw's rise: new problems for agents, AI coding and team collaboration") is InfoQ China's edited write-up, dated 30 March 2026, of an episode of its livestream programme run with QCon in the run-up to QCon Beijing 2026, held 16–18 April. Its participants are a senior technical expert at Taobao Shangou, the technical lead of NetEase CodeWave's business centre and a senior expert engineer at Ping An Technology, and the text is their conversation as condensed by InfoQ, so its claims are the speakers' own accounts of their teams' experience rather than independent reporting.

The first half is about [[SoftwareApplication/openclaw]]: why it appeared when it did, what using it is actually like, and its architecture, costs and security exposure. The second half turns to AI coding in teams, where the speakers agree that the central problem is not generating code but keeping it controllable, and discuss when to use [[DefinedTerm/vibe-coding]], when to require [[DefinedTerm/spec-driven-development]], and which guardrails work.

## Key Points

- One speaker presents OpenClaw, like Manus, as the natural result of capabilities crossing a threshold rather than a sudden breakthrough, citing its use of a long-context Claude model, [[DefinedTerm/programmatic-tool-calling]] and skills, and calls it a "product–technology fit"; its innovation, he says, was connecting a desktop agent to chat tools through a channel gateway.
- The speakers dispute that it is a low-barrier product: using it well, one says, requires familiarity with JSON configuration, troubleshooting ability and continual tuning of skills. They report heavy token consumption, unstable configuration files that can be rewritten or corrupted on restart, and an agent that, given an unclear instruction to analyse a page's APIs, called a delete endpoint and erased the user's comments.
- One team, using it on cloud desktops for compliance reasons, stopped letting the AI change code directly and instead had it produce a design-document-level change proposal with an HTML report of candidate code snippets; the speaker says about 60% of the snippets were directly usable.
- Asked what the biggest real problem with AI coding is in 2026, the NetEase speaker names instability and lack of control: misunderstood requirements, technology stacks that differ from the team's own, and poor maintainability. His example is an AI that implemented a screenshot tool by calling a third-party screenshot API instead of the headless browser the team intended.
- The Ping An speaker says technical standards can be turned into executable rules with CI/CD and tools such as ArchUnit and PMD, but that getting AI to follow business-level rules is much harder; a single AI asked to self-check against its prompt is, in his experience, confidently wrong until a human points out the specific violation.
- Several speakers recommend having a different model, or at least a fresh session with its own context window, review generated code (see [[DefinedTerm/cross-model-review]]), and argue that practices such as BDD and TDD gain value because AI can now write the tests.
- The NetEase team uses [[DefinedTerm/easy-approach-to-requirements-syntax]] to remove ambiguity from requirements, and the speaker says Amazon's [[SoftwareApplication/kiro]] brought EARS into spec-driven development in 2025.
- On when to vibe and when to write a spec first, the speakers converge on exploratory, throwaway or low-precision work for vibe coding and spec-driven development for systems with clear requirements that must be maintained; one proposes judging by complexity and precision requirements, and another says even without a full spec flow a reviewed plan (for example in Claude Code's plan mode) should come before execution.
- On review and responsibility, the speakers say product managers and architects must take part in spec and architecture review, tests should be generated from the spec and run in CI/CD, and the developer remains responsible for AI-written code. The Ping An speaker describes [[SoftwareApplication/openspec]]'s proposal, task, apply and archive flow and stresses archiving successful solutions as reusable knowledge.
- Their three most effective guardrails: standardising requirements (for example with EARS), test generation run in CI/CD, and team-wide shared skills, lint and CI rules and a constitution; plus monitoring, gradual rollout and rollback before release.
- For legacy systems, the NetEase speaker recommends [[SoftwareApplication/deepwiki]]-style repository analysis combined with requirements documents, design documents and bug history, and the Ping An speaker describes focusing knowledge work on the roughly 20% of files that change most often.
- On a reported exposure of OpenClaw instances, one speaker attributes it to users publishing the console port or binding it to the LAN and says the console can be restricted to the local machine; another argues the risk remains because the agent acts with the user's permissions and may not match the user's intent, suggesting an intent-level control beyond RBAC.

## Context

The roundtable was organised to promote QCon Beijing 2026's track on coding-agent-driven R&D, and InfoQ notes that the text was condensed from the livestream. The NetEase speaker says his team began practising spec-driven development after Kiro's release the previous September, and that after NetEase's leadership put forward a "spec first" principle almost all of its business units are trying to adopt it at scale; these and the percentages quoted are the speakers' own reports.
