---
title: "A Survey on Code Generation with LLM-based Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, surveys, code-generation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.00083'
    hash: sha256:fa7359ad66622d19e4c575d652a495d4060c511a03ad122023b745174eada4d4
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A survey of code generation agents powered by large language models, characterising them by autonomy, an expanded task scope across the software development lifecycle, and a shift toward engineering practicality. It categorises single-agent and multi-agent techniques, reviews applications, benchmarks and deployed tools, and sets out five dimensions of open challenges."
  author: ["Yihong Dong", "Xue Jiang", "Jiaru Qian", "Tian Wang", "Kechi Zhang", "Zhi Jin", "Ge Li"]
  datePublished: "2025-09-30"
  abstract: "The survey argues that code generation agents powered by large language models are changing the software development paradigm, and distinguishes them from earlier code generation techniques by three core features: autonomy, an expanded task scope reaching beyond code snippets to the full software development lifecycle, and a shift of research emphasis from algorithmic innovation toward practical engineering concerns such as system reliability, process management and tool integration. It traces the technology's developmental trajectory, categorises its core techniques into single-agent and multi-agent architectures, details applications across the lifecycle, summarises mainstream evaluation benchmarks and metrics, catalogues representative tools, and proposes long-term research directions."
  keywords: ["Code Generation", "Software Development", "Large Language Models", "LLM-based Agent", "Multi-agent System"]
---

This survey reviews code generation agents built on large language models. Its organising claim is
that such agents differ from earlier code generation techniques in three ways: **autonomy**, the
ability to independently manage an entire workflow from task decomposition through coding and
debugging; an **expanded task scope**, reaching beyond generating code snippets to cover the full
software development lifecycle; and an **enhancement of engineering practicality**, a shift of
research emphasis away from algorithmic innovation and toward practical engineering challenges such
as system reliability, process management and tool integration. The authors frame this as a
transformation of the developer's role from code writer to task definer, process supervisor and
final result reviewer.

The corpus was assembled by searching the ACM Digital Library, IEEE Xplore, SpringerLink, Google
Scholar, DBLP and the China National Knowledge Infrastructure, using a bilingual Chinese and English
keyword strategy over titles, abstracts, keywords and index terms, with a retrieval window from 2022
to June 2025 and forward and backward snowballing. That produced 447 candidates, which five
screening rules — removing duplicates and near-duplicate versions from the same team, manually
vetting preprints for impact and innovation, excluding books, dissertations and short papers,
focusing on technical-innovation papers rather than pure technical reports or reviews, and a final
relevance pass — reduced to 100 core papers.

The survey is structured around a division between scaffolding techniques and application. It treats
single-agent methods under three headings (planning and reasoning, tool integration and retrieval
enhancement, and reflection and self-improvement) and multi-agent systems under three more
(workflows, context management and memory, and collaborative optimisation), then reviews applications
across the lifecycle, evaluation benchmarks and metrics, deployed tools, and open challenges.

## Key Points

- The survey distinguishes LLMs from LLM-based agents architecturally rather than by capability: an
  LLM's operation is a single, passive response process that lacks active planning, state maintenance
  or continuous interaction with external environments, while an agent constructs a dynamic workflow
  with autonomy, interactivity and iterativity, using the LLM as the reasoning engine that decides
  the next action from the current environmental state.
- It identifies four recurring multi-agent workflow shapes: pipeline-based division of labour, where
  each agent owns one stage and passes intermediate products on; hierarchical planning-execution,
  where higher-level agents decompose and lower-level agents implement; self-negotiation circular
  optimisation, centred on negotiation, reflection and self-feedback across multiple rounds; and
  self-evolving structural updates, where the system reorganises its own communication paths and
  responsibilities based on collaboration effectiveness and failure feedback.
- On context, it reports that the blackboard model — an explicit shared memory space holding task
  descriptions, intermediate results and revision records that all agents can read and update — was
  the first such mechanism introduced into code generation tasks, and that later systems extend it
  with decoupled instruction registers and file storage, brain-like short-term / long-term /
  evolutionary memory tiers, and self-organising agent pools that scale the number of agents rather
  than each agent's context window.
- It groups benchmarks into three generations: method- and class-level benchmarks focused on
  functional correctness of isolated code, programming-contest benchmarks that test algorithmic
  reasoning, and benchmarks that simulate real software development scenarios by providing a complete
  development environment in which agents interact with codebases, command-line interfaces and
  debugging tools.
- Beyond functional correctness it argues that evaluation should also measure process: API call cost
  and token consumption, latency, trajectory efficiency (how many steps an agent takes), and the
  quality of intermediate steps such as tool usage accuracy. It also notes evaluation expanding
  toward non-functional attributes including security, readability and complexity, maintainability
  via inter-module coupling, and whether agents update related tests to maintain coverage.
- It places deployed tools on an evolutionary trajectory of three categories — **Co-pilot**, close
  human-machine collaboration assisting a programmer; **Collaborator**, capable of understanding
  entire codebase contexts and engaging in deep interactive collaboration; and **Autonomous Team**,
  aimed at automating the whole development process with humans acting more as client or manager.
  [[SoftwareApplication/github-copilot]] is placed in the first, [[SoftwareApplication/cursor]] in
  the second, and [[SoftwareApplication/devin]] and [[SoftwareApplication/claude-code]] in the third.
- It argues that context engineering is not merely an extension of prompt design but a dynamic
  methodology for delivering the right information and tools at the right time and in the appropriate
  format, and classifies context defects into four types: context poisoning (incorrect or
  hallucinated information contaminating later reasoning), context distraction (redundant information
  overwhelming key signals), context confusion (format inconsistencies causing misinterpretation),
  and context conflict (contradictory information causing decision errors).
- Its challenges span five dimensions: limitations of agent core capabilities (domain-specific tasks,
  intent understanding, large codebases and project-level dependencies, multimodal inputs, context
  engineering); robustness and updatability (error cascading along the collaboration chain,
  coordination complexity as agent counts grow, and knowledge updates); tool integration and
  deployment in open environments (flexible and secure tool use, high operational cost, lightweight
  edge deployment); trustworthiness, security and ethical risk (reliability and debuggability,
  malicious code generation, copyright and ownership); and the completeness of evaluation systems.

## Notes

The survey positions itself against earlier English-language surveys of LLM-based agents for software
engineering, which it characterises as classifying technologies from an application perspective. Its
two stated differences are that it classifies from a methodological perspective, on the argument that
the underlying technical methods are common across application scenarios, and that it concentrates on
integrating the latest research advances given how quickly the field moves.

The authors note that the number of papers in the area has grown year over year since the technology
emerged in 2023, and that relevant work appears not only at software engineering venues but
frequently at mainstream natural language processing and artificial intelligence conferences,
which they read as evidence of attention from multiple disciplinary fields. They also observe that
because of the pace of the field relative to traditional review cycles, many results are published as
arXiv preprints, several of which have received high citation counts.
