---
title: "AGrail: A Lifelong Agent Guardrail with Effective and Adaptive Safety Detection"
type: "schema:ScholarlyArticle"
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
  description: "An ACL 2025 paper introducing AGrail, a lifelong guardrail framework that uses two collaborative LLMs and an evolving memory of safety checks to detect task-specific and systemic risks in LLM agent actions, and Safe-OS, a benchmark of attacks against online OS agents used to evaluate it."
  author: ["Weidi Luo", "Shenghong Dai", "Xiaogeng Liu", "Suman Banerjee", "Huan Sun", "Muhao Chen", "Chaowei Xiao"]
  keywords: ["AGrail", "LLM agent guardrail", "agent safety", "Safe-OS", "prompt injection", "test-time adaptation"]
---

This paper introduces [[DefinedTerm/agrail]], a lifelong guardrail framework for LLM agents that generates and iteratively refines the safety checks used to approve or block an agent's actions, addressing two gaps the authors identify in prior guardrail work: reliance on manually specified trusted contexts that do not generalize across tasks, and no systematic method for identifying which safety policies are actually effective for a given risk. AGrail distinguishes two categories of agent risk — task-specific risks identified by an agent administrator for a given task, and systemic risks that arise from an agent's interactions with its environment regardless of task, such as a prompt injection attack or an unintended file overwrite — and targets both.

The paper also introduces [[Dataset/safe-os]], a 100-example benchmark of prompt-injection, system-sabotage, and environment attacks against an online OS agent, built because the authors judged existing safety benchmarks to rely too heavily on LLM-generated synthetic cases that do not reflect real-world attacks. Built on Claude-3.5-Sonnet, AGrail is reported to reach 96.3% average accuracy detecting task-specific risks across the Mind2Web-SC and EICU-AC benchmarks, reduce attack success rate to 3.8% for Safe-OS system-sabotage attacks, 0% for Safe-OS and AdvWeb prompt-injection attacks, and an average 17% for EIA attacks, while preserving 96% of benign actions on Safe-OS — outperforming baseline model-based defenses (customized chain-of-thought prompting on Claude-3.5-Sonnet/GPT-4o) and guardrail-based defenses (LLaMA-Guard3, GuardAgent, AgentMonitor, ToolEmu) on the combination of risk detection and benign-action preservation.

## Key Points

- AGrail's Analyzer and Executor are two instances of the same LLM: the Analyzer retrieves and revises safety checks from a shared memory based on the current agent action and safety criteria, and the Executor verifies each check (invoking an external tool or relying on reasoning) and blocks the action if any check is unsafe.
- The paper defines two risk categories: task-specific risks, explicitly identified by an agent administrator for a given task's objectives and constraints, and systemic risks, which arise from an agent's interactions with its environment and can make an otherwise-normal action harmful depending on context (e.g. renaming a file that overwrites an existing one).
- AGrail supports both a default set of universal safety criteria (information confidentiality, integrity, and availability) applicable across agent types, and manually authored task-specific safety criteria for narrower domains.
- Safe-OS assigns OS agents two distinct user identities — a root user with sudo privileges and a regular user without — to represent access-control violations realistically, and includes both harmful and benign scenarios to measure guardrail overdefensiveness.
- On Mind2Web-SC and EICU-AC, AGrail built on Claude-3.5-Sonnet achieves 94.0% and 98.4% label-prediction accuracy respectively; on Safe-OS, it achieves 95.6% normal-scenario accuracy while keeping system-sabotage and prompt-injection attack success rates at 3.8% and 0%.
- An ablation study finds AGrail's performance is stable across different memory-training data orderings when built on Claude-3.5-Sonnet, but GPT-4o-mini shows significant variability, indicating stronger foundation models make the framework more robust to input-sequence effects.
- A domain-transferability test — training AGrail's memory on Mind2Web-SC and transferring it to EICU-AC — found no performance degradation on Claude-3.5-Sonnet and only a 5.6% drop on GPT-4o, which the authors present as evidence of AGrail's transferability across downstream tasks under universal safety criteria.
- The authors state two limitations: AGrail relies on off-the-shelf LLMs as its reasoning components rather than a model purpose-trained for guardrailing, and its auxiliary detection tools are limited by the current scarcity of tooling built specifically for LLM-agent security.

## Notes

The paper positions AGrail against two named prior systems it argues are limited by manually specified trusted contexts: GuardAgent, which struggles with dynamic downstream tasks, and Conseca, whose LLM-generated adaptive safety policies can misinterpret task requirements and become either overly restrictive or overly permissive. The paper's main experiments use GPT-4-Turbo (for prompt-injection attacks) and GPT-4o (for other attacks) as the OS agent's foundation model, and evaluate defense agencies including LLaMA-Guard3, GuardAgent, AgentMonitor, and ToolEmu as baselines.
