---
title: "Agent Security Bench (ASB)"
type: "schema:Dataset"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2410.02644'
    hash: sha256:240e3fda399587075bf76504650459f73c6bda43ebcf8baf0e8118cd3781e401
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A benchmarking framework for evaluating attacks and defenses against LLM-based agents, spanning 10 scenarios (e.g. e-commerce, autonomous driving, finance), 10 agents, over 400 tools, 27 attack/defense method types, and 7 evaluation metrics, introduced in the Agent Security Bench paper."
  creator: ["Hanrong Zhang", "Jingyuan Huang", "Kai Mei", "Yifei Yao", "Zhenting Wang", "Chenlu Zhan", "Hongwei Wang", "Yongfeng Zhang"]
  url: "https://github.com/agiresearch/ASB"
---

Agent Security Bench (ASB) is a benchmarking framework, introduced in [[ScholarlyArticle/agent-security-bench]], designed to formalize, benchmark, and evaluate attacks and defenses against LLM-based agents across realistic scenarios such as e-commerce, autonomous driving, and finance.

## Contents

ASB spans 10 scenarios, 10 agents targeting those scenarios, over 400 tools, 27 different types of attack/defense methods, and 7 evaluation metrics. It formalizes attacks that target different stages of an agent's operation: direct prompt injection (DPI) attacks that manipulate the user prompt directly, indirect prompt injection (IPI) attacks that embed malicious instructions in tool responses, a memory poisoning attack that corrupts a retrieval-augmented-generation memory database with adversarial key-value pairs, a Plan-of-Thought (PoT) backdoor attack targeting the agent's hidden system prompt, and mixed attacks that combine these. Its evaluation metrics include Attack Success Rate (ASR) and Refuse Rate (RR), used respectively to measure how effective an attack or a defense is and how well an agent recognizes and rejects unsafe requests.

## Provenance

ASB was created by researchers at Zhejiang University and Rutgers University, with its code published at github.com/agiresearch/ASB.

## Use

[[ScholarlyArticle/agent-security-bench]] uses ASB to benchmark 10 prompt injection attacks, a memory poisoning attack, the PoT backdoor attack, 4 mixed attacks, and 11 corresponding defenses across 13 LLM backbones, reporting attack success rates, refusal rates, and a combined Net Resilient Performance metric for each.
