---
title: "backpressure"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, code-quality, agentic-loop]
sources:
  - type: url
    url: 'https://ghuntley.com/ralph/'
    hash: sha256:9836ee3ee0773613f370a27796b1e456199be38681f73a47b974e210dd356317
  - type: url
    url: 'https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents'
    hash: sha256:210c3b64f14464d0f411066d18a2164f9d8b5069812277a8a440cb571d86e3f1
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "In Geoffrey Huntley's framing of agentic loops, any automated mechanism wired into the loop that rejects invalid code generation — a type system, test suite, static analyser, or security scanner — chosen for how fast it can reject as much as for how thoroughly."
  termCode: ""
  inDefinedTermSet: ""
---

Backpressure, as [[Person/geoffrey-huntley]] uses the term for agentic loops in [[BlogPosting/ralph-wiggum-as-a-software-engineer]], is whatever is wired into the loop to reject invalid code generation. His framing splits an unattended loop into two phases: generation, which is now cheap, and backpressure, which is where "you need to have your engineering hat on" — because when generating code is easy, the hard part becomes ensuring the right thing was generated.

## Usage

Huntley's claim is that anything producing a machine-readable pass or fail can serve this role: type systems, test suites, static analysers, security scanners. Statically typed languages provide some of it inherently through their type system; for dynamically typed languages he stresses wiring in a static analyser or type checker explicitly, naming Dialyzer for Erlang and Pyrefly as examples, and warns that skipping this leads to "a bonfire of outcomes."

The selection criterion he emphasises is throughput rather than rigour alone — "the speed of the wheel turning that matters, balanced against the axis of correctness." His worked example is Rust: he chose it for CURSED because a compiler demanded extreme correctness, while noting that slow compilation and the models' difficulty producing correct Rust on the first attempt mean more attempts and a slower loop, which he presents as a trade-off rather than a mistake.

A staple prompt in his loop pairs generation with immediate verification: after implementing functionality or resolving a problem, run the tests for that unit of code, and treat missing functionality as something to add per the specifications rather than stub out. He extends the obligation to unrelated failures, instructing the agent to fix tests that break outside its current work as part of the same increment of change.

The term also has a second, opposite sense in the same post. Huntley warns that fanning out to hundreds of parallel [[DefinedTerm/subagents]] all running builds and tests produces "bad form back pressure" — here meaning contention that degrades the loop rather than a check that protects it — which is why his prompt allows many subagents for search and file writing but only one for build and test.

### Verification has to be context-efficient too

[[BlogPosting/skill-issue-harness-engineering-for-coding-agents]] uses the term in Huntley's first sense and adds a constraint his account does not: the check must be cheap in context as well as fast in wall-clock. Its stated core insight matches his — the likelihood of solving a problem with a coding agent is strongly correlated with the agent's ability to verify its own work — and that team calls building these mechanisms into their repository "one of the highest-leverage things we have spent time on." Their inventory is typechecks and build steps, unit and integration tests, code coverage reporting with a Stop hook that prompts the agent when coverage drops, and UI interaction testing.

The constraint comes from a specific failure they report: running the full test suite after every change flooded the context window with 4,000 lines of passing tests, after which the agent lost track of the actual task and began hallucinating about test files it had just read. Their fix was to swallow the output and surface only errors, applied to builds as well — success silent, failure verbose. The same post lists running a five-minute test suite at the end of every session among the things that did not work for them, recommending a subset instead.

## Related Terms

Backpressure is the verification half of [[DefinedTerm/ralph]], and its underlying idea — give the agent something that returns a pass or fail so the loop closes without a human in it — recurs across [[DefinedTerm/agentic-coding]] practice. Related mechanisms include the automated testing and continuous integration that [[DefinedTerm/vibe-engineering]] lists among the practices LLMs reward, the quality gates of [[DefinedTerm/llm-as-judge]] where the checker is another model rather than a deterministic tool, and the event-triggered checks covered under [[DefinedTerm/agent-hooks]].
