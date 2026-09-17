---
title: "Safe-OS"
type: "schema:Dataset"
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
  description: "A 100-example benchmark of prompt-injection, system-sabotage, and environment attacks against an online OS agent, built on AgentBench's OS agent and Docker-simulated environment, introduced to evaluate LLM-agent guardrails under systemic risk."
  creator: ["Weidi Luo", "Shenghong Dai", "Xiaogeng Liu", "Suman Banerjee", "Huan Sun", "Muhao Chen", "Chaowei Xiao"]
  url: "https://eddyluo1232.github.io/AGrail/"
  variableMeasured: ["description", "evaluation", "label", "user", "attack"]
---

Safe-OS is a 100-example benchmark for evaluating whether guardrail systems can detect systemic risks against an online OS agent, introduced alongside [[DefinedTerm/agrail]] in [[ScholarlyArticle/agrail]]. It is built on the OS agent and Docker-based simulated environment from AgentBench, extended to assign two distinct user identities — a root user with sudo privileges and a regular user without — so that access-control violations can be represented realistically.

## Contents

Each record follows AgentBench's OS-agent data format (a natural-language description, an optional initialization/start Bash script run inside Docker, a match- or code-based evaluation check, and metadata such as the acting user and, for attacks, an attack-type label and any injected guard-request principles). The 100 examples split into 30 system-sabotage attacks built from common LLM-jailbreak strategies (e.g. prompting a fork bomb), 27 benign normal-task examples, 20 environment-dependent attacks (risks that depend on the surrounding environment rather than being identifiable from the action text alone, such as an unintentional file overwrite), and 23 prompt-injection attacks (malicious instructions hidden in a file, path, or environment variable that the OS agent reads). Every command was manually verified to be executable against an OS agent powered by GPT-4o or GPT-4-Turbo, and the authors report that their red-team, prompt-injection, and environment attacks each achieve at least a 90% attack success rate on GPT-4-Turbo.

## Provenance

The dataset was constructed by the AGrail authors specifically because they judged existing OS-agent safety datasets to rely too heavily on LLM-generated synthetic test cases that do not fully reflect real-world scenarios; Safe-OS's attack scenarios are instead designed based on successful attacks previously reported against GPT-4-based OS agents. It runs in a Docker-simulated OS environment and is published as part of the AGrail project at <https://eddyluo1232.github.io/AGrail/>.

## Use

The introducing paper, [[ScholarlyArticle/agrail]], uses Safe-OS to evaluate [[DefinedTerm/agrail]] and baseline defense agencies (LLaMA-Guard3, GuardAgent, AgentMonitor, ToolEmu) on both attack-detection accuracy (lower attack success rate is better) and overdefensiveness (how much benign, normal-scenario activity is blocked); AGrail based on Claude-3.5-Sonnet is reported to reduce attack success rate to 3.8% for system-sabotage attacks and 0% for prompt-injection attacks while preserving 96% of benign actions, compared with baselines that in some cases blocked over 49% of benign actions.
