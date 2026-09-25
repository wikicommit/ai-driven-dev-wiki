---
title: "Observation Masking"
type: "schema:DefinedTerm"
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
  description: "A context-management strategy for LLM agents that simply omits older environment observations from the agent's context history, rather than compressing that history with LLM-based summarization."
---

Observation masking is a context-management strategy for LLM-based agents in which older environment observations are simply omitted from the agent's context history, instead of the history being compressed with LLM-based summarization. It addresses the long, expensive context histories that agents accumulate through iterative reasoning, exploration and tool use.

## Usage

[[ScholarlyArticle/the-complexity-trap]] compares observation masking with LLM summarization, the approach it says state-of-the-art software engineering agents such as [[SoftwareApplication/openhands]] and [[SoftwareApplication/cursor]] use. Within [[SoftwareApplication/swe-agent]] on [[Dataset/swe-bench-verified]], across five model configurations, that paper finds that simple environment observation masking halves cost relative to the raw agent while matching, and sometimes slightly exceeding, the solve rate of LLM summarization. The same paper introduces a hybrid approach that reduces costs by a further 7% compared with observation masking alone and 11% compared with LLM summarization alone.

## When It Applies

The strategy applies to LLM agents whose iterative tool use produces long context histories, and the evidence for it comes from software engineering agents. How well-established it is rests on one study's measured results: the comparison above was run in SWE-agent on SWE-bench Verified, and the paper describes its evidence that the findings generalize to the OpenHands agent scaffold as initial. Its authors present the result as raising concerns about the trend towards pure LLM summarization.

## Related Terms

- [[DefinedTerm/compaction]] — a related approach to keeping an agent's context within bounds
- [[DefinedTerm/context-engineering]] — the broader practice of managing what enters an agent's context
