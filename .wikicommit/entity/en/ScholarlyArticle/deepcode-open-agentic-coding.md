---
title: "DeepCode: Open Agentic Coding"
type: "schema:ScholarlyArticle"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.07921'
    hash: sha256:314c8fd358fe756fabd1a16577a270aadea8b7375da1f84868c4809b3eb32278
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A paper proposing DeepCode, an agentic framework that reframes document-to-repository code synthesis (e.g. reproducing a scientific paper as a codebase) as an information-flow management problem, reporting it surpasses commercial coding agents and PhD-level human experts on the PaperBench benchmark."
  author: ["Zongwei Li", "Zhonghang Li", "Zirui Guo", "Xubin Ren", "Chao Huang"]
  datePublished: "2025-12-08"
---

This paper presents DeepCode, an open agentic coding framework for high-fidelity document-to-repository synthesis — most centrally, reproducing a scientific paper's experiments as a complete, executable code repository using only the paper itself as specification. It frames the core obstacle as a conflict between information overload (papers are long, multimodal specifications) and the finite context window of the LLMs doing the generation, and proposes treating repository synthesis as an information-flow / channel-optimization problem.

DeepCode addresses this through three phases: Blueprint Generation (a Concept Agent and an Algorithm Agent independently analyze a hierarchically-indexed version of the source document, which a Code Planning Agent synthesizes into a single implementation blueprint); Code Generation (files are generated iteratively against that blueprint using CodeMem, a stateful summary-based memory of already-generated files, and CodeRAG, a retrieval-augmented system that injects patterns from external repositories only when needed); and Automated Verification (a static-analysis pass followed by sandboxed execution, with an iterative loop that feeds runtime errors back as corrective signals).

## Key Points

- On PaperBench Code-Dev's 20-ICML-paper benchmark (graded by SimpleJudge, an automated judge built on OpenAI's o3-mini), DeepCode scored 73.5±2.8, versus 43.3±1.1 for the best general-purpose LLM-agent baseline (o1 with Iterative Agent scaffolding) and 51.1±1.4 for PaperCoder, a specialized scientific-code-agent baseline.
- On a 5-paper subset compared directly against commercial coding agents using the same underlying model (Claude Sonnet 4.5-thinking), DeepCode scored 0.8541 average, versus Claude Code's 0.5871, Cursor's 0.5841, and Codex's (GPT-5-Codex-high) 0.3997 — the paper argues this gap, given the shared base model with Cursor and Claude Code, shows the gain comes from DeepCode's architecture rather than model choice.
- On a 3-paper subset, DeepCode averaged 75.9±4.5, exceeding the human baseline's 72.4 (the best-of-3 attempts from 8 ML PhD students/graduates from institutions including Berkeley, Cambridge, and Carnegie Mellon, working part-time over four weeks).
- An ablation across five LLM backbones found replication score tracked model capability closely under a fixed DeepCode architecture: Claude-4.5-Sonnet and GPT-5 scored 0.69-0.82 across three tasks, Claude-3.5-Sonnet and Gemini-2.5-Pro scored 0.44-0.73, and DeepSeek-R1 scored around 0.29 on all three.
- Ablating CodeRAG on Gemini-2.5-Flash showed up to a 70% relative gain from adding it, but the paper reports negligible gains from adding CodeRAG to a frontier model (Claude 4.5 Sonnet), concluding it mainly helps cost-efficient models that lack sufficient implementation patterns in their own parameters.
- Ablating CodeMem (comparing it against a naive sliding-window message-eviction baseline) found the naive approach scored as low as 0.33-0.43 on some tasks due to losing foundational class definitions to context truncation, while CodeMem restored scores to 0.70-0.92 on the same tasks.
- Ablating the Automated Verification phase found consistent but comparatively modest gains of 3.7-6.5%, attributed mainly to correcting residual errors (typos in variable names, missing dependencies, wrong command-line arguments) rather than fixing deeper logic problems, since the paper frames earlier phases as already achieving most of the technical correctness.
- The paper names three open challenges for future work: agentic capability versus computational cost (proposing hybrid architectures mixing large and small models), moving from "episodic" agents that reset per project to ones that accumulate reusable experience, and moving from a linear plan-then-code workflow to dynamic, bidirectional planning that can revise the blueprint mid-implementation.

## Notes

The paper is a preprint under review, not yet peer-reviewed at publication. Its evaluation relies on PaperBench Code-Dev (an existing OpenAI-created benchmark) and an LLM-based automated judge (SimpleJudge, built on OpenAI's o3-mini) rather than the paper's own from-scratch benchmark or human grading; the human-expert comparison baseline is also drawn from the benchmark's own prior publication, not newly collected by this paper. DeepCode's source code is published at github.com/HKUDS/DeepCode.
