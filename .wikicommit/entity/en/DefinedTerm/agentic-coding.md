---
title: "Agentic Coding"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2505.19443'
    hash: sha256:6570a1ae86ae608d97b50f389a3ae52d197c066e9bb8412ba0eaea93265f7f52
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Software development in which autonomous or semi-autonomous AI agents plan, execute, test, and iterate on multi-step coding tasks from a high-level goal, with the developer acting as a supervisor and reviewer rather than a direct implementer."
---

Agentic coding is a mode of AI-assisted software development in which autonomous or semi-autonomous software agents are delegated substantial cognitive and operational responsibility: interpreting a high-level goal, planning and decomposing it into sub-tasks, using tools and resources (compilers, test runners, version control, APIs) to execute them, and iterating based on feedback, with minimal continuous human intervention. The developer's role shifts from low-level implementer to system-level supervisor and goal-setter: specifying objectives and constraints, monitoring execution traces and outputs, and validating results before integration.

## Usage

Reviewed against vibe coding, agentic coding is characterized by moderate-to-high AI autonomy, hierarchical planner–executor architectures (often with specialized sub-agents such as a coder, tester, reviewer, and fixer coordinated by a planner), sandboxed or containerized execution environments, persistent memory across multi-step tasks, and an integrated validation pipeline that automatically synthesizes and runs tests rather than relying on a human to invoke them. Named examples of agentic coding platforms include Codex, which can run `git diff`, apply patches, and generate pull requests automatically; Google's Jules, which clones and analyzes a repository, modifies code, and commits changes to a new branch for review; and Claude Code, built with explainability and oversight features that let a developer audit changes, trace reasoning, and roll back unsafe actions.

## When It Applies

It suits feature-level or system-level tasks where correctness, traceability, and automation matter more than exploratory speed: end-to-end feature implementation, complex multi-file refactoring, system migrations, and CI/CD pipeline automation. It assumes an execution environment that can safely grant an agent write access and tool use (a sandbox or container with resource and namespace isolation), and it introduces risks distinct from vibe coding: reduced human oversight can lead to skill atrophy in developers who stop engaging with implementation details, and autonomous changes across multiple modules can propagate errors silently if the agent lacks rollback mechanisms or observability hooks. It is presented as complementary to, rather than a replacement for, vibe coding — suited to the implementation and operational phases of a project that vibe coding's exploratory prototyping feeds into.

## Related Terms

[[DefinedTerm/vibe-coding]], [[DefinedTerm/ai-coding-agent]], [[DefinedTerm/harness-engineering]]
