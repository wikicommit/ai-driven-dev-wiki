---
title: "Nova"
type: "schema:ComputerLanguage"
lang: en
tags: [programming-languages, effect-systems, ai-assisted-development]
sources:
  - type: url
    url: 'https://habr.com/ru/articles/1043394/'
    hash: sha256:b1c46bd96d1f67f65b893293dc56fd1234cea6e9556c6d7a1ddf949fa4f378d7
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An open-source programming language, built largely by autonomous Claude Code agents, that declares a function's side effects in its type so that a reviewer can see from the signature what the function actually does."
  url: "https://github.com/nv-lang/nova"
---

Nova is a programming language designed, in its author's words, with the AI era in mind. Its premise is that when most code is written by LLMs, a language should move side effects into types, so that a reviewer — human or model — can tell from a function's signature that it reads a database, can fail with a particular error, reads the time or writes to a log, without reading the body or guessing from the name. The author acknowledges that the idea is not new, pointing to the academic languages Koka, Eff and Effekt, and presents Nova as an attempt to make an effect system practical, with a standard library aimed at backend work and at being used together with LLMs.

The language and its compiler are developed by a single author working with [[SoftwareApplication/claude-code]] agents that execute human-reviewed implementation plans, a process described in [[BlogPosting/a-month-building-the-nova-language-with-claude-code]]. The repository is public under the MIT license.

## Details

A Nova function type lists its parameters, a list of effects and its return type; the author's example is a money-transfer function whose effects include database access, a typed failure for insufficient funds, time and logging. Nova also has contracts that state what a function requires and guarantees, checked at compile time through an SMT solver.

The compiler generates C code, which is then compiled with an ordinary C compiler; the author considers this the right choice at the language's current stage because many bugs are caught by inspecting the generated C. The runtime has a fiber scheduler, uses the Boehm conservative garbage collector and libuv for asynchronous I/O, and the standard library was under active development at the time of writing. An early interpreter mode existed alongside code generation but was largely abandoned because maintaining two execution paths cost too much.

The memory model changed during development: an opt-in cycle-collection design with per-field memory prefixes for real-time guarantees was dropped in favour of managed memory with a garbage collector by default, with real-time behaviour kept as an opt-in `region { ... }` block for zones such as audio, trading or embedded code.
