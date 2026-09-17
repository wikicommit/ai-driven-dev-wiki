---
title: "AGENTPI"
type: "schema:Dataset"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.10453'
    hash: sha256:625f851b7a6a267411ea05b96666e7d41a492cc58a66c5c9afa63e6e1cbaab4c
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The first benchmark explicitly designed to evaluate LLM agent execution integrity under context-aware prompt injection attacks in dynamic, context-dependent tasks, covering 5 context-aware attack vectors across 4 task domains (Banking, Travel, Workspace, Slack), introduced in the prompt injection landscape SoK paper."
  creator: ["Peiran Wang", "Xinfeng Li", "Chong Xiang", "Jinghuai Zhang", "Ying Li", "Lixia Zhang", "Xiaofeng Wang", "Yuan Tian"]
---

AGENTPI is a benchmark, introduced in [[ScholarlyArticle/landscape-of-prompt-injection-threats-in-llm-agents]], designed to evaluate LLM agent execution integrity under context-aware prompt injection attacks — attacks that exploit dynamic, context-dependent tasks where an agent's actions must depend on runtime environmental observations rather than being fully determined by the user's initial prompt.

## Contents

The benchmark consists of 200 evaluation samples, organized as a grid of 5 attack vectors applied across 4 task domains, with 10 unique samples for each of the 20 combinations. The 5 attack vectors are action switching, parameter manipulation, branch divergence, reasoning corruption, and delegation exploitation. The attacks are tested across 4 distinct environments — Banking, Travel, Workspace, and Slack — simulating 66 unique tools across these domains to approximate real-world agent ecosystems and to ensure defenses are evaluated against diverse APIs and logic structures rather than a single scenario. A defining feature of AGENTPI is its context complexity: the average length of the tool observation into which payloads are injected is approximately 280 tokens, so that the benchmark evaluates an agent's ability to maintain attention over substantial structured data (such as JSON or logs) rather than just short strings. AGENTPI's evaluation metrics are multi-dimensional, covering attack success rate (ASR), utility under no-attack conditions, time cost, and token cost.

## Provenance

AGENTPI was created by researchers at UCLA, NTU, and NVIDIA, introduced as part of the same paper's systematic literature review and taxonomy of prompt injection threats in LLM agents.

## Use

[[ScholarlyArticle/landscape-of-prompt-injection-threats-in-llm-agents]] uses AGENTPI to empirically evaluate 9 defense configurations across text-level and execution-level categories against GPT-4o-mini, reporting attack success rate, utility, and computational cost trade-offs for each.
