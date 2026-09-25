---
title: "Alibaba LingmaAgent: Improving Automated Issue Resolution via Comprehensive Repository Exploration"
type: "schema:ScholarlyArticle"
lang: en
tags: [software-issue-resolution, ai-coding-agent, repository-understanding, benchmarking]
sources:
  - type: url
    url: 'https://arxiv.org/html/2406.01422v2'
    hash: sha256:d9bfa615cea940d9674ffc433e47eb528cb25093699809cd3e9b54dabf0caf1d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A paper from Tongyi Lab, Alibaba Group presenting LingmaAgent, an issue-resolution agent deployed in Alibaba Cloud's TONGYI Lingma coding assistant that condenses a repository into a knowledge graph and explores it with Monte Carlo tree search before generating patches."
  author: ["Yingwei Ma", "Qingping Yang", "Rongyu Cao", "Binhua Li", "Fei Huang", "Yongbin Li"]
  datePublished: "2025-03-26"
  keywords: ["Automatic Software Engineering", "Software Engineering Agents", "Large Language Models", "Fault Localization", "Automated Program Repair", "Monte Carlo Tree Search"]
---

This paper presents LingmaAgent, an automated software engineering method for resolving issues in
real code repositories, deployed in TONGYI Lingma, an IDE-based coding assistant developed by
Alibaba Cloud. The authors, from Tongyi Lab at Alibaba Group, argue that earlier LLM-based agents
focused on local code information and so failed to grasp the global context and interdependencies
among functions and classes; their position is that a comprehensive understanding of the whole
repository is the most critical path to automated software engineering. The version described here
(v2, dated 26 March 2025) appears in the companion proceedings of FSE '25.

The method runs in three stages. It first builds a **repository knowledge graph** top-down, parsing
each file with abstract syntax trees into a hierarchical tree of files, classes and functions and
then adding directed edges for function call relationships — deliberately limited to functions, which
the authors call the basic unit of program execution. It then explores that graph with **Monte Carlo
tree search**, using BM25 relevance to the issue to guide expansion, an LLM prompted with in-context
examples and chain-of-thought to score how relevant each reached node is, and expansion along call
relationships from high-scoring nodes. Finally a summary agent condenses what was found into a
repository-level "experience" and plan, and the agent retrieves further code through search APIs
adopted from [[SoftwareApplication/autocoderover]] before localizing the fault and generating a
patch.

## Key Points

- On [[Dataset/swe-bench]]'s Lite subset (300 instances), LingmaAgent with GPT-4 Turbo resolved
  21.33% of issues against 18.00% for [[SoftwareApplication/swe-agent]] and 16.11% for AutoCodeRover
  under the paper's comparison, which the authors report as an 18.5% relative improvement over
  SWE-agent.
- Its resolved cases overlap only partly with SWE-agent's; adding SWE-agent-style execution feedback
  (reproduce, fix, re-run) to LingmaAgent raised its resolved rate to 27.7% with GPT-4, which the
  authors read as the two approaches being complementary.
- The same pipeline resolved 38.33% of SWE-bench Lite with Claude 3.5 Sonnet (v1022) and execution
  feedback, the highest of the models the paper tried.
- Ablations each lowered the resolved rate: removing the call graph (to 19.67%), removing the summary
  agent (17.67%), and removing both the tree search and the summary (16.00%).
- Adding an LLM-based static review agent that re-generated patches failing review also *lowered* the
  resolved rate, to 18.33%; the authors speculate that static review relies on surface grammatical
  information and misses logical errors.
- Fault localization was more accurate than either agent baseline at both function level (49.3%) and
  file level (67.7%).
- Raising the number of tree-search iterations raised the resolved rate with diminishing returns, and
  between 200 and 600 iterations the patch application rate fell.
- On an in-house Alibaba Cloud dataset of 194 issues across Java, JavaScript and TypeScript
  repositories, LingmaAgent resolved 16.9% fully automatically; on a random 30-issue subset where
  engineers could adjust its plans, search calls and fault localization (fewer than five
  interventions), the rate rose from 16.7% to 43.3% — a result on 30 issues.
- A Python prototype was open-sourced as RepoUnderstander.

## Notes

The authors name two limitations: the tree search consumes resources (they set 600 iterations and a
300-second limit, though 50 iterations already outperformed the other agents in their tests), and
their evaluation rests mainly on SWE-bench Lite, with a human-in-the-loop evaluation limited in scope
and a possibility that the models used saw parts of the test repositories in training. They propose a
dynamic, continuously updated version of SWE-bench as future work.

The paper sits within [[DefinedTerm/software-issue-resolution]]: its knowledge-graph construction is
a form of repository preprocessing and its tree search a localization strategy, and it compares
itself directly against the SWE-agent and AutoCodeRover agents it draws on.
