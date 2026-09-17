---
title: "The Landscape of Prompt Injection Threats in LLM Agents: From Taxonomy to Analysis"
type: "schema:ScholarlyArticle"
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
  description: "A Systematization of Knowledge (SoK) covering 78 papers on prompt injection attacks and defenses against LLM agents, establishing taxonomies of attacks by payload-generation strategy and defenses by intervention stage, and introducing AGENTPI, a new benchmark for evaluating agent execution integrity under context-aware attacks."
  author: ["Peiran Wang", "Xinfeng Li", "Chong Xiang", "Jinghuai Zhang", "Ying Li", "Lixia Zhang", "Xiaofeng Wang", "Yuan Tian"]
  keywords: ["prompt injection", "LLM agents", "systematization of knowledge", "taxonomy", "benchmark"]
---

This paper presents a Systematization of Knowledge (SoK) of the prompt injection (PI) threat landscape in LLM agents, drawing on a systematic literature review of 78 papers (collected as of October 20, 2025) to establish taxonomies of PI attacks by payload-generation strategy (heuristic vs. optimization-based) and of PI defenses by intervention stage (text-level, model-level, and execution-level). It introduces [[Dataset/agentpi]], the first benchmark explicitly designed to evaluate agent execution integrity under context-aware attacks in dynamic, context-dependent tasks, where an agent's action depends functionally on observations retrieved from its environment rather than being fully determined by the user's initial prompt.

## Key Points

- The paper's attack taxonomy distinguishes heuristic payload-generation techniques from optimization-based ones (e.g. fuzzing or gradient guidance used to generate stealthy payloads), noting that optimization-based attacks often face challenges with query efficiency or require white-box access to the target model.
- The paper's defense taxonomy groups approaches by intervention stage: text-level (e.g. delimiters, sandwiching, paraphrasing, instruction-based defenses), model-level, and execution-level (e.g. tool filtering, policy-based approaches such as Progent and Melon); it notes that isolation-based approaches separating control and data flow can severely compromise an agent's utility on complex tasks.
- A central finding of the SoK's analysis is that most existing defenses and benchmarks focus on static inputs and overlook context-dependent tasks, where agents are authorized to rely on runtime environmental observations to determine their actions — a gap the paper's AGENTPI benchmark is designed to address.
- AGENTPI's 5 context-aware attacks span control flow (action switching, which forces a deviation to an unauthorized tool; parameter manipulation, which corrupts extracted arguments while preserving the correct action type), logic flow (branch divergence, which fabricates false facts to steer conditional execution; reasoning corruption, which interferes with cognitive operations such as aggregation or sorting), and authority flow (delegation exploitation, which abuses an explicit user delegation of authority to an external context to exceed the implicit safety boundary of the original intent).
- In an empirical evaluation of 9 defense configurations across the text-level and execution-level categories against GPT-4o-mini, the paper reports that execution-level defenses such as Progent and Melon reduce the attack success rate for action-switching and delegation-exploitation attacks to near zero, but that this comes with a severe security-utility trade-off — e.g. Progent achieves the lowest attack success rate for action switching while causing a "catastrophic utility drop" to below 0.3 — whereas text-level defenses (e.g. delimiters, paraphrasing) preserve utility comparable to baseline but offer negligible security gains.
- The paper also reports that some execution-level defenses (e.g. Progent) show lower latency than the undefended baseline not because of genuine efficiency but as an artifact of an aggressive "early refusal" policy that terminates generation, and that execution-level defenses can bring up to 3× the computational cost of the baseline.
- The paper's conclusion states that current defenses often fail to preserve reasoning integrity against context-aware logic manipulation and struggle to simultaneously achieve high trustworthiness, high utility, and low latency, and it proposes open problems including fine-grained attention access control, hybrid human-AI intervention, and resource-aware availability defenses.

## Notes

The extracted text interleaves the paper's two-column layout in places, and several tables and figures are visually garbled by OCR/markdown conversion; the findings summarized above are drawn from the paper's readable prose (Sections 6-8) rather than from garbled table layouts.
