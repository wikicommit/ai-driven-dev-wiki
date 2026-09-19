---
title: "Agentic Coding"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2505.19443'
    hash: sha256:6570a1ae86ae608d97b50f389a3ae52d197c066e9bb8412ba0eaea93265f7f52
  - type: url
    url: 'https://www.anthropic.com/research/claude-code-expertise'
    hash: sha256:0a6863b8e2c10a2517ea14c69053f2df45ca56ecf794fbbe95c1dc977fbf3879
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Software development in which autonomous or semi-autonomous AI agents plan, execute, test, and iterate on multi-step coding tasks from a high-level goal, with the developer acting as a supervisor and reviewer rather than a direct implementer."
---

Agentic coding is a mode of AI-assisted software development in which autonomous or semi-autonomous software agents are delegated substantial cognitive and operational responsibility: interpreting a high-level goal, planning and decomposing it into sub-tasks, using tools and resources (compilers, test runners, version control, APIs) to execute them, and iterating based on feedback, with minimal continuous human intervention. The developer's role shifts from low-level implementer to system-level supervisor and goal-setter: specifying objectives and constraints, monitoring execution traces and outputs, and validating results before integration.

## Usage

Reviewed against vibe coding, agentic coding is characterized by moderate-to-high AI autonomy, hierarchical planner–executor architectures (often with specialized sub-agents such as a coder, tester, reviewer, and fixer coordinated by a planner), sandboxed or containerized execution environments, persistent memory across multi-step tasks, and an integrated validation pipeline that automatically synthesizes and runs tests rather than relying on a human to invoke them. Named examples of agentic coding platforms include Codex, which can run `git diff`, apply patches, and generate pull requests automatically; Google's Jules, which clones and analyzes a repository, modifies code, and commits changes to a new branch for review; and Claude Code, built with explainability and oversight features that let a developer audit changes, trace reasoning, and roll back unsafe actions.

## What It Looks Like in Practice

The account above is taxonomic — it describes what agentic coding is designed to be. A large-scale
observational study,
[[ScholarlyArticle/agentic-coding-and-persistent-returns-to-expertise]], reports what roughly 400,000
[[SoftwareApplication/claude-code]] sessions between October 2025 and April 2026 actually consisted of,
and several of its findings qualify the picture.

The supervisor role is real but narrower than "monitoring execution". Measuring who makes which
decisions, that study finds people making about 70% of planning decisions — what to do, which approach,
what counts as done — and the agent about 80% of execution decisions: which files to change, what code
to write, which commands to run. The split is between *what* and *how*, not between doing and watching.

The work is also less exclusively code than the definition suggests. Sessions divide across nine work
modes, of which roughly 56% write, fix, test or orchestrate code; 17% operate software (deploying,
configuring, running pipelines, monitoring); 14% plan or work out how an existing system behaves; and
13% produce data analysis or prose documents. Over the seven months observed, the share of sessions
spent debugging fell by nearly half while usage shifted toward more end-to-end agentic work.

The scale of delegation per instruction is measurable: a typical session runs about four turns, and each
user prompt sets off around 10 agent actions on average, occasionally over 100, with about 2,400 words
of agent output per turn.

What that study adds to the risk picture is a finding about who benefits. Session success rises with the
user's task-specific expertise — verified success 15% for novice-rated sessions against 28–33% for
intermediate and above, as adjusted rates comparing sessions matched on work mode, task-value band,
month, subject and occupation group, and excluding sessions judged to have no clear goal — while
occupation separates outcomes much less, with every one of the ten largest
occupations landing within seven points of software engineers on code-producing sessions. The authors'
reading is that a coding background is becoming less relevant to successful programming while command of
a domain is not. Note that these are transcript-based measures from one vendor's own product, and that
the study observes no real-world outcomes.

## When It Applies

It suits feature-level or system-level tasks where correctness, traceability, and automation matter more than exploratory speed: end-to-end feature implementation, complex multi-file refactoring, system migrations, and CI/CD pipeline automation. It assumes an execution environment that can safely grant an agent write access and tool use (a sandbox or container with resource and namespace isolation), and it introduces risks distinct from vibe coding: reduced human oversight can lead to skill atrophy in developers who stop engaging with implementation details, and autonomous changes across multiple modules can propagate errors silently if the agent lacks rollback mechanisms or observability hooks. It is presented as complementary to, rather than a replacement for, vibe coding — suited to the implementation and operational phases of a project that vibe coding's exploratory prototyping feeds into.

## Related Terms

[[DefinedTerm/vibe-coding]], [[DefinedTerm/ai-coding-agent]], [[DefinedTerm/harness-engineering]]
