---
title: "Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG"
type: "schema:ScholarlyArticle"
lang: en
tags: [context-engineering, agentic-coding]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2501.09136'
    hash: sha256:044c9dc18233e488fe537a45dbd983d1d9e3c9ef3d4205b5598c00897eb34767
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An analytical survey of Agentic RAG systems, which embed autonomous agents into the retrieval pipeline to escape the static workflows of traditional RAG. It proposes a taxonomy of architectures by agent cardinality, control structure, autonomy and knowledge representation."
  author: ["Aditi Singh", "Abul Ehtesham", "Saket Kumar", "Tala Talaei Khoei", "Athanasios V. Vasilakos"]
  keywords: ["Agentic RAG", "autonomous AI agents", "reflection", "planning", "tool use", "multi-agent collaboration", "multi-step reasoning"]
---

This survey, by Aditi Singh, Abul Ehtesham, Saket Kumar, Tala Talaei Khoei and Athanasios V. Vasilakos across Cleveland State University, Kent State University, Northeastern University's Khoury College and the Roux Institute, and a Center for AI Research, is an analytical survey of [[DefinedTerm/agentic-rag]] systems. Its argument begins from a limitation it attributes to conventional [[DefinedTerm/retrieval-augmented-generation]]: while RAG addressed the problem of static training data producing outdated or inaccurate output, "traditional RAG systems are constrained by static workflows and lack the adaptability required for multi-step reasoning and complex task management."

Agentic RAG, on the paper's account, "transcends these limitations by embedding autonomous AI agents into the RAG pipeline." The paper does not claim the term: it attributes the convergence of RAG and agentic intelligence that gave rise to Agentic RAG to earlier work, and describes a field it says already suffers from inconsistent terminology. What it presents as its own is the taxonomy. Those agents draw on four agentic design patterns the paper names — reflection, planning, tool use, and multi-agent collaboration — to manage retrieval strategies dynamically, iteratively refine contextual understanding, and adapt workflows through operational structures the paper describes as ranging from sequential steps to adaptive collaboration.

## Key Contributions

- **Tracing the paradigm shift.** The survey traces the evolution of RAG paradigms up to the agentic form.
- **A principled taxonomy.** Agentic RAG architectures are classified along four axes: agent cardinality, control structure, autonomy, and knowledge representation.
- **Comparative analysis of trade-offs.** The paper compares design trade-offs across existing frameworks.
- **Applications.** It examines real-world applications in domains including customer support and virtual assistants, healthcare, legal and contract analysis, finance, education, enterprise document processing and graph-enhanced multimodal workflows, and distils practical lessons for system designers and practitioners.
- **Open research challenges.** It identifies challenges in evaluation, coordination, memory management, efficiency, and governance, and outlines directions for future research.

The survey maintains an accompanying GitHub repository for the material.

## Notes

The four design patterns the paper builds on — reflection, planning, tool use, and multi-agent collaboration — are the same vocabulary practitioner writing in this wiki's subject area uses for coding agents, which is what makes the survey relevant here even though it is not about software development. Its claimed benefits for Agentic RAG systems are stated in strong terms — "unparalleled flexibility, scalability, and context-awareness across diverse applications" — and are the survey's own characterisation rather than a measured result.

The domains it surveys for applications are outside this wiki's scope; what carries over is the structural claim, that a retrieval pipeline with an agent deciding what to retrieve next behaves differently from one with a fixed retrieval step. For the codebase-specific version of that same question — an agent choosing between lexical and semantic retrieval as it works — see [[DefinedTerm/semantic-search]], and for the agents themselves [[DefinedTerm/coding-agent]] and [[DefinedTerm/multi-agent-orchestration]].
