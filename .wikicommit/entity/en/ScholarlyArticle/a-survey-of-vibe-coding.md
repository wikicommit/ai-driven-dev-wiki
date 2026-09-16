---
title: "A Survey of Vibe Coding with Large Language Models"
type: "schema:ScholarlyArticle"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2510.12399'
    hash: sha256:e7a4dc7327555d0478beeb5067576e505fb504e405921ca26c1b0f2a12f26118
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A survey formalizing vibe coding as a constrained Markov Decision Process over a human-project-agent triad, synthesizing the field into a taxonomy of five composable development models, and surveying the coding-LLM, agent, environment, and feedback-mechanism ecosystem underneath it."
  author: ["Yuyao Ge", "Lingrui Mei", "Zenghao Duan", "Tianhao Li", "Yujia Zheng", "Yiwei Wang", "Lexin Wang", "Jiayu Yao", "Tianyu Liu", "Yujun Cai", "Baolong Bi", "Fangda Guo", "Jiafeng Guo", "Shenghua Liu", "Xueqi Cheng"]
  datePublished: "2025-12-23"
  keywords: ["Vibe Coding", "Coding Agent", "Large Language Models"]
---

This paper presents what it describes as the first comprehensive, systematic survey of vibe coding, drawing on over 1,000 research papers to formalize the practice as a discipline and survey its supporting ecosystem (large language models for code, coding agents, development environments, and feedback mechanisms). Its central theoretical contribution is a formal definition of vibe coding as a dynamic triadic relationship among a human developer, a software project, and a coding agent, modeled as a Constrained Markov Decision Process in which the human defines goals and constraints, the project supplies the state space, and the agent executes policies and state transitions within it.

Building on that formalization, the paper's second major contribution is a taxonomy of [[DefinedTerm/vibe-coding-development-models]] — five distinct, composable patterns for how humans and agents divide responsibility in practice, classified along three axes: how much a human reviews AI-generated code, how much the workflow relies on structured constraints (planning documents, tests, rules), and how much context management (codebase indexing, retrieval) it uses.

## Key Points

- The paper's formal definition explicitly ties vibe coding to validating an implementation "through outcome observation rather than line-by-line code comprehension," and separately notes that of its own five development models, the Unconstrained Automation Model (UAM) is "the development approach most closely aligned with the original definition of Vibe Coding" — implying the survey's own broader umbrella term extends beyond that original, narrower meaning.
- The five-model taxonomy: Unconstrained Automation (AI dominates, humans supply requirements only, likened to Rapid Application Development), Iterative Conversational Collaboration (humans review each output, likened to pair programming), Planning-Driven (humans design upfront via specification/rule/plan documents before AI implements, likened to waterfall), Test-Driven (humans write tests as the specification and AI implements to pass them, following red-green-refactor), and Context-Enhanced (not a standalone workflow but a horizontal capability — retrieval-augmented generation, codebase indexing, rule loading — that can be layered onto any of the other four).
- The paper's own comparative table rates the four base models plus the cross-cutting Context-Enhanced Model across upfront investment, human control, structured constraints, development speed, code quality, technical debt, maintainability, and security risk, showing Unconstrained Automation as fastest but rated "High" on technical debt and security risk, versus Test-Driven's "High" technical debt rating offset by a "None" security-risk rating and a "Strict" maintainability rating.
- The paper reports (citing other empirical work) that introducing autonomous coding agents into production pipelines has been associated with a tenfold increase in security warnings and technical debt accumulation within six months of adoption.
- It names three systemic risk categories specific to increasingly autonomous coding agents: cascading errors (a flawed output from one agent propagating through interconnected pipelines or multi-agent workflows), dependency proliferation (agents introducing or hallucinating unverified/nonexistent packages, with one cited study finding nearly one-fifth of AI-suggested packages nonexistent or untrusted), and alignment failures (agents optimizing for explicit task metrics while disregarding implicit safety or maintainability constraints in a prompt).
- It surveys "scalable oversight" approaches proposed for supervising agents whose output volume exceeds what humans can directly review: hierarchical weak-to-strong supervision (citing OpenAI's own superalignment experiments fine-tuning GPT-4 under GPT-2-level guidance), multi-agent debate/critique (citing DebateCoder, where two LLMs alternately generate code and adversarial tests against each other), and continuous automated monitoring via model-aware static/dynamic analysis and reinforcement-learning-based "watchdog" agents.
- It argues successful vibe coding depends on context engineering, well-established development environments, and the chosen human-agent collaboration model at least as much as on raw coding-agent capability, and reports that the current ecosystem lacks mature tooling specifically built for dynamic context management in coding workflows, making it a largely manual, ad-hoc practice today.

## Notes

The paper is a survey/synthesis rather than an empirical study of its own; its taxonomy of five development models and its formal CMDP definition are the authors' own conceptual contributions, while the specific empirical claims it reports about production risk (e.g. the tenfold increase in security warnings, the one-fifth-nonexistent-packages figure) are drawn from other cited studies rather than measured directly by this paper. The paper acknowledges that empirical research on vibe coding's real-world process impacts remains nascent and lacks longitudinal validation.
