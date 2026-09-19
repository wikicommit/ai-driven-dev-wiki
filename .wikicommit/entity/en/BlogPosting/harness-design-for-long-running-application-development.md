---
title: "Harness design for long-running application development"
type: "schema:BlogPosting"
lang: en
tags: [agent-architecture, evaluation, long-horizon-tasks, agent-tooling]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/harness-design-long-running-apps'
    hash: sha256:47a08ad7125c953a6a359d169a11e61245c1d5329e47cb7057f496aaaef42b2a
  - type: url
    url: 'https://www.anthropic.com/research/building-effective-agents'
    hash: sha256:611504eb30423330be060ed8f00e432a0adcb417f992b2cfb5cbf9ccd8d511bf
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An Anthropic Labs engineer's account of building a GAN-inspired generator–evaluator harness, first for frontend design and then for long-running autonomous full-stack development, and of progressively simplifying it as models improved. Reports duration and cost figures for two multi-hour builds."
  author: ["Prithvi Rajasekaran"]
  datePublished: "2026-03-24"
  publisher: "[[Organization/anthropic]]"
---

This post reports work on two problems the author treats as interconnected: getting Claude to produce
high-quality frontend designs, and getting it to build complete applications without human
intervention. Earlier efforts on a frontend design skill and a long-running coding agent harness had
improved performance above baseline through prompt engineering and harness design, but the author
reports both hit ceilings — which is given as the reason for seeking an approach that would hold
across two domains as different as subjective taste and verifiable correctness.

The approach taken is borrowed from Generative Adversarial Networks: a multi-agent structure pairing
a **generator** with an **evaluator**. The post's central claim about why this helps is about
self-evaluation rather than about generation — agents asked to judge their own work tend to praise it
confidently even when quality is visibly mediocre, and the author argues that tuning a standalone
evaluator to be skeptical is far more tractable than making a generator critical of its own output.
Separation does not by itself remove the leniency, since the evaluator is still an LLM inclined to be
generous toward LLM output, but it gives the generator something concrete to iterate against.

Applied to long-running coding, this became a three-agent planner–generator–evaluator architecture
producing full-stack applications over multi-hour autonomous sessions. The later half of the post is
an account of taking that architecture apart again as models improved, and the closing position is
that the space of interesting harness combinations does not shrink as models get better — it moves.

## Key Points

- Two failure modes are identified in agents on long tasks: loss of coherence as the context window
  fills, and [[DefinedTerm/context-anxiety]], where a model wraps up work prematurely as it nears what
  it believes is its context limit. [[DefinedTerm/context-reset]] is presented as addressing both.
- A reset is distinguished from [[DefinedTerm/compaction]] on the grounds that compaction summarises
  history in place and so preserves continuity without giving the agent a clean slate, which means
  context anxiety can persist through it; the cost of a reset is that the handoff artifact must carry
  enough state, plus added orchestration complexity, token overhead and latency.
- For frontend design the author wrote four grading criteria given to both generator and evaluator:
  design quality (whether the design reads as a coherent whole), originality (evidence of custom
  decisions rather than template layouts and library defaults), craft (typography hierarchy, spacing,
  colour harmony, contrast ratios) and functionality (usability independent of aesthetics).
- Design quality and originality were weighted above craft and functionality, on the stated grounds
  that Claude already scored well on the latter two by default while producing bland output on the
  former two; the criteria explicitly penalised generic patterns, naming purple gradients over white
  cards as a telltale sign of AI generation.
- The evaluator was calibrated with few-shot examples carrying detailed score breakdowns, which the
  author reports aligned its judgment with his preferences and reduced score drift across iterations.
- The frontend loop was built on the [[SoftwareApplication/claude-agent-sdk]], with the evaluator given
  the Playwright MCP so it could navigate and screenshot the live page before scoring rather than
  grading a static image; runs of 5 to 15 iterations stretched up to four hours of wall-clock time.
- The wording of the criteria shaped output in ways the author reports not fully anticipating —
  including the phrase "the best designs are museum quality", which pushed designs toward a particular
  visual convergence.
- Score improvement across iterations is reported as real but not cleanly linear: the author regularly
  preferred a middle iteration to the last, and notes that even the first iteration beat an unprompted
  baseline, suggesting the criteria steered the model before any evaluator feedback arrived.
- One reported run illustrates a discontinuous change: asked for a Dutch art museum site, the model
  produced a polished dark-themed landing page by the ninth iteration, then on the tenth scrapped it
  entirely for a 3D room with a CSS-perspective checkered floor, artwork hung in free-form positions
  and doorway-based navigation instead of scrolling or clicking.
- In the full-stack harness the planner expanded a 1–4 sentence prompt into a full product spec; it was
  instructed to be ambitious about scope and to stay at the level of product context and high-level
  technical design, on the stated reasoning that granular technical details specified upfront would
  cascade errors into implementation.
- The generator worked in sprints, one feature at a time, on a React, Vite, FastAPI and SQLite (later
  PostgreSQL) stack with git for version control; before each sprint the generator and evaluator
  negotiated a sprint contract agreeing what "done" meant and how it would be verified, with the two
  communicating by writing and reading files.
- On a retro game maker prompt, a solo run took 20 minutes and $9 while the full harness took 6 hours
  and $200 — over 20x the cost. The solo run's application had broken wiring between entity
  definitions and the game runtime, so the game did not respond to input; the harness run's spec ran to
  16 features across ten sprints and produced a playable result.
- The author reports Claude is a poor QA agent out of the box, watching it identify legitimate issues
  and then talk itself into approving the work anyway, and testing superficially rather than probing
  edge cases; the fix described is reading evaluator logs, finding where its judgment diverged from the
  author's, and updating the QA prompt over several rounds.
- A general principle is drawn for harness design: every component encodes an assumption about what the
  model cannot do on its own, and those assumptions are worth stress testing because they may be wrong
  and because they go stale as models improve. The post quotes Anthropic's own Building Effective
  Agents post for the underlying idea — "find the simplest solution possible, and only increase
  complexity when needed".
- Context resets were not part of this harness to begin with: Opus 4.5 had largely removed context
  anxiety on its own, so the agents were run as one continuous session with the Agent SDK's automatic
  compaction handling context growth.
- The later simplification pass proceeded by removing one component at a time and reviewing the impact of
  each, after a first attempt at cutting the harness back radically failed to replicate the original's
  performance and left it hard to tell which pieces were load-bearing. The sprint construct was removed
  after Opus 4.6 landed, and the evaluator moved to a single pass at the end of the run rather than
  grading per sprint.
- The evaluator's value is reported as conditional rather than fixed: as raw model capability rose, tasks
  that previously needed its check came within what the generator handled alone, so the post's stated
  rule is that an evaluator is worth its cost when the task sits beyond what the current model does
  reliably solo.
- The updated harness built a browser DAW in about 3 hours 50 minutes for $124.70, with the builder
  running coherently for over two hours without sprint decomposition; the reported breakdown gives the
  planner 4.7 minutes and $0.46, three build rounds of 2h07, 1h02 and 10.9 minutes, and three QA rounds
  of 8.8, 6.8 and 9.6 minutes.
- QA still found real gaps in that run, quoted in the post: first-round feedback that core DAW features
  were display-only without interactive depth, and second-round feedback that audio recording remained
  stub-only and clip resize and split were not implemented.

## Context

This is a firsthand engineering account from one member of Anthropic's Labs team, describing his own
experiments rather than a controlled study. There is no baseline beyond the single solo-versus-harness
comparison on one prompt, no repetition, and the quality judgments driving the frontend work are
explicitly the author's own taste — a point the post makes itself in noting that the evaluator was
calibrated to align with his preferences.

The post is candid about limits in its own results. The harness-built game maker retained workflow
problems the author reads as a gap in the base model's product intuition rather than something the
harness addressed; the generated game's physics had rough edges, with his character jumping onto a
platform and ending up overlapping it; and an AI-generated level left him stuck behind a wall. For the DAW he notes the application is far from a professional music production
program and that Claude cannot hear, which made the QA feedback loop less effective on musical taste.
Even the tuned evaluator is described as leaving small layout issues, unintuitive interactions and bugs
in deeply nested features undiscovered.

Its relationship to the author's earlier harness work is one of revision rather than extension: several
components that earlier work established as necessary are removed here, and the stated reason is that
the model changed underneath them.
