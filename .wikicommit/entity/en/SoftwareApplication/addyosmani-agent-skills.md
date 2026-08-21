---
title: "addyosmani/agent-skills"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-skills, engineering-practice, agentic-coding, open-source]
sources:
  - type: url
    url: 'https://github.com/addyosmani/agent-skills'
    hash: sha256:1438a09672625c5be59b8c9d50d37e217646a38b19d7e89d26dbfea6ffa0896a
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An open-source pack of 24 Agent Skills encoding senior-engineering workflows, quality gates and verification requirements across the development lifecycle, with slash commands, specialist personas and setup paths for a dozen agent harnesses."
  applicationCategory: "DeveloperApplication"
  author: "[[Person/addy-osmani]]"
  operatingSystem: ""
  softwareVersion: ""
  license: "MIT"
---

`addyosmani/agent-skills` is an open-source repository of [[DefinedTerm/agent-skills]] describing itself as "production-grade engineering skills for AI coding agents." Its stated purpose is to encode the workflows, quality gates and best practices senior engineers use, packaged so that agents follow them consistently at every phase of development. Its diagnosis of the problem is direct: AI coding agents default to the shortest path, which often means skipping specs, tests, security reviews and the practices that make software reliable.

## Overview

The pack is organised around a six-stage lifecycle — Define, Plan, Build, Verify, Review, Ship — with eight slash commands mapping onto it: `/spec` ("spec before code"), `/plan` ("small, atomic tasks"), `/build` ("one slice at a time"), `/test` ("tests are proof"), `/review` ("improve code health"), `/webperf` ("measure before you optimize"), `/code-simplify` ("clarity over cleverness"), and `/ship` ("faster is safer"). Skills also activate automatically from what the agent is doing — designing an API triggers the API-design skill, building UI triggers the frontend skill.

A `/build auto` mode removes the human step *between* tasks rather than the verification: the plan is approved once, then generated and implemented in a single pass, with every task still test-driven and committed individually and the run pausing on failures or risky steps.

## Features

The repository contains 24 skills — 23 lifecycle skills plus one meta-skill on using the pack — alongside four specialist agent personas (a code reviewer at Senior Staff Engineer level, a test engineer, a security auditor, and a web-performance auditor), seven supplementary reference checklists, session lifecycle hooks, and per-tool setup documentation.

Four design choices are stated for the skills themselves. **Process, not prose**: skills are workflows with steps, checkpoints and exit criteria, not reference docs. **Anti-rationalization**: every skill carries a table of the excuses agents use to skip steps — the example given is "I'll add tests later" — with documented counter-arguments. **Verification is non-negotiable**: every skill ends with evidence requirements such as passing tests, build output or runtime data, and "'seems right' is never sufficient." **[[DefinedTerm/progressive-disclosure]]**: the `SKILL.md` is the entry point and supporting references load only when needed, keeping token usage minimal.

Installation is deliberately harness-agnostic. The repository documents `npx skills add addyosmani/agent-skills` via the open skills CLI, which it says installs into 70-plus agents, alongside native paths for [[SoftwareApplication/claude-code]] plugin marketplace install, [[SoftwareApplication/cursor]], Antigravity CLI, [[SoftwareApplication/gemini-cli]], Windsurf, OpenCode, [[SoftwareApplication/github-copilot]], [[SoftwareApplication/kiro]], [[SoftwareApplication/codex]] and Command Code. One documented portability gap is that a per-skill `npx` install copies only that skill's directory and not the repository-level `references/` directory, so shared checklists are unavailable unless the whole repo is integrated.

## History

The repository's own framing places its content lineage in Google's engineering culture: it states that skills bake in concepts from *Software Engineering at Google* and Google's engineering practices guide, naming Hyrum's Law in API design, the Beyoncé Rule and test pyramid in testing, change sizing and review speed norms in code review, Chesterton's Fence in simplification, trunk-based development in git workflow, and Shift Left with feature flags in CI/CD. At the time of this snapshot the repository shows 88.8k stars, 9.5k forks and 437 commits, and is MIT-licensed. It links a comparison document positioning itself against two other skill packs.
