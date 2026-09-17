---
title: "AGrail"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://aclanthology.org/2025.acl-long.399.pdf'
    hash: sha256:c86e2264e53af6e3dc4e70a819d26f3e1b912598c8d14d8dadddbc75fa99ebf2
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A lifelong guardrail framework, proposed by Luo et al., that uses two collaborative LLMs and an evolving memory of safety checks to decide whether an LLM agent's action should be allowed to execute, refining its checks over time instead of relying on a manually specified trusted context."
---

AGrail is a lifelong guardrail framework, proposed by Luo et al. in [[ScholarlyArticle/agrail]], that generates and iteratively refines the set of safety checks used to decide whether an LLM agent's action should be allowed to execute. Two identical LLMs play distinct roles: an Analyzer retrieves relevant safety checks from a memory module and revises, merges, or adds to them based on the current agent action, safety criteria, and any manually specified guard request; an Executor then verifies each proposed check — invoking an external tool when needed, or relying on its own reasoning otherwise — discards checks it judges redundant or incorrect, and blocks the agent's action if any check comes back unsafe. The memory of accumulated safety checks is updated after each action, so the framework's checks improve as it processes more actions of a given task — a test-time adaptation (TTA) process the paper frames as achieving lifelong self-adaptation, converging toward an ideal set of checks for each type of agent action without ever observing that ideal set directly.

## When It Applies

AGrail is intended for online deployment alongside an existing LLM agent, checking each action before it executes rather than analyzing agent output after the fact. It supports both a default set of universal safety criteria (three categories: information confidentiality, integrity, and availability) applicable across agent types, and manually authored, task-specific safety criteria for narrower domains; it can also invoke auxiliary detection tools (e.g., an OS environment checker, a permission checker, an HTML-choice checker) when reasoning alone is judged insufficient. The introducing paper evaluates it against task-specific risks (Mind2Web-SC, a web-agent access-control benchmark; EICU-AC, an electronic-health-record access-control benchmark) and systemic risks (prompt injection, system sabotage, and environment attacks on OS agents via the paper's own [[Dataset/safe-os]] benchmark; prompt injection on web agents via AdvWeb and EIA), reporting that it depends on the underlying foundation model's reasoning strength — a stronger model (Claude-3.5-Sonnet) is more robust to the order in which safety checks are learned than a weaker one (GPT-4o-mini). The authors state two limitations: the framework relies on off-the-shelf LLMs for its own reasoning rather than a purpose-trained guardrail model, and its auxiliary detection tools are limited by the current scarcity of tooling for LLM-agent security.

## Related Terms

[[ScholarlyArticle/agrail]], [[Dataset/safe-os]], [[DefinedTerm/guardrails]]
