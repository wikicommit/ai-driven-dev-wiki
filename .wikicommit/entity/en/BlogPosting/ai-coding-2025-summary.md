---
title: "AI 编程 2025 总结：国产模型“能力追平”，国产编程工具还在“情感陪伴”"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, ai-assisted-programming, spec-driven-development, verification, industry]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/ai-coding-2025-summary/'
    hash: sha256:1eb970e45975be927b65ca9e4e1cd27a97cb998901d1d657940011e93c9f86db
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A December 2025 Chinese-language year-end review of AI coding by Phodal Huang, author of the open-source coding tool AutoDev, identifying six trends in 2025 and arguing that coding tools should compete on engineering certainty rather than on offering the developer emotional comfort."
  author: ["Phodal Huang"]
  datePublished: "2025-12-30"
---

Phodal Huang, who introduces himself in the post as the author of the open-source AI coding tool
AutoDev, frames this year-end review around a case study he had read of a Chinese AI coding tool that
spent considerable space on the agent's "added value" of comforting and encouraging a programmer who is
struggling. His response is a question: if the models and tools were really strong enough, why would
the experience need to be made up for with comfort? What a programmer needs when a problem will not
resolve, he argues, is a system that gets the job done.

The post then sets out six trends he saw in AI coding in 2025, with an emphasis on the Chinese
ecosystem, and closes by saying that in 2026 developers do not need a chat box that says "keep going"
but a "digital partner" that finds a system flaw at two in the morning and quietly submits a fix — and
that AutoDev's own path is to give the bandwidth spent on "emotional companionship" back to
"engineering certainty".

## Key Points

- Chinese coding models have begun following Claude's route of strengthening the coding ability and
  agentic behaviour of their main text models. Having tried MiniMax M2.1 and GLM 4.7 at year end, the
  author reports solid agentic behaviour — clear task planning, sensible tool calls, multi-step
  engineering operations — while noting a legacy-system migration scenario in which the model lost focus
  after a long conversation, and cautioning that high leaderboard scores do not carry over to every
  scenario.
- Many model vendors have gradually given up building their own AI coding tools and instead make their
  models usable inside mature existing tools, so that developers get the most mature tool plus a
  replaceable model — for example Chinese models inside [[SoftwareApplication/cursor]] or
  [[SoftwareApplication/claude-code]].
- Specifications are making a comeback alongside continued experimentation with
  [[DefinedTerm/context-engineering]]: he groups the rise of [[DefinedTerm/model-context-protocol]] and
  then of Skills, [[DefinedTerm/agents-md]] and [[DefinedTerm/spec-driven-development]] as coding tools
  exploring what better context engineering looks like. He points to Claude Code adding LSP support for
  gathering context at the end of the year, and calls file-operation-based agentic RAG too costly and
  prone to missing key context.
- The barrier to end-to-end tooling is falling: he cites Atlassian's Rovo Dev CLI and its integration
  with Jira and Bitbucket, GitHub Copilot's deeper integration with GitHub.com, Augment Code's review
  product, and Cursor's December acquisition of the code-review company Graphite, concluding that
  competition is moving from single capabilities to end-to-end closed loops.
- In what he calls an era of self-verification, tools have begun to take responsibility for their
  output — judging whether a task is actually complete rather than only whether the code runs. He cites
  testing agents such as Playwright's native agents and ScenGen using OODA-like loops, and Playwright's
  Healer Agent replaying failed steps to generate fixes.
- AI lowers the barrier to every technology stack, which he says also means AI is replacing repetitive,
  templatable work; the valuable work that remains is designing complex systems, planning engineering
  delivery and coordinating upstream and downstream processes.

## Context

The post is an opinion piece grounded in the author's own trials of tools and models; it reports no
measurements. On code review he describes having shown Augment's team, through enterprise access they
provided, what he thought an AI-era code-review agent should do — a structured summary of the whole
change, a diagram-level overview rather than fragmented comments, and continuity across the change's
lifecycle — and notes that the product now implements this, without claiming the direction came from his
feedback.
