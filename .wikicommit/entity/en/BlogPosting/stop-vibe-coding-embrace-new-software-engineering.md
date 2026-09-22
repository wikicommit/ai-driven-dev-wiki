---
title: "停止“氛围编程”（Vibe Coding），拥抱新一代软件工程"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, agentic-engineering, code-review]
sources:
  - type: url
    url: 'https://tonybai.com/2026/02/28/agentic-software-engineering/'
    hash: sha256:71f1a7a4e0110bdb853371fac1dec6fd860c60643931805915db71acb1c96375
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The opening instalment of a Chinese-language micro-column on software engineering in the age of AI agents. It argues that vibe coding buys speed while accumulating trust debt, that the bottleneck has moved from writing code to human attention and review bandwidth, and that the answer is not faster generation but an engineering system around the agent — putting non-deterministic output inside a deterministic cage."
  author: "Tony Bai"
  datePublished: "2026-02-28"
---

The piece opens on an analogy it then refuses to let go of: an extremely capable junior programmer who writes a thousand compiling, passing lines while you fetch a coffee, but who has no architectural instinct, refactors core logic before understanding the intent behind it, and forgets tomorrow the conventions you corrected today. Nobody, the author argues, would let such a hire push straight to production unsupervised — they would get strict review, explicit boundaries and a demand for evidence at each step — and the author's claim is that the industry is nevertheless making exactly that mistake with coding agents.

From that the author draws the distinction the post is built on. For a throwaway script or a prototype, [[DefinedTerm/vibe-coding]] feels like magic; for long-lived, high-reliability enterprise software it is, in the author's image, designing a sea-crossing bridge in a paint program. The speed is real and so is the liability accumulating behind it, which the author calls [[DefinedTerm/trust-debt]]. The mechanism given is a shift in where the constraint sits: when humans typed line by line, the physical limit on output also bought the brain time to absorb context, think about architectural boundaries and run a subconscious quality check. With generation no longer the bottleneck, human attention and review bandwidth are — and the conventional response of opening a pull request and eyeballing the diff collapses when an agent produces hundreds of lines spanning several microservices, altering a database schema and introducing new dependencies within seconds.

The author is explicit that the framing is not their own invention, crediting the influence of Ahmed E. Hassan's work on Software Engineering 3.0 and agentic software engineering, while arguing that a gap remains between understanding that theory and turning it into a team's daily muscle memory — and presenting the column as an attempt to close it with practice and templates rather than prompt tricks or plugin tutorials.

## Key Points

- The stated failure is not that AI reduces the work but that it relocates it: the pain of writing code becomes the pain of reading it and cleaning up afterwards, and treating an agent as a faster typewriter without upgrading the engineering management system around it produces system-scale disasters at speed rather than a tenfold gain.
- The author's claim is that the bottleneck moved from code generation to human attention and review bandwidth, and that this is what breaks conventional pull-request review. What comes out is characterized as extremely optimized locally while its global logic may be fragmented.
- The claim that software engineering is over in the age of AI is rejected by analogy to civil engineering, which the author describes as never having been about hand-forging a perfect steel bar but about producing reliable bridges given materials with tolerances and workers who make mistakes — through redundant design, safety margins and inspection standards.
- The author's stated definition of the new discipline follows from that analogy: how to deliver software that can be absolutely trusted, continuously and stably, from a mixed team of humans and stochastic, unreliable AI teammates, by means of systematic engineering constraints, restated more plainly as putting non-deterministic magic inside a deterministic engineering cage.
- The column's stated agenda names several mechanisms it will develop: exploiting the agent's tirelessness for boundary testing and refactoring, replacing loose prompts with an intent contract that draws the agent's safe autonomous boundary, upgrading diff-based review into evidence-chain audit via a [[DefinedTerm/merge-readiness-pack]], designing automated coordination pipelines for the shift from one person and one agent to ten people and a hundred concurrent agents, and an argument that deliberately boring, restrictive strongly-typed languages such as Go and Rust become the firmer foundation for enterprise systems in this setting. These are stated as the column's forthcoming subjects, not as conclusions the post establishes.
- The post is a column opener and carries the accompanying sales framing, including a fourteen-lecture outline across four modules and a conditional fifth. Its arguments are the author's own position, drawn from their reading and their own development pipeline, and the post reports no measurement of any of them.

## Context

The post reaches the same diagnosis that [[DefinedTerm/review-bottleneck]] names from other sources — that review capacity, not generation capacity, is what limits agent-assisted delivery — and links it explicitly to a debt metaphor. Its framing that software engineering is entering a golden age of engineering rather than ending puts it against the stronger claims made for [[DefinedTerm/vibe-coding]], while its grounding in Hassan's SE 3.0 work places it alongside this wiki's other material on [[DefinedTerm/agentic-engineering]].

The author's own position on where this leaves practitioners is stated as a choice of role rather than of tooling: a passenger screaming inside a self-driving car that has lost control, or the commander of an AI racing fleet. The post is explicit that the column will not cover prompt techniques that go stale within months, nor the installation of any particular tool.
