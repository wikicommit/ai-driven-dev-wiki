---
title: "Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-Based Agents"
type: "schema:ScholarlyArticle"
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
  description: "An ICLR 2025 paper introducing Agent Security Bench (ASB), a framework spanning 10 scenarios, 10 agents, over 400 tools, and 27 attack/defense method types, used to formalize and benchmark prompt injection, memory poisoning, and a novel Plan-of-Thought backdoor attack against 13 LLM backbones, finding current defenses largely inadequate."
  author: ["Hanrong Zhang", "Jingyuan Huang", "Kai Mei", "Yifei Yao", "Zhenting Wang", "Chenlu Zhan", "Hongwei Wang", "Yongfeng Zhang"]
  keywords: ["LLM agents", "prompt injection", "memory poisoning", "backdoor attack", "agent security", "benchmark"]
---

This paper introduces [[Dataset/agent-security-bench]] (ASB), a framework for formalizing, benchmarking, and evaluating attacks and defenses against LLM-based agents. It formally defines four attack families against an agent's operational pipeline — direct prompt injection (DPI, manipulating the user-prompt step directly), indirect prompt injection (IPI, embedding malicious instructions in tool responses), memory poisoning (corrupting a retrieval-augmented memory database with adversarial key-value pairs), and a novel Plan-of-Thought (PoT) backdoor attack targeting the agent's hidden system prompt — plus mixed attacks that combine several of these.

The paper benchmarks 10 prompt injection attacks, a memory poisoning attack, the PoT backdoor attack, 4 mixed attacks, and 11 corresponding defenses across 13 LLM backbones, including both closed models (e.g. Claude 3.5 Sonnet, GPT-3.5 Turbo, GPT-4o, GPT-4o-mini) and open models (e.g. LLaMA 3/3.1, Gemma2, Mixtral, Qwen2).

## Key Points

- Across all tested LLM backbones, the paper reports Mixed Attack (combining DPI, IPI, and memory poisoning) as the most impactful attack, with the highest average attack success rate (84.30%) and the lowest average refusal rate (3.22%); Memory Poisoning alone was the least effective, with an average ASR of 7.92%. DPI averaged 72.68% ASR, IPI 27.55%, and the PoT backdoor attack 42.12%.
- The paper reports that attack success rate and agent capability show a rise-then-fall relationship: more capable backbone models are initially more vulnerable because they follow injected instructions more readily (e.g. GPT-4o shows elevated ASR), but at the highest capability levels stronger refusal behavior counteracts this — the paper contrasts GPT-4o (20.05% refusal rate under DPI, 60.35% ASR) with GPT-3.5 Turbo (3.00% refusal rate, 98.40% ASR).
- The paper introduces a Net Resilient Performance (NRP) metric to jointly assess a backbone's task utility and adversarial resilience, reporting that Claude 3.5 Sonnet, LLaMA3-70B, and GPT-4o achieved relatively high NRP scores among the backbones tested.
- The paper reports that agent performance under no attack (PNA) is generally weaker than the same backbone LLM's standalone leaderboard quality, with Claude 3.5 Sonnet, LLaMA3-70B, and GPT-4o as the exceptions that matched or approached their standalone leaderboard performance.
- The paper's defense evaluation (against DPI and IPI) finds current prevention-based defenses largely inadequate: even the best-performing defenses it tested against DPI (Dynamic Prompt Rewriting, reducing average ASR to 44.45%, and an Instruction-based defense, reducing it to 56.87%) left a majority of attacks succeeding, and the paper reports these defenses often cause utility losses on primary tasks even when no attack is present.
- The paper's conclusion states that ASB reveals key vulnerabilities of LLM-based agents at every operational step (system prompt, user prompt, tool usage, and memory retrieval) and that current defenses show limited effectiveness against the attacks it benchmarks.

## Notes

Several tables and mathematical formalizations (attack/defense definitions in Sections 4.1–4.4) are rendered with garbled OCR artifacts in the extracted text; the figures and findings summarized above are drawn from the paper's readable prose (Sections 5.3, 5.4, and 6) rather than from the garbled formulas or table layouts themselves.
