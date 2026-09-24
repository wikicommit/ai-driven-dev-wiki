---
title: "Mise en Place for Agentic Coding: Deliberate Preparation as Context Engineering Methodology"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, context-engineering, vibe-coding, spec-driven-development, multi-agent]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.05400'
    hash: sha256:1f126c8e3d5e00a7ac0db71cd27186c357be2d109f14c9979f133b56b18b3303
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper proposing mise en place (MEP), a three-phase preparation methodology for agentic coding, illustrated with a single hackathon case study, and introducing context fluency as an emerging developer skill."
  author: ["Andrew Zigler"]
  abstract: "The paper argues that the dominant vibe-coding workflow creates a systematic alignment problem, in which agents lacking sufficient context produce code that needs extensive debugging and refactoring. Drawing on the culinary concept of mise en place, it proposes a three-phase preparation methodology — contextual grounding, collaborative specification and task decomposition — reports its application during a competitive hackathon where roughly two hours of preparation enabled rapid parallel implementation of a full-stack educational platform by concurrent AI agents, introduces context fluency as an emerging developer skill, and sets out a research agenda for empirically validating preparation-phase methodologies."
  keywords: ["agentic coding", "mise en place", "context engineering", "vibe coding", "context fluency"]
---

This paper, by an author at LinearB and published for VibeX 2026 (Glasgow, June 2026), argues
that the bottleneck in agentic coding is not code generation but alignment between developer intent
and agent output. It traces that alignment problem to [[DefinedTerm/vibe-coding]], which it
describes as the dominant workflow pattern: the developer states an intent, the agent produces code,
and misalignments are resolved through iterative correction. The author's claim is that the
alignment problem is fundamentally a preparation problem, and the paper's answer is
[[DefinedTerm/mise-en-place-methodology]] — a preparation-first methodology named after the
professional-kitchen practice of having every ingredient measured and every tool positioned before
cooking begins.

The paper makes four contributions: the three-phase methodology, grounded in backward design and in
the externalization of tacit knowledge; a case study of applying it at a competitive hackathon; the
concept of [[DefinedTerm/context-fluency]]; and a research agenda of five open questions. It is
explicit that the ingredients of the methodology are individually well established and that its
contribution is their integration into one phase-gated sequence completed before implementation.

## Key Points

- The methodology has three sequential phases whose artifacts feed the next: contextual grounding,
  which externalizes domain expertise and tacit knowledge into briefing documents agents consult;
  collaborative specification, in which human-agent dialogue produces a design document that records
  value judgments as constraints and captures why as well as what; and task decomposition, which turns
  the specification into dependency-aware task records so that several agents can work in parallel
  without coordination overhead, followed by integration verification against the specification.
- The paper positions the methodology against neighbouring approaches: against
  [[DefinedTerm/spec-driven-development]] it adds a phase for tacit, value-laden knowledge that
  specifications alone do not capture; against [[DefinedTerm/prompt-engineering]] it works at the
  scope of the workflow rather than the single invocation; and against iterative or vibe-coding
  workflows it front-loads alignment work that those flows pay incrementally as rework.
- In the hackathon case study, held in January 2026 with about 12 teams and a five-hour window, the
  author spent roughly two hours preparing while most teams began coding within fifteen minutes.
  Preparation produced 10 planning documents totalling 9,386 words and 64 task records with
  dependencies; four parallel subagents then worked across distinct feature areas, closing task
  records at a median of 5.9 minutes each, and the final codebase of 8,496 lines of TypeScript was
  deployed to production as a full-stack educational platform.
- The author reports that no structural refactoring was needed during deployment — the bugs that
  emerged were integration and styling issues — and that bug-type task records resolved in a median
  1.2 minutes against 9.7 minutes for implementation tasks, and reads near-zero architectural rework as
  consistent with the hypothesis that rich upfront context reduces agent misalignment, while stating
  that causation cannot be established from a single case.
- Across the twelve-team field, workflow style split roughly in half between vibe-coding pitches and
  teams that opened with explicit planning, and only the author's team fanned out parallel subagents
  from a decomposed plan; the paper does not link these patterns to outcomes.
- The research agenda asks whether deliberate preparation reduces agent misalignment compared with
  iterative development, what counts as sufficient context and when to stop preparing, how context
  fluency varies across practitioners, domains and models, whether the method scales beyond
  prototyping, and how preparation time relates to implementation quality.

## Notes

For task decomposition the author used Beads, which the paper describes as lightweight Git-backed
JSON records carrying priorities, dependencies and acceptance criteria (see [[DefinedTerm/beads]]),
while noting that the principle generalizes. It also cites the Research-Plan-Implement methodology as
the closest prior work, differing from it by formalizing tacit-knowledge externalization and by
requiring all three phases to finish before implementation begins.

The author states three limitations: the evidence is a single five-hour hackathon with one
practitioner, which is illustrative rather than generalizable; there was no control group or
iteration-first comparison and the other eleven teams were not instrumented; and the author's own
background in both education and software engineering is a confound that cannot be separated from
the method's contribution. The paper releases an artifact bundle with the anonymized hackathon data,
prompts, agent configurations and context-engineering scaffolds on Zenodo. The version extracted here
is arXiv:2605.05400v1.
