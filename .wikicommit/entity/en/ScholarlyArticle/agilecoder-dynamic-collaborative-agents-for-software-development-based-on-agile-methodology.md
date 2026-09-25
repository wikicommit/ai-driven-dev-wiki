---
title: "AgileCoder: Dynamic Collaborative Agents for Software Development based on Agile Methodology"
type: "schema:ScholarlyArticle"
lang: en
tags: [multi-agent, coding-agents, software-process, code-generation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2406.11912'
    hash: sha256:0bb6ae4b557525a907cd35ba8c21dc61c06135078855bd330d09e93218f0e09d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A preprint from the FPT Software AI Center proposing AgileCoder, a multi-agent software development framework that assigns Agile roles to LLM agents, works in sprints, and maintains a dynamically updated code dependency graph for context retrieval."
  author: ["Minh Huynh Nguyen", "Thang Chau Phan", "Phong X. Nguyen", "Nghi D. Q. Bui"]
  abstract: "The authors argue that existing software agents frequently oversimplify software development workflows, and propose AgileCoder, a multi-agent system that integrates Agile Methodology into the framework by assigning Agile roles such as Product Manager, Developer and Tester to different agents, which collaboratively develop software from user inputs and organize their work into sprints for incremental development. They also introduce the Dynamic Code Graph Generator, a module that creates a Code Dependency Graph dynamically as the codebase is updated so that agents can better comprehend it, and report that AgileCoder surpasses ChatDev and MetaGPT."
---

This preprint, from the FPT Software AI Center in Vietnam, takes aim at how LLM-based software
agents model the development process. It describes [[SoftwareApplication/metagpt]], which encodes
Standardized Operating Procedures, and [[SoftwareApplication/chatdev]], which simulates a virtual
chat-powered technology company, as both following the classic waterfall model, and argues that
this oversimplifies the dynamic, iterative nature of real-world development, where, it says,
roughly 70% of professional teams adopt Agile Methodology. It also argues that these systems rely
too heavily on LLMs to manage code generation across an entire repository.

The paper's answer is [[SoftwareApplication/agilecoder]], a multi-agent framework that mimics an
Agile workflow. Agents play the roles of Product Manager, Scrum Master, Developer, Senior Developer
and Tester; after the Product Manager builds a product backlog of tasks and acceptance criteria,
work proceeds in sprints, each with planning, development, testing and review phases, and outputs
are inherited from one sprint to the next until the Scrum Master judges the software deliverable.
Alongside the agents, a static-analysis module, the Dynamic Code Graph Generator, maintains a Code
Dependency Graph whose nodes are code files and whose edges are mainly import relations, updated
whenever the code changes; it is used to decide which files need new tests, to order test
execution, and to retrieve the relevant cross-file context when an error occurs, rather than
loading the whole codebase into the model.

The framework is evaluated on HumanEval and MBPP and on [[Dataset/projectdev]], a set of 14 more intricate
software development tasks the authors compiled, which they describe as more appropriate than
HumanEval and MBPP for assessing complex multi-agent systems. They report that AgileCoder achieves
the best pass@1 among the compared agents on the first two and markedly higher executability than
ChatDev and MetaGPT on ProjectDev, at the cost of more tokens and running time.

## Key Points

- The paper characterizes MetaGPT and ChatDev as following a waterfall model, and proposes adapting Agile Methodology — roles, backlogs and sprints — to a multi-agent framework instead.
- AgileCoder's agents take the roles Product Manager, Scrum Master, Developer, Senior Developer and Tester, and each sprint runs planning, development, testing and review phases.
- The Senior Developer performs a static code review in three sequential steps — basic implementation checks, backlog compliance, then acceptance criteria and bug identification — which in an ablation beats a single-step review.
- The Dynamic Code Graph Generator maintains a Code Dependency Graph of files and their import relations, used to select which files to test, to derive a testing plan by reversing a topological order, and to retrieve context for bug fixing.
- Agents communicate in two-party instructor–assistant conversations with a message stream as working memory, while a global message pool holds all conversation outputs and task statuses, each conversation accessing only the relevant parts.
- With GPT-3.5 Turbo, AgileCoder reports 70.53% pass@1 on HumanEval and 80.92% on MBPP, which the authors state are improvements of 7.71% and 6.19% over MetaGPT.
- On ProjectDev, AgileCoder reports 57.79% executability against 32.79% for ChatDev and 7.73% for MetaGPT, with no non-executable programs, while using more tokens and running time and completing tasks in 1.64 sprints on average.
- Ablations report that removing incremental development, generated test suites or code review lowers pass@1, and that without the code dependency graph executability falls from 57.50% to 23.38% and context-length errors appear.

## Notes

The authors acknowledge that HumanEval and MBPP, which mostly contain simple competitive
programming problems, may not suit complex multi-agent systems, and note that the comparable
benchmarks from MetaGPT (SoftwareDev) and ChatDev (SRDD) are not publicly available, whereas they
state ProjectDev will be released. ProjectDev executability is assessed manually by developers
against each task's list of requirements. Among the limitations they list are the continued
reliance on LLMs for code generation and decision-making, the computational cost of maintaining
the dependency graph as codebases grow, and the absence of non-technical aspects of Agile
development such as team dynamics; they suggest pair programming, CI/CD, Kanban or Lean as
further Agile practices to explore. The paper sits among work on
[[DefinedTerm/llm-based-multi-agent-system]] designs for software development.
