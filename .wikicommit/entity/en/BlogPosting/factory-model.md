---
title: "The Factory Model: How Coding Agents Changed Software Engineering"
type: "schema:BlogPosting"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/factory-model/'
    hash: sha256:5c88d875dc4b49c7cdcb8bc777758f860985d09734d623a7d4b1817af75e9a35
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Addy Osmani's argument that autonomous coding agents have produced a step change comparable to earlier rises in software's level of abstraction, shifting the developer's job from writing code to building and orchestrating a fleet of agents — a 'factory' — and that with generation increasingly automated, specification clarity and disciplined testing, not typing speed, now separate strong engineering results from weak ones."
  author: "Addy Osmani"
  datePublished: "2026-02-25"
---

This post argues that a recent jump in coding-agent capability is a step change, not a gradual improvement, and places it within "the arc of raising abstraction" that has run from bits to instructions, instructions to functions, functions to objects, objects to services, and services to distributed systems. Its central claim is that "coding has changed dramatically" while "software engineering, at its core, has not": the mechanical work of producing code is being automated, but the cognitive work of specifying, architecting, and evaluating systems is being amplified rather than replaced. It frames the present moment with a factory metaphor — see [[DefinedTerm/factory-model]] — in which a developer builds and runs a fleet of agents rather than writing code directly.

The post traces this to three generations of AI coding tools: accelerated autocomplete, synchronous agents directed step by step, and autonomous agents that can run for hours or days against a specification with comparatively little supervision. It argues that with this third generation, verification rather than generation has become software development's unsolved bottleneck, and that the skills separating strong engineers from weak ones have shifted toward specification clarity, architectural judgment, and disciplined review rather than away from technical skill altogether.

## Key Points

- Frames the current shift as another step in the historical "arc of abstraction," citing Grady Booch's description of it as "software's third age" — see [[DefinedTerm/softwares-third-age]].
- Distinguishes three generations of AI coding tools: accelerated autocomplete (keystroke savings within an unchanged write-run-debug loop), synchronous agents (natural-language tasking with the developer present for every step), and autonomous agents (a specification handed off and run for up to hours or days, returning logs, previews, and pull requests for review).
- States the factory mental model and extends the analogy: a factory has quality control, has process documentation, has inputs that must be precisely specified or the output comes out wrong, and stalls when its environment is unreliable — and reports that inside teams that have adopted the model aggressively, a substantial portion of merged pull requests now originate from agents running autonomously in cloud environments.
- Draws an onboarding parallel: agents that get stuck search commit history, run `git blame`, and escalate to a human via Slack, the way a new engineer would — and argues that a codebase whose documentation and history would not let a new engineer understand why it is structured a certain way will also make an agent struggle.
- Argues "your spec is the leverage": at the scale of running dozens of agents in parallel, spec quality determines the difference between mediocre and exceptional output, because ambiguous requirements and poor architectural decisions propagate across the whole fleet rather than affecting one implementation.
- Lists what agentic development still requires: clear, evaluable requirements; strong abstractions and clean module boundaries; reliable tests; careful tradeoffs; and [[DefinedTerm/human-in-the-loop]] review — arguing agents "make confident mistakes" whose output is good enough to get past casual review, raising rather than lowering the bar for review skill.
- Argues red/green test-driven development becomes close to mandatory in an agentic workflow, because an agent optimizing for passing tests will find ways to pass them, and a test suite written after the implementation risks confirming what the implementation happens to do rather than what it should do — see [[DefinedTerm/red-green-tdd]].
- Argues verification, not generation, is the unsolved bottleneck: UI verification remains brittle, context-window limits can make agents miss constraints outside what they are reasoning over on large codebases, and flaky environments become systemic blockers once dozens of agents hit them at once — naming better automated regression detection, artifact-level validation, reliable environment provisioning, and [[DefinedTerm/guardrails]] as unmet infrastructure needs.
- Lists systems thinking, problem decomposition, architectural judgment, specification clarity, output evaluation, and orchestration skill as the capabilities that will distinguish high-leverage engineers, framing them as existing skills whose relative importance has risen rather than new skills.
- Cites reported year-over-year growth — new website creation up roughly 40%, new iOS apps up nearly 50%, and US GitHub code pushes up 35% — as evidence that the barrier to creating software has genuinely dropped, while cautioning that more quantity does not necessarily mean better quality.

## Context

The post opens by saying it expands on thoughts from Michael Truell of Cursor, and later quotes further remarks attributed to him — "the developer's job is becoming building the system that builds the software, the factory, not just the product" and "reviewing ideas is a lot more fun than reviewing code," the second linked to a video from Cursor's own account — as resonating with its argument; see [[SoftwareApplication/cursor]]. It lists further reading by the same author, including posts titled "Human judgment doesn't leave the software factory. It relocates.", "Practical Loop Engineering", and "Agentic Code Quality". It closes by pointing readers to the author's O'Reilly book [[Book/leading-effective-engineering-teams]] for a fuller treatment of hiring, delegation, communication, and leading teams that ship.
