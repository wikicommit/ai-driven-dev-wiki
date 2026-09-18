---
title: "AI Agentic Programming: A Survey of Techniques, Challenges, and Opportunities"
type: "schema:ScholarlyArticle"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A systematic literature review covering 152 academic papers from 2022-2025 that surveys AI agentic programming, introducing a taxonomy of agent behavioral dimensions and system architecture categories, reviewing core enabling techniques and coding benchmarks, and outlining open challenges and future research directions for building coding agents."
  author: ["Huanting Wang", "Jingzhi Gong", "Huawei Zhang", "Jie Xu", "Zheng Wang"]
  abstract: "AI agentic programming is described as an emerging paradigm where LLM-based coding agents autonomously plan, execute, and interact with tools such as compilers, debuggers, and version control systems. The survey introduces a taxonomy of agent behaviors and system architectures and examines techniques for planning, context management, tool integration, execution monitoring, and benchmarking datasets, highlighting challenges of the field and discussing opportunities for building reliable, transparent, and collaborative coding agents."
  keywords: ["Large Language Models", "LLMs", "AI Agents", "AI Agentic Programming"]
---

This paper is a systematic literature review of AI agentic programming, an emerging programming paradigm in which large-language-model-based coding agents autonomously plan, execute, and interact with tools such as compilers, debuggers, and version control systems. The authors followed a systematic-literature-review methodology, searching Google Scholar, the ACM Digital Library, IEEE Xplore, SpringerLink, and arXiv.org, plus proceedings from top-tier venues (FSE, ICSE, ASE, ICML, NeurIPS, AAAI), and combined agent, programming, and AI/LLM search-term clusters with Boolean operators.

The search retrieved 7,700 papers from database searches, of which 395 were selected for full-text review after title/abstract screening, 141 met all inclusion criteria, and a final corpus of 152 papers was assembled after backward and forward citation chaining. Included studies had to focus on AI systems for software development with autonomous or semi-autonomous behavior, demonstrate agentic behaviors such as planning, tool use, or adaptive decision-making, and present novel techniques, architectures, or evaluations; studies covering only traditional code completion or non-programming domains were excluded. Of the 152 academic references (2022-2025), the paper reports 5% appeared in 2022, 22% in 2023, 53% in 2024, and 20% in 2025.

Building on this corpus, the paper proposes a taxonomy of AI agentic programming systems along behavioral dimensions and system categories, reviews the techniques and tools that enable agentic behavior, compares agentic programming to related automation paradigms, surveys benchmarks and evaluation practices, and discusses open challenges and future research directions.

## Key Points

- The survey defines AI agentic programming as a paradigm distinguished from traditional code generation by four properties: autonomy (acting without continuous human supervision), interactivity (engaging with external tools during execution), iterative refinement (improving outputs from intermediate feedback), and goal-orientation (pursuing high-level objectives rather than responding to single prompts).
- It proposes a taxonomy of agentic behavior dimensions — reactivity vs. proactivity, single-turn vs. multi-turn execution, tool-augmented vs. standalone operation, and static vs. adaptive strategy revision — and of agent system categories: interactive code assistants, autonomous task-oriented agents, planning-centric agents, and multi-agent/collaborative systems.
- It compares AI agentic programming against six related paradigms it discusses in turn — program synthesis, code completion tools, DevOps automation, automated machine learning, multi-agent and human-AI collaboration systems, and robotics/reinforcement-learning agents — arguing that agentic programming is distinguished from each by autonomous, iterative, multi-step, tool-integrated behavior across the software development lifecycle, operating in a symbolic, language-driven environment rather than the physical or simulated environments of the latter two.
- Using SWE-Bench as a case study, it reports that commonly used coding benchmarks such as HumanEval and SWE-Bench are heavily biased toward Python and typically evaluate small, self-contained, or function/module-level problems rather than the large-codebase, multi-turn, tool-integrated workflows that practical agentic systems are expected to handle.
- It identifies six open challenges for the field: evaluation and benchmarking, communication protocols for multi-agent systems, domain-specific models for specialized environments, safety and privacy as agents gain autonomy, the mismatch between human-centric toolchains/languages and agent needs, and scalable memory for long-running tasks.

## Notes

The authors describe AI agentic programming as still in its early stages, noting that existing systems vary in architecture, autonomy, tool integration, and reasoning capability, and that the field lacks a standard taxonomy, benchmark suite, or evaluation methodology at the time of writing. The survey focuses primarily on LLM-driven agentic systems for software development, while noting that many of its insights extend to general AI agents in other domains such as information retrieval.
