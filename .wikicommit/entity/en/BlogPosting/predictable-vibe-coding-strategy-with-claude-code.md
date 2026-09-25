---
title: "Claude Code를 활용한 예측 가능한 바이브 코딩 전략"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, context-engineering, prompting]
sources:
  - type: url
    url: 'https://helloworld.kurly.com/blog/vibe-coding-with-claude-code/'
    hash: sha256:ebce348758ea4336c22fe2c0c79c3120371a0d7c62e9c800a099fbcd0248ecb2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Kurly tech blog guide arguing that the failures of agent-led coding come from structural limits of LLMs — lost information in long contexts, training-data bias, ambiguous specs, compounding errors and weak working memory — and mapping each to a Claude Code feature that compensates for it at the system level."
  author: ["박재영"]
  datePublished: "2025-12-17"
---

This post on Kurly's tech blog is a practical guide to what its author calls predictable [[DefinedTerm/vibe-coding]] with [[SoftwareApplication/claude-code]]. It starts from Karpathy's original, deliberately extreme definition of vibe coding — accepting every change without reading the diff — and says that in practice the term is used more broadly; the guide covers a mode in which the developer does read the code while the LLM leads generation, the developer conveying intent in natural language, the agent generating code, editing files and running commands, and the developer checking results and adjusting direction. It presents this as a stepping stone toward being able to trust an agent enough to stop reading its code.

The post's through-line is that agent failures are not random: it attributes them to cognitive limits of LLMs that it compares to limits of human cognition, and argues that since these limits have not been solved inside the model, they have to be compensated for from outside, at the system level — which is how it reads Claude Code's tools. It was written against Claude Code 2.0.67 and Claude Opus 4.5, and notes that features and UI may since have changed.

## Key Points

- Handing an agent a whole specification at once disappoints: items in the spec go missing, unrequested features appear, and the direction drifts. The post traces this to five causes.
- Long inputs lose their middle — the post's name for this is [[DefinedTerm/lost-in-the-middle]] — which it likens to the serial position effect in human memory.
- Agents regress toward patterns that were common in training data: in its illustration, a rule to use Zustand rather than Redux holds for the first few turns and then gives way to Redux as the conversation lengthens, because explicit context competes with a learned prior.
- Specifications are inherently ambiguous, through contradictory requirements and high-entropy phrases such as "a security-conscious authentication system" that admit several readings.
- Because generation is autoregressive, an early misreading — deciding "security-conscious" means two-factor authentication — compounds through session handling, error handling, UI and tests, and costs more to fix the later it is found.
- Even short instructions lose items when there are many distinct rules to track, which the post attributes to LLMs lacking a separate working memory; chain of thought, reasoning tokens and agent loops are read as ways of supplying an external scratchpad rather than internal working memory.
- Its remedies map each limit to a Claude Code feature: small multi-turn requests, plan mode to catch a misreading before it reaches code, a to-do list to track items, subagents to split context, extended thinking for debugging and architecture decisions (and not for boilerplate), CLAUDE.md files — a short onboarding file at the root and directory-level files for local conventions — agent skills that run checks rather than list rules, and compaction with important decisions saved to a file first.
- On prompts, it asks that anyone reading a request should picture the same thing: one requirement per turn, concrete numbers, boundary conditions stated, and positive instructions ("use Zustand") preferred to prohibitions ("don't use Redux").
- Its one-line summary is to split work small, check often, and turn repetition into skills.

## Context

The guide is the author's own practice and reasoning rather than a measured study; its comparisons between LLM behaviour and human cognition cite research on human working memory and a benchmark on LLMs but are offered as analogies, and it says explicitly that LLM mechanisms differ from human working memory. See also [[DefinedTerm/claude-md]], [[DefinedTerm/agent-skills]], [[DefinedTerm/compaction]] and [[DefinedTerm/sub-agent-architecture]].
