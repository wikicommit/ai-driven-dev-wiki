---
title: "個人的AIコーディングエージェントとの向き合い方（2026）"
type: "schema:BlogPosting"
lang: en
tags: [agents, developer-experience, context-files, code-review]
sources:
  - type: url
    url: 'https://zenn.dev/x_shunei/articles/f3f67a3af18224-life-with-ai-agent'
    hash: sha256:b1d7777bab2ee81342c8b86268d242b6fa8847f10c56eb4880efc8a6489c3b02
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A software engineer's personal account, written at the start of 2026, of delegating most coding work to AI coding agents: the working habits that make it effective, which tools are used for what, and the unease and lost enjoyment that come with it."
  author: ["井上"]
  datePublished: "2026-01-31"
---

Written as a snapshot to look back on later, this post records how one software engineer works with
AI coding agents after a year, 2025, in which such tools became central to development work. The
author reports delegating around 80% of coding and technical research to agents, with hand-written
code down to roughly 20% of their time, and describes the result as both clearly faster and more
tiring.

The first half is practical — the habits the author relies on and how tools are divided between
tasks — and the second half is reflective, covering anxiety about skills, the loss of the enjoyment
of writing code, and why studying and judgment still matter.

## Key Points

- Productivity rose but so did fatigue from context switching. The author reports trying to run two or
  three agent tasks in parallel while also reviewing code and answering messages, and finding that three
  agents did not triple output because review and merging left the human as the bottleneck — a firsthand
  instance of the [[DefinedTerm/review-bottleneck]].
- Plan mode is described as the author's most important habit: checking how the agent intends to proceed
  before it starts reduces rework, and the author observes that large course corrections after changes
  have already been made tend to go badly because the agent is pulled along by its earlier edits.
- Generated code that is within an acceptable range of quality is not polished further, on the author's
  reasoning that future model updates can refactor it; the author nonetheless keeps every line in a state
  they could explain, as with their own code.
- When output is poor, the author treats the cause as insufficient context or insufficiently detailed
  instructions, iterates on the plan, and reports that voice input helps once prompts grow long.
- Project instruction files — [[DefinedTerm/claude-md]] and [[DefinedTerm/agents-md]] — are called
  essential: without them, the author reports, an agent will typically not infer project choices such as
  the package manager in use (falling back to pip in a project that uses uv).
- The author's division of tools as of early 2026: [[SoftwareApplication/claude-code]] for coding,
  chosen for its detailed planning but limited by rate limits on the Pro plan; ChatGPT and
  [[SoftwareApplication/openai-codex]] for research, with Codex judged strong as a model but less
  polished as a tool; and JetBrains AI as a fallback that can run Claude Code inside the IDE.
- On keeping up with the field, the author advises not chasing every new technique, since workaround
  prompting tricks are often made unnecessary by the next model update.
- The author reframes the fear of losing technical skill as learning a new skill — giving context,
  setting direction and reviewing output — likened to management, while noting that this skill is hard
  to make visible.
- Studying remains necessary in the author's view because AI output cannot be merged unreviewed, and
  spotting problematic code from security, UX and non-functional perspectives requires knowledge; the
  author argues that review ability has become more important, not less.
- Because agents tend to implement things that were not asked for, the author argues that deciding what
  not to build contributes most to productivity, and that its value has risen as implementation has
  become cheaper.

## Context

The post is explicitly personal and provisional: the author says they do not know whether their
approach is the best one, that tools are changing too fast to name a best choice, and that the
question of how to recover the enjoyment of building is still open for them. Its observations about
productivity are self-reported impressions rather than measurements.
