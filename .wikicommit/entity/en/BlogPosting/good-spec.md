---
title: "How to write a good spec for AI agents"
type: "schema:BlogPosting"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/good-spec/'
    hash: sha256:fbb1e0c078b1d920689cbc3c652ad4bf253d5b39c77f957cab7ee4e6cd1ff5fa
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A guide distilling five principles for writing specifications that keep AI coding agents focused and productive: starting high-level, structuring the spec like a PRD, breaking work into modular prompts, building in self-checks and constraints, and iterating continuously."
  author: "Addy Osmani"
  datePublished: "2026-01-13"
---

This guide sets out five principles for writing specifications for AI coding agents, aimed at developers who find that a spec detailed enough to avoid ambiguity also becomes too large for a model to handle reliably. It draws on the author's own use of coding agents and on a GitHub analysis of over 2,500 agent configuration files to argue that spec quality, not spec length, is what keeps an agent focused.

The five principles are: start with a high-level vision and let the AI draft the details; structure the spec like a professional PRD covering six core areas; break tasks into modular prompts rather than one large prompt; build in self-checks, three-tier boundaries, and human expertise; and treat the spec as a living document to be tested, iterated, and evolved.

## Key Points

- GitHub's analysis of over 2,500 agent configuration files found the most effective specs cover six areas: commands, testing, project structure, code style, git workflow, and boundaries — with "never commit secrets" the single most common helpful constraint found.
- It recommends a three-tier boundary system over a flat list of rules: "Always do" (act without asking), "Ask first" (needs human approval), and "Never do" (hard stops) — reported by the GitHub study as more effective than an undifferentiated list of don'ts.
- It cites the "curse of instructions" finding that model adherence to individual directives drops as more instructions are piled into one prompt, and recommends decomposing requirements into sequential, focused instructions instead.
- It presents GitHub's Spec Kit as a four-phase gated workflow — Specify, Plan, Tasks, Implement — where a spec becomes an executable artifact that drives task breakdown and implementation rather than being written once and set aside.
- It recommends using an "extended table of contents" — an agent-generated hierarchical summary of a large spec's sections — so the agent can keep a compact index in context and pull in only the relevant section on demand.
- It recommends [[DefinedTerm/llm-as-a-judge]] for subjective quality criteria (style, readability, architectural adherence) that are hard to test automatically, using a second agent or prompt to review the first agent's output against the spec's guidelines.
- Citing Simon Willison, it names the "lethal trifecta" of properties that make AI agents dangerous — speed, non-determinism, and cost — and argues a spec and review process must account for all three rather than letting speed outpace verification.
- It distinguishes "vibe coding" from "AI-assisted engineering," describing the former as suited to exploration and throwaway projects and the latter as requiring the discipline (specs, tests, review) the post describes, and warns against conflating the two when shipping to production.

## Context

The post cites GitHub's own published analysis of agent configuration files and GitHub's Spec Kit documentation as its main evidentiary sources for spec structure, and draws repeatedly on Simon Willison's separately published writing (on vibe engineering, the lethal trifecta, and reviewing AI-generated code) for its cautions about human review and risk. It frames itself as a practical synthesis of these sources rather than as original research of its own.
