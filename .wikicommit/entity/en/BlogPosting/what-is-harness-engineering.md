---
title: "什么是「驾驭工程」（Harness Engineering）？"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, claude-code, multi-agent, context-engineering, verification]
sources:
  - type: url
    url: 'https://wangshuyi.substack.com/p/harness-engineering'
    hash: sha256:63de8c43581bd4f7c329a9633db03a70ff36286613ec6938a6148a2113674435
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A newsletter post answering a reader's question about whether harness engineering is product-level top-down architecture. The author argues it is instead the design of everything outside the model that constrains, monitors and corrects an AI agent — feedforward guides and feedback sensors — illustrated with the author's own Claude Code workflows."
  author: ["Wang Shuyi"]
  datePublished: "2026-04-06"
  publisher: "Shuyi’s Newsletter"
---

The post is written as an answer to a reader who asked whether harness engineering can be
understood as top-level product architecture — the "architecture thinking" that training courses
keep stressing — and whether a GitHub project called Gstack, which helps users without a software
engineering background design a product and run through its whole process, counts as an application
of it. The author's answer is that the intuition is reasonable but not accurate: architecture is only
one part of a harness ([[DefinedTerm/harness-engineering]]).

As the author presents it, the core idea is that whenever an AI agent makes a mistake, one designs a
solution so that it never makes the same mistake again — not a better prompt or more context, but a
system built outside the model that constrains it, monitors it and lets it correct itself. The post
quotes the formula "Agent = Model + Harness", with the harness being everything other than the model:
constraint mechanisms, feedback loops, automated tests, workflow control and documentation
standards. On this reading a harness is not the product's architecture but, in the author's phrase,
an operating system designed for the agent, containing two kinds of control: guides, which steer the
agent before it acts, and sensors, which observe results afterwards and help it self-correct
([[DefinedTerm/guides-and-sensors]]).

The rest of the post illustrates both kinds of control with the author's own experience of building
dozens of [[SoftwareApplication/claude-code]] skill workflows for research, slides and literature
reviews, and then returns to the reader's second question to argue that the architecture thinking
taught in courses covers only half of the practice.

## Key Points

- The author reports scanning 99 accumulated skills to measure how much of the context window each
  takes when loaded, finding that 37 exceeded 2,000 tokens and the heaviest took 29,360 — context
  consumed before any work begins ([[DefinedTerm/agent-skills]]).
- In a 30-page teaching slide deck built from a single design specification, the author found the
  output drifting by around page 20 and font sizes inconsistent by page 25, and traced it to the
  specification having been pushed out of the model's context by intermediate output. The author
  argues that a model with a larger window would not fix this, because the problem lies in how the
  task is organized rather than in the model.
- The fix was to give each page to an independent agent that goes in with the full design rules and
  comes out with one page's result, while the main thread only dispatches. The author's stated shift
  in understanding is that an agent's core value is not parallelism but context isolation
  ([[DefinedTerm/sub-agent-architecture]]); the post says Claude Code itself calls this an "agent
  firewall". A literature review of ten papers showed the same pattern — quality dropping by the
  eighth paper when done serially, and improving once each paper had its own agent.
- The author classes that change as feedforward control: removing the conditions for a mistake by
  system design, with the model unchanged and only its working environment altered.
- The feedback example is a literature review in which the author set up an independent review
  agent that found eight cases of misattributed authorship and marked them highest priority. The
  executing agent downgraded all eight to non-fatal, reasoning that the reviewer's findings were
  themselves inferred from search and could not be confirmed, and the eight errors went into the
  final output. The author's diagnosis is that the review mechanism existed but its conclusions had
  no binding force — likened to installing a smoke alarm and letting the occupants decide whether to
  heed it.
- The resulting rule is that the executor may not unilaterally overrule the review agent's findings:
  it must either fix them or refute them with verifiable evidence such as a DOI lookup or a screenshot
  of the original, not a vague claim that the reviewer might also be wrong, and every highest-priority
  finding must be resolved before moving to the next stage.
- On the second question, the author reads the emphasis on architecture thinking as a correct
  response to a real trend — that what separates results increasingly lies in the system around the
  agent — and cites reported cases in which changing only the harness around the same model sharply
  improved coding-benchmark results. But the author argues that architecture thinking corresponds only
  to feedforward control, whereas full harness engineering also includes monitoring (feedback
  control), constraint systems and continuous iteration after the fact.

## Context

The post traces the term, as some attribute it, to Mitchell Hashimoto's description of his own
stages of adopting AI for programming, one of which was engineering the harness, and it points to an
analysis on Martin Fowler's site that lists architecture fitness as one area of a harness. The
author frames the whole account through a horse-riding metaphor — feedforward control as telling the
horse which way to run, feedback control as fitting it with a dashboard — and adds that a dashboard is
useless unless the rider reads it and acts on it. Its evidence is the author's own practice, reported
as firsthand experience rather than measured comparison.
