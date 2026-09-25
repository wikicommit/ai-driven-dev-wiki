---
title: "Towards Secure Agent Skills: Architecture, Threat Taxonomy, and Security Analysis"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-skills, agent-security, threat-modeling]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2604.02837'
    hash: sha256:6c5c15e538769fcda1bc3667ae0079f115ff185d93373b8bc3f11f45abf590d3
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A security analysis of the Agent Skills framework that defines a four-phase skill lifecycle, builds a threat taxonomy of seven categories and seventeen scenarios, and validates it against five confirmed security incidents."
  author: ["Zhiyuan Li", "Jingzheng Wu", "Xiang Ling", "Xing Cui", "Tianyue Luo"]
  datePublished: "2026-04-03"
  keywords: ["agent skills", "threat taxonomy", "security analysis", "LLM agents"]
---

The paper describes [[DefinedTerm/agent-skills]] as an emerging open standard that defines a modular, filesystem-based packaging format through which LLM-based agents acquire domain-specific expertise on demand. It notes that despite rapid adoption across multiple agentic platforms and the emergence of large community marketplaces, the security properties of Agent Skills had not been systematically studied, and presents itself as the first comprehensive security analysis of the framework.

The authors define the full lifecycle of an Agent Skill in four phases — Creation, Distribution, Deployment and Execution — and identify the structural attack surface each phase introduces. On that basis they construct a threat taxonomy and validate it against five confirmed security incidents in the Agent Skills ecosystem, then discuss defense directions for each threat category, open research challenges, and recommendations for stakeholders.

## Key Points

- The paper models an Agent Skill's lifecycle in four phases: Creation, Distribution, Deployment and Execution, each with its own structural attack surface.
- Its threat taxonomy comprises seven categories and seventeen scenarios organized across three attack layers, grounded in both architectural analysis and real-world evidence.
- The taxonomy is validated through analysis of five confirmed security incidents in the Agent Skills ecosystem.
- The authors conclude that the most severe threats arise from structural properties of the framework itself: the absence of a data-instruction boundary, a single-approval persistent trust model, and the lack of mandatory marketplace security review.
- They argue that these structural threats cannot be addressed through incremental mitigations alone.

## Notes

The paper was submitted to arXiv on 3 April 2026 and is filed under Cryptography and Security (cs.CR) and Artificial Intelligence (cs.AI).
