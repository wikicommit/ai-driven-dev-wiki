---
title: "Ralph Wiggum as a \"software engineer\""
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, agentic-loop, ai-assisted-programming]
sources:
  - type: url
    url: 'https://ghuntley.com/ralph/'
    hash: sha256:9836ee3ee0773613f370a27796b1e456199be38681f73a47b974e210dd356317
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A 14 July 2025 post in which Geoffrey Huntley describes [[DefinedTerm/ralph]] — running a coding agent in an unattended shell loop, one task per iteration — and the tuning practices he used to build a programming language with it."
  author:
    - "[[Person/geoffrey-huntley]]"
  datePublished: "2025-07-14"
  publisher: ""
---

"Ralph Wiggum as a 'software engineer'" is a post published on 14 July 2025 in which [[Person/geoffrey-huntley]] sets out [[DefinedTerm/ralph]], a technique that in its purest form is a Bash loop feeding a fixed prompt file to a coding agent over and over. The post's framing is that the technique is "deterministically bad in an undeterministic world": each loop will fail in identifiable ways, and those failures are addressed by adding instructions to the prompt rather than by changing tools.

The post is written from Huntley's experience building CURSED, a new programming language and compiler he says was built by Ralph, including programming in a language absent from the model's training data. It presents the prompts he was using at the time, the failure modes he ran into, and the reasoning behind each correction, rather than offering a reusable recipe — he states explicitly that there is no such thing as a perfect prompt and that taking his verbatim will not reproduce his outcomes, because the prompt evolved through continual observation of model behaviour.

Its overall claim is that Ralph can replace the majority of outsourcing for greenfield projects, while insisting that senior expertise remains necessary to guide it. Huntley writes that anyone claiming a tool can do 100% of the work without an engineer is "peddling horseshit," and separately that he would not use Ralph on an existing codebase.

## Key Points

- **One item per loop.** Huntley repeats that the agent should be asked to do one thing per iteration, and that the operator must trust it to choose which thing is most important. He relaxes this only as a project stabilises, and narrows back to one item when results go off the rails.
- **Deterministic stack allocation.** Each loop should allocate the same things into context: the plan file (`fix_plan.md`) and the specifications. He accepts that re-spending the context allocation every loop is wasteful, on the grounds that a fuller context window produces worse outcomes.
- **Subagents as the context strategy.** The primary context window should act as a scheduler that dispatches [[DefinedTerm/subagents]] for expensive work such as searching the filesystem or summarising whether a test suite passed. He notes that fanning out hundreds of subagents onto build and test steps produces "bad form back pressure," so his prompt permits many parallel subagents for search and file writing but only one for building and testing.
- **Two phases: generate, then [[DefinedTerm/backpressure]].** Generation is cheap and steered by specifications and a project-specific standard library; the hard part is rejecting output that is wrong. Type systems, test suites, static analysers, and security scanners are all described as things that can be wired in for this purpose, balanced against how fast the loop can turn.
- **Tune with "signs," not blame.** The post's recurring metaphor is adding a sign next to the slide so Ralph looks before jumping. Recurring failures — assuming code is unimplemented after a `ripgrep` search, writing placeholder implementations — are each answered with an added instruction, and Huntley frames blaming the tools rather than the operator as the wrong response.
- **Capture reasoning for future loops.** Because each loop begins with a fresh context window, he instructs the agent to document why a test and its implementation matter, describing this as leaving notes for future iterations that will not have the reasoning in context.
- **Expect breakage.** He states plainly that operators will sometimes wake to a codebase that does not compile, and that the judgment call is whether to `git reset --hard` and restart the loop or write new prompts to rescue it.

## Context

The post positions Ralph against the multi-agent and agent-to-agent communication work Huntley says he encountered in San Francisco at the time, arguing by analogy that non-deterministic microservices would be "a red hot mess" and that a monolithic single process doing one task per loop is preferable. It also links out to several of his earlier posts on specifications, subagents, and context-window behaviour, which he treats as prerequisites rather than restating.

Huntley states his own caveats directly: he expects CURSED to have significant gaps, describes the repository as full of garbage, temporary files, and binaries, and asks readers not to circulate it. He also anticipates the maintainability objection and answers it rhetorically rather than empirically — questioning why humans should be the frame for maintainability when loops can be re-run to adapt code. Readers should treat the reported economics in the post, including a second-hand figure of a $50,000 contract delivered for $297, as an anecdote relayed from a private message rather than a measured result.
