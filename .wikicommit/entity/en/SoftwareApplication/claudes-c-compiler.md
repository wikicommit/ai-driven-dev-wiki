---
title: "Claude's C Compiler"
type: "schema:SoftwareApplication"
lang: en
tags: [multi-agent, long-running-agents]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/building-c-compiler'
    hash: sha256:bb87bd35323bfc4ad526181ebcbea5616b7d93436bb9fcd985cf4d0f8de8a1c5
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A 100,000-line, Rust-based C compiler written from scratch by a team of 16 parallel Claude Opus 4.6 agents, able to build a bootable Linux 6.9 on x86, ARM and RISC-V."
  applicationCategory: "Compiler"
---

Claude's C Compiler is a C compiler written in Rust by a team of parallel Claude agents as an experiment in long-running autonomous development, described in [[BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes]]. It was specified as a from-scratch optimizing compiler with no dependencies, compatible with GCC, able to compile the Linux kernel and designed to support multiple backends; the human author specified some design points, such as an SSA intermediate representation to enable multiple optimization passes, but not how to implement them.

It was built over nearly 2,000 [[SoftwareApplication/claude-code]] sessions across two weeks by Claude Opus 4.6, at a total cost of just under $20,000. The implementation is described as clean-room — Claude had no internet access at any point during development — and depends only on the Rust standard library. Its source code is publicly available.

## Capabilities

The compiler is about 100,000 lines long and can build a bootable Linux 6.9 on x86, ARM and RISC-V. It can also compile QEMU, FFmpeg, SQLite, PostgreSQL and Redis, has a 99% pass rate on most compiler test suites including the GCC torture test suite, and can compile and run Doom.

Its announcement lists several limitations:

- It lacks the 16-bit x86 compiler needed to boot Linux out of real mode and calls out to GCC for that phase; its x86_32 and x86_64 compilers are its own, and on ARM and RISC-V it compiles entirely by itself. The compiler can output correct 16-bit x86, but the result is over 60kb, far beyond the 32k code limit Linux enforces.
- It has no assembler or linker of its own; those were the last parts Claude began automating and are described as still somewhat buggy, and the demo video used GCC's assembler and linker.
- It builds many projects but not all, and is not yet a drop-in replacement for a real compiler.
- Even with all optimizations enabled, its generated code is less efficient than GCC's with all optimizations disabled.
- The Rust code quality is described as reasonable but nowhere near what an expert Rust programmer might produce.

## Adoption & Ecosystem

The compiler was built as a capability benchmark rather than as a production tool, and it is presented as having nearly reached the limits of the model that wrote it: further fixes were not fully successful, and new features and bug fixes frequently broke existing functionality. Its development relied on a harness of parallel agents coordinating through git and lock files, and on using GCC as a known-good oracle so that different agents could work on different failing kernel files at once. Readers are invited to download it and try it on their own C projects.
