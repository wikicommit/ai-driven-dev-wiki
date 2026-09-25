---
title: "The Complexity Trap: Simple Observation Masking Is as Efficient as LLM Summarization for Agent Context Management"
type: "schema:ScholarlyArticle"
lang: en
tags: [context-management, coding-agents, agent-efficiency]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2508.21433'
    hash: sha256:076629bf6f11cd9f92e8dc62895ee320175fe2824c0d7908b39b8a3bd7670bc9
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A 2025 arXiv paper comparing context-management strategies for LLM-based software engineering agents, which finds that simply masking older environment observations halves cost relative to the raw agent while matching the solve rate of LLM summarization, and introduces a hybrid of the two."
  author: ["Tobias Lindenbauer", "Igor Slinko", "Ludwig Felder", "Egor Bogomolov", "Yaroslav Zharov"]
  datePublished: "2025-08-29"
  keywords: ["observation masking", "LLM summarization", "context management", "software engineering agents"]
---

LLM-based agents solve complex tasks through iterative reasoning, exploration and tool use, and this process can produce long, expensive context histories. The paper notes that state-of-the-art software engineering agents such as [[SoftwareApplication/openhands]] and [[SoftwareApplication/cursor]] use LLM-based summarization to deal with this, and asks whether that added complexity brings tangible performance benefits compared with simply omitting older observations.

The authors run a systematic comparison of the two approaches within [[SoftwareApplication/swe-agent]] on [[Dataset/swe-bench-verified]], across five diverse model configurations, and report initial evidence that their findings generalize to the OpenHands agent scaffold. They find that simple environment [[DefinedTerm/observation-masking]] halves cost relative to the raw agent while matching, and sometimes slightly exceeding, the solve rate of LLM summarization. They also introduce a hybrid approach that reduces costs further.

## Key Points

- A simple environment observation masking strategy halves cost relative to the raw agent while matching, and sometimes slightly exceeding, the solve rate of LLM summarization.
- The main comparison is run within SWE-agent on SWE-bench Verified across five model configurations; the evidence that the findings carry over to the OpenHands agent scaffold is described as initial.
- A novel hybrid approach reduces costs by a further 7% compared with observation masking alone and 11% compared with LLM summarization alone.
- The authors say their findings raise concerns about the trend towards pure LLM summarization and point to untapped cost reductions on the efficiency-effectiveness frontier.

## Notes

The paper was first submitted to arXiv on 29 August 2025; version 3, dated 27 October 2025, is the camera-ready version for the 4th DL4C workshop co-located with NeurIPS 2025, and adds the OpenHands generality probe and the hybrid context-management strategy. The authors release code and data for reproducibility.
