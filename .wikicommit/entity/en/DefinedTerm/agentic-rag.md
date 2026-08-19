---
title: "Agentic RAG"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agentic-coding, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2501.09136'
    hash: sha256:044c9dc18233e488fe537a45dbd983d1d9e3c9ef3d4205b5598c00897eb34767
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Retrieval-augmented generation with autonomous AI agents embedded in the pipeline, so that retrieval strategy is decided and revised as work proceeds rather than fixed in advance. The definition and taxonomy recorded here follow a survey by Singh and colleagues, which surveys an already-named paradigm rather than coining it."
---

Agentic RAG is [[DefinedTerm/retrieval-augmented-generation]] with autonomous AI agents embedded in the pipeline. The definition and taxonomy used here follow [[ScholarlyArticle/agentic-rag-survey]], which surveys an already-named paradigm — it attributes the convergence of RAG and agentic intelligence that gave rise to the term to earlier work — and whose case for the paradigm rests on what conventional RAG cannot do: traditional systems "are constrained by static workflows and lack the adaptability required for multi-step reasoning and complex task management", and Agentic RAG "transcends these limitations by embedding autonomous AI agents into the RAG pipeline."

What the agents contribute is decision-making about retrieval rather than a new retrieval mechanism. Drawing on four agentic design patterns the survey names — reflection, planning, tool use, and multi-agent collaboration — they dynamically manage retrieval strategies, iteratively refine contextual understanding, and adapt workflows through operational structures the survey describes as ranging from sequential steps to adaptive collaboration.

## Usage

The survey's taxonomy classifies Agentic RAG architectures along four axes, which is the most portable part of the framing: **agent cardinality** (how many agents), **control structure** (how they are coordinated), **autonomy** (how much they decide unaided), and **knowledge representation** (how retrieved material is held). It pairs that with a comparative analysis of design trade-offs across existing frameworks, and identifies open challenges in evaluation, coordination, memory management, efficiency and governance.

The claimed payoff is stated in the survey's own strong terms — "unparalleled flexibility, scalability, and context-awareness across diverse applications" — and should be read as the authors' characterisation rather than a measured outcome. The application domains it surveys include customer support and virtual assistants, healthcare, legal and contract analysis, finance, education, enterprise document processing and graph-enhanced multimodal workflows; software development is not among them.

The connection to this wiki's subject area is the shape of the idea rather than its stated applications. A coding agent that decides, mid-task, whether to grep, run a semantic query, or open a specific file is making exactly the retrieval-strategy decisions this term names — see [[DefinedTerm/semantic-search]] for a vendor's account of that choice in practice.

## Related Terms

The paradigm it extends is [[DefinedTerm/retrieval-augmented-generation]]; the design patterns it builds on are the same ones covered under [[DefinedTerm/coding-agent]] and [[DefinedTerm/multi-agent-orchestration]], and the broader problem it addresses is [[DefinedTerm/context-engineering]].
