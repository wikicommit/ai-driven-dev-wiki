---
title: "人間は意図、AIは実装：Codexが導く「要件を伝えるだけ」のAI駆動開発ワークフロー"
type: "schema:BlogPosting"
lang: en
tags: [agents, agent-config, spec-driven-development]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62010/'
    hash: sha256:212b9942c34a29825737eb0d331e5cd97a885416e16beed5147f5f78e9074c63
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A phase-by-phase walkthrough of an AI-driven development workflow for small web applications, built around Codex and demonstrated on a feature-request voting board, in which prompts state requirements rather than output paths and the agent works out placement from rule files it has been given in advance."
  author: ["李俊浩"]
  datePublished: "2026-02-06"
  publisher: "[[Organization/cyberagent]]"
---

This post is a walkthrough of an AI-driven development workflow for small web applications, given as a sequence of phases with the actual prompt for each and the output the author expects back. Its worked example is a feature-request voting board — users post feature requests, others vote on them, and a product team uses the result to set priorities — chosen so each phase can be shown on something concrete.

The author's image of the division of labour is Google Maps: the person gives the destination (the *why*), and the AI proposes the best route (the *how*) and leads them to the deliverable (the *what*). The stated relationship is that the human defines what they want to achieve and the AI presents the best options for how to proceed.

The technique the post is actually about is what it calls requirement-based prompting: rather than enumerating output paths in the prompt, state the requirement and the documents to consult, and let the agent place files by rules it was given in advance. The post's own summary names five points — requirement-based prompt design, the use of `AGENTS.md` and `project-rules.md` to pre-define auto-generation rules, UI wireframes as ASCII art plus Mermaid, `context.json` for context management, and optimizing the cycle for small-scale development by trimming phases that are not needed.

## Key Points

- The workflow runs in six phases: project vision (Phase 0), project initialization (Phase 1), requirements definition and domain modeling (Phase 2), architecture and technology-stack selection (Phase 3), development-environment setup (Phase 4), and feature implementation with `context.json` management (Phase 5).
- Several phase prompts carry an explicit constraint forbidding the AI to emit any source code: the vision, wireframe, domain-model and architecture prompts all state it. The vision prompt gives its reason as keeping the discussion at the conceptual level and holding off technology and architecture questions; the domain-model prompt gives its own as preserving freedom in the later technology choice.
- [[DefinedTerm/agents-md]] is presented as the agent's long-term memory: it holds the project overview, folder layout, documents that must be consulted, working rules and current status, and the post's stated effect is that the AI can then make consistent judgments.
- The four working rules the post puts in `AGENTS.md` are: plan before acting and execute after approval; present three options when planning or proposing; check and update the relevant specification before implementing; and update `context.json` when a feature is completed.
- `AGENTS.md` also carries the auto-generation rules themselves — trigger phrases, the process to run, the folder and file layout to produce, and the shape of the resulting files — which is what lets a one-line human prompt ("read vision.md and generate the user stories") expand into a multi-step run.
- The generation steps are gated on human approval rather than fully automatic: the story-splitting step and the install step both present a plan and wait for an approve-or-revise answer before creating anything.
- UI wireframes are produced as ASCII art for the screens plus Mermaid diagrams for screen transitions and component structure, with the prompt specifying no output path and letting the agent place the file per its rules.
- The domain model is deliberately specified as technology-independent: the prompt names entities, value objects, aggregates and domain events as its design items, asks for class and relationship diagrams in Mermaid, and forbids assuming any particular datastore — which the post argues preserves freedom in the later technology choice.
- `context.json` is a per-story file recording the story path, related stories, the code touched by layer, new and modified files, status and timestamps. The post gives its three purposes as progress tracking, telling the AI which files to consult, and making dependencies visible.
- The post is a demonstration of a method on a sample project. It reports no measurement, no comparison against working without the method, and no account of running it on production software.

## Context

The post scopes itself explicitly to small-scale web application development, and its architecture phase is written around that: the prompt asks for the simplest structure that does not distort the domain model, with a monolith recommended and complex architectures treated as overkill at this size.

Its stated aim is to draw out the potential of large-context code models — Codex is the one it names — by treating them as a development partner rather than an autocomplete, and its claim for the prompt style is that the more the rule files are filled in, the simpler the prompts become and the better the output quality gets.
