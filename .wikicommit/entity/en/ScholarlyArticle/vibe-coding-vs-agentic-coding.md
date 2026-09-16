---
title: "Vibe Coding vs. Agentic Coding: Fundamentals and Practical Implications of Agentic AI"
type: "schema:ScholarlyArticle"
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
  description: "A review paper proposing a formal taxonomy contrasting vibe coding and agentic coding across conceptual foundations, execution architecture, workflow, safety mechanisms, and tool ecosystems, arguing the two are complementary rather than competing paradigms."
  author: ["Ranjan Sapkota", "Konstantinos I. Roumeliotis", "Manoj Karkee"]
  datePublished: "2025-05-26"
  keywords: ["Agentic AI", "Vibe Coding", "Code Generation", "Autonomous Agents", "Developer Tools", "Software Engineering", "LLMs", "AI Code Assistants"]
---

This review paper proposes a formal taxonomy distinguishing vibe coding from agentic coding as two paradigms of LLM-assisted software development, covering conceptual foundations, execution architecture, workflow patterns, safety mechanisms, and tool ecosystems, illustrated through comparative workflow examples and use cases. It defines vibe coding as a human-centric model in which a developer remains an active co-creator — prompting, reviewing generated code, and iterating conversationally — and agentic coding as a model in which autonomous agents plan, execute, test, and iterate on multi-step tasks with the developer acting as a supervisor and reviewer rather than an implementer.

The paper's central argument is that the two paradigms are complementary trajectories rather than competitors: vibe coding suits early-stage prototyping, exploration, and education, while agentic coding suits enterprise-grade automation, large-scale refactoring, and CI/CD integration, and the authors expect hybrid workflows combining both to define the next generation of development practice.

## Key Points

- The paper attributes the coining of "vibe coding" to Andrej Karpathy, describing it as developers communicating desired outcomes through natural language rather than specifying logic in syntactic detail, with the developer as an "ever-present conductor" who reviews and refines each generated piece.
- Its comparative taxonomy (Table I) characterizes agentic coding as having moderate-to-high AI autonomy with the developer as architect/supervisor, versus vibe coding's low-to-moderate autonomy with the developer as director/co-pilot who actively reviews each generated piece.
- Its architectural comparison (Table II) describes agentic coding systems as using hierarchical planner–executor modules, sandboxed/containerized execution, vector memory stores, and integrated multi-agent coordination (specialized coder/tester/reviewer/fixer sub-agents), against vibe coding's session-bound, human-managed execution loop with limited or no write access to the runtime environment.
- It lists generic agentic-coding safety features — namespace isolation, resource limits, logging hooks, and rollback triggers — and separately names Claude Code, Amazon Q Developer, and Devika as tools that log every decision node and code transformation for post-hoc inspection, contrasted with vibe coding's reliance on externally-applied, post-hoc static analysis tools (e.g. SonarQube, CodeQL, ESLint security plugins) with no native runtime enforcement.
- It identifies limitations specific to agentic coding: overdependence on agents risking skill atrophy in developers, "silent error propagation" across autonomously modified modules absent rollback/observability hooks, and expanded runtime privileges creating new security vectors (prompt injection, dependency confusion, secret leakage in AI-generated commits).
- It identifies limitations specific to vibe coding: the "black-box" opacity of most LLM coding assistants' internal decision processes, poor compatibility with production systems due to missing runtime/deployment context, and accumulation of technical debt from rapid, review-light iteration.
- Its future roadmap (Section IX) names five directions for agentic AI: architecting trustworthy autonomy (embedded explainability, regulatory compliance, runtime policy sandboxes), multi-agent collaboration via specialized sub-agents coordinated by an orchestrator, long-term memory and context continuity across multi-day tasks, human-AI collaboration infrastructure (supervision dashboards, AI-literacy training), and strategic hybrid-workflow integration of both paradigms.
- It situates today's agentic coding within a four-decade history of AI agents, from 1990s rule-based/finite-state systems (e.g. SHERLOCK, Andes) through 2000s–2010s reinforcement-learning and multi-agent systems (e.g. JADE), to today's LLM-based agents (e.g. AutoGPT, Codex, Devin).

## Notes

The paper is a review/survey rather than an empirical study of its own: its comparative tables and taxonomy synthesize claims, examples, and tool behavior drawn from the cited literature and named commercial platforms (Codex, Jules, Claude Code, Devin, and others) rather than from original experiments the authors ran themselves. Numeric figures it cites for other studies (e.g. productivity gains, benchmark scores) are not this paper's own measurements.
