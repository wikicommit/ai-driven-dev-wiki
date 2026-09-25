---
title: "Agent Skills for Large Language Models: Architecture, Acquisition, Security, and the Path Forward"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-skills, agent-architecture, survey, agent-security]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2602.12430'
    hash: sha256:2395d685ed58334e3fe7d29b145c497e368ba0b5ad83330017a3703ae18c3cf8
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A survey of the agent skills landscape — composable packages of instructions, code and resources that agents load on demand — organized along four axes (architecture, acquisition, deployment at scale, and security), which also proposes a Skill Trust and Lifecycle Governance Framework."
  author: ["Renjun Xu", "Yang Yan"]
  datePublished: "2026-02-12"
  keywords: ["agent skills", "progressive disclosure", "Model Context Protocol", "skill acquisition", "agent security"]
---

This survey describes the move from monolithic language models to modular, skill-equipped agents as a defining shift in how large language models are deployed in practice. Rather than encoding all procedural knowledge in model weights, [[DefinedTerm/agent-skills]] — which the authors describe as composable packages of instructions, code and resources that agents load on demand — allow capabilities to be extended dynamically without retraining. The survey describes this as formalized in a paradigm of [[DefinedTerm/progressive-disclosure]], portable skill definitions, and integration with the [[DefinedTerm/model-context-protocol]].

The authors organize the field along four axes: architectural foundations, skill acquisition, deployment at scale, and security. On security, they point to recent empirical analyses reporting that 26.1% of community-contributed skills contain vulnerabilities, and on that basis propose a Skill Trust and Lifecycle Governance Framework — a four-tier, gate-based permission model that maps a skill's provenance to graduated deployment capabilities. The survey sets itself apart from prior surveys that broadly cover LLM agents or tool use by focusing specifically on the emerging skill abstraction layer and its implications for the next generation of agentic systems.

## Key Points

- The architectural-foundations axis examines the SKILL.md specification, progressive context loading, and the complementary roles of skills and MCP.
- The skill-acquisition axis covers reinforcement learning with skill libraries, autonomous skill discovery (SEAgent), and compositional skill synthesis.
- The deployment-at-scale axis covers the computer-use agent (CUA) stack, GUI grounding advances, and benchmark progress on OSWorld and SWE-bench.
- The security axis draws on recent empirical analyses — work the survey cites rather than its own measurement — reporting that 26.1% of community-contributed skills contain vulnerabilities.
- The authors propose a Skill Trust and Lifecycle Governance Framework: a four-tier, gate-based permission model that maps skill provenance to graduated deployment capabilities.
- The survey identifies seven open challenges, from cross-platform skill portability to capability-based permission models, and proposes a research agenda toward trustworthy, self-improving skill ecosystems.

## Notes

The paper was first submitted to arXiv on 12 February 2026 and last revised on 2 June 2026 (version 4). It was accepted by the Agent Skills '26 Workshop at the ACM Conference on AI and Agentic Systems 2026, and is filed under Multiagent Systems (cs.MA) and Artificial Intelligence (cs.AI). The authors describe the landscape they survey as having evolved rapidly over the preceding few months.
