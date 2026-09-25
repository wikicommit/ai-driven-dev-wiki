---
title: "Building a C compiler with a team of parallel Claudes"
type: "schema:BlogPosting"
lang: en
tags: [long-running-agents, harness-engineering, multi-agent]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/building-c-compiler'
    hash: sha256:bb87bd35323bfc4ad526181ebcbea5616b7d93436bb9fcd985cf4d0f8de8a1c5
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An Anthropic engineering post reporting an experiment in which 16 Claude Opus 4.6 agents, running in parallel in an unattended loop, built a Rust-based C compiler capable of building the Linux kernel, and drawing lessons about designing harnesses for long-running autonomous agent teams."
  author: ["Nicholas Carlini"]
  datePublished: "2026-02-05"
  publisher: "[[Organization/anthropic]]"
---

The post, written by a researcher on [[Organization/anthropic]]'s Safeguards team, describes an approach to supervising language models that the author calls "agent teams": multiple Claude instances working in parallel on a shared codebase without active human intervention. To stress-test it, 16 agents were tasked with writing a Rust-based C compiler from scratch that could compile the Linux kernel. Over nearly 2,000 [[SoftwareApplication/claude-code]] sessions and about $20,000 in API costs, the team produced [[SoftwareApplication/claudes-c-compiler]], a 100,000-line compiler that can build Linux 6.9 on x86, ARM and RISC-V.

The author frames the compiler as an interesting artifact but puts the weight of the post on what the experiment taught about designing harnesses for long-running autonomous agent teams: how to write tests that keep agents on track without human oversight, how to structure work so several agents can progress in parallel, and where the approach reaches its ceiling. The project was also designed as a capability benchmark, used across the Claude 4 model series to probe what models can only just achieve today.

The harness itself is deliberately bare-bones. Each agent runs Claude Code in an infinite shell loop inside its own Docker container, cloning from a shared bare git repository and pushing back to it; a new session starts in a fresh container as soon as the previous one ends. The author notes the loop will look familiar to anyone who has seen a [[DefinedTerm/ralph-loop]], and advises running it in a container rather than on one's own machine.

## Key Points

- Existing agent scaffolds such as Claude Code are described as needing an operator online, because on a long problem the model eventually stops to wait for input; running it in a loop is the author's way to elicit sustained autonomous progress.
- Agents avoid duplicating work through a simple lock: an agent claims a task by writing a text file to a `current_tasks/` directory, and git's synchronization forces a second agent claiming the same task to choose another.
- There is no orchestration agent and no other inter-agent communication; each agent decides for itself what to do, and in most cases picks up the "next most obvious" problem.
- Most of the author's effort went into the environment around Claude — the tests, the environment and the feedback — rather than into the loop itself.
- The task verifier must be nearly perfect, because an autonomous agent will otherwise solve the wrong problem; a continuous integration pipeline with stricter enforcement was added when new features began breaking existing functionality.
- Because each agent starts in a fresh container with no context, the agents were instructed to maintain extensive READMEs and progress files.
- Test output was designed around two stated model limitations: context window pollution (print a few lines, log the rest to files, put `ERROR` and its reason on one line for grep) and time blindness (a default `--fast` option runs a deterministic per-agent random 1% or 10% sample).
- Parallelism was easy while there were many independent failing tests, but broke down on the Linux kernel, a single giant task on which every agent hit and fixed the same bug.
- The fix was to use GCC as a known-good compiler oracle: compile most of the kernel with GCC and only a random remainder with Claude's compiler, so different agents could chase different bugs in different files.
- Parallelism also allowed specialized roles — one agent coalescing duplicate code, others working on compiler performance, efficiency of the generated code, a Rust-developer design critique, and documentation.
- The run consumed about 2 billion input tokens and 140 million output tokens over two weeks; the author judges the cost to be a fraction of what producing the compiler himself, let alone with a team, would have cost.
- The author reports that earlier Opus 4 models were barely able to produce a functional compiler and that Opus 4.5 was the first to pass large test suites while still failing on real large projects.
- The resulting compiler is said to have nearly reached the limits of Opus's abilities: attempts to fix its remaining limitations were not fully successful, and new features and bug fixes frequently broke existing functionality.

## Context

The post is a single researcher's first-hand account of one experiment, written for Anthropic's engineering blog, and the author calls the harness a very early research prototype. It closes on a note of caution rather than triumph: fully autonomous development is said to carry real risks, since for an autonomous system it is easy to see tests pass and assume the job is done when that is rarely the case, and the author — who previously worked in penetration testing — names programmers deploying software they have never personally verified as a real concern. The author says the experiment both excites him and leaves him uneasy.

Its emphasis on externalizing progress into files and on test output shaped for a model's context places it alongside this wiki's other accounts of [[DefinedTerm/long-running-agent]] design and [[DefinedTerm/harness-engineering]].
