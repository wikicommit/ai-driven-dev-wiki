---
title: "Building a C compiler with a team of parallel Claudes"
type: "schema:BlogPosting"
lang: en
tags: [multi-agent, agent-harness, autonomous-development, capability-benchmark]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/building-c-compiler'
    hash: sha256:76ec31b147cb595b08d33f9b46ece5a385276d3165f3c8ca4ab62600055ab111
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An Anthropic engineering report on tasking 16 parallel Claude instances with writing a Rust-based C compiler from scratch, and what the experiment taught about designing harnesses for long-running autonomous agent teams."
  author: "[[Person/nicholas-carlini]]"
  datePublished: "2026-02-05"
  publisher: "[[Organization/anthropic]]"
---

This post reports an experiment in which 16 agents were tasked with writing a Rust-based C compiler from scratch, capable of compiling the Linux kernel, and then largely left alone. Over nearly 2,000 Claude Code sessions and just under $20,000 in API costs the team produced a 100,000-line compiler that builds Linux 6.9 on x86, ARM and RISC-V.

Its author is explicit that the compiler is a side effect: the post focuses on what the project taught about designing harnesses for long-running autonomous agent teams — how to write tests that keep agents on track without human oversight, how to structure work so several agents can progress in parallel, and where the approach hits its ceiling. The project is framed as a capability benchmark, run across the Claude 4 model series, with the stated aim of stress-testing what models can *just barely* do today in order to anticipate what they will reliably do later.

## Key Points

- **The loop is deliberately minimal.** Existing agent scaffolds expect an operator to be online; a model given a long problem will eventually stop and wait for input. The harness here is a bash `while true` loop that starts a fresh Claude Code session as soon as the previous one finishes, with a prompt telling it to break the problem into small pieces, track what it is working on, and keep going. The post notes the resemblance to the [[DefinedTerm/ralph]] loop, and warns to run it in a container rather than on a real machine.
- **Parallelism is coordinated by git, not by an orchestrator.** Each agent gets a Docker container with a bare repo mounted, clones to a workspace, and pushes back when done. Task collisions are prevented by a lock file written into a `current_tasks/` directory — if two agents claim the same task, git's own synchronisation forces the second to pick another. There is no orchestration agent, no inter-agent messaging, and no enforced process for managing high-level goals; each agent decides what to do, usually picking the "next most obvious" problem. The author calls it a very early research prototype.
- **Test quality is the binding constraint.** Because the agent will autonomously solve whatever problem it is given, "it's important that the task verifier is nearly perfect, otherwise Claude will solve the wrong problem." When agents began breaking existing functionality with each new feature, the answer was a CI pipeline with stricter enforcement so new commits could not break existing code.
- **The harness is written for the model, not the author** — see [[DefinedTerm/agent-harness]] for the specific design rules this yielded.
- **A one-big-task ceiling, and the oracle that broke it.** With hundreds of independent failing tests, parallelism is trivial: each agent takes a different one. Compiling the Linux kernel is one giant task, so every agent hit the same bug, fixed it, and overwrote the others' changes — 16 agents did not help. The fix was to use GCC as a known-good compiler oracle: a harness compiled most of the kernel with GCC and only the remaining files with Claude's compiler, so a failure localised the bug to that subset and each agent could work on different files. Delta debugging was still needed afterwards to find pairs of files that failed together but worked independently.
- **Specialisation is a use of parallelism, not just throughput.** Beyond the agents solving the problem, one was tasked with coalescing duplicate code — the post notes LLM-written code frequently re-implements existing functionality — one with the compiler's own performance, one with the efficiency of the code it emits, one with critiquing the project's design from a Rust developer's perspective and restructuring accordingly, and one with documentation.

## Context

The evaluation section is unusually candid about limits. The run consumed 2 billion input tokens and generated 140 million output tokens over two weeks. The compiler is a clean-room implementation with no internet access during development, depending only on the Rust standard library; it compiles QEMU, FFmpeg, SQLite, postgres and redis, reaches a 99% pass rate on most compiler test suites, and can compile and run Doom. But it lacks a 16-bit x86 compiler and calls out to GCC to boot Linux out of real mode; it has no assembler or linker of its own; it builds many projects but not all; its generated code is less efficient than GCC's with all optimisations disabled; and its Rust code quality is described as reasonable but well below what an expert Rust programmer would produce. The author says he tried hard to fix several of these and was not fully successful, with new features and bugfixes frequently breaking existing functionality.

The post closes on discomfort rather than triumph. Its stated concern is that with autonomous systems "it is easy to see tests pass and assume the job is done, when this is rarely the case" — see [[DefinedTerm/verification-bottleneck]] — and the author, drawing on his own background in penetration testing, names the prospect of programmers deploying software they have never personally verified as a real concern. His summary is that the experiment both excites and unsettles him, and that the rapid progress in models and scaffolds "opens the door to writing an enormous amount of new code" in a way that will require new strategies to navigate safely.
