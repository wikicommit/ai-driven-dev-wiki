---
title: "A Comprehensive Survey of Retrieval-Augmented Generation (RAG): Evolution, Current Landscape and Future Directions"
type: "schema:ScholarlyArticle"
lang: en
tags: [context-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2410.12837'
    hash: sha256:5b2969986c406dda926c6c42810d0a4661ec8b5bb51b7fc27fa2469c19ebdfcd
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A survey tracing retrieval-augmented generation from its foundational concepts to the state of the art, covering the basic architecture, technological advances in retrieval-augmented language models, applications across question-answering, summarization and knowledge-based tasks, and open challenges of scalability, bias and ethics."
  author: ["Shailja Gupta", "Rajesh Ranjan", "Surya Narayan Singh"]
  keywords: ["retrieval-augmented generation", "survey", "retrieval efficiency", "knowledge-intensive tasks"]
---

This survey, by Shailja Gupta and Rajesh Ranjan of Carnegie Mellon University and Surya Narayan Singh of BIT Sindri, presents what its abstract calls "a comprehensive study of Retrieval-Augmented Generation (RAG), tracing its evolution from foundational concepts to the current state of the art." Its framing of what [[DefinedTerm/retrieval-augmented-generation]] is for is the standard one: RAG combines retrieval mechanisms with generative language models to improve the accuracy of outputs, addressing key limitations of LLMs.

## Key Contributions

- **Architecture.** The survey explores the basic architecture of RAG, focusing on how retrieval and generation are integrated to handle knowledge-intensive tasks.
- **Technological review.** It provides a detailed review of significant technological advancements in RAG, including key innovations in retrieval-augmented language models.
- **Applications.** It covers applications across domains including question-answering, summarization and knowledge-based tasks.
- **Recent breakthroughs.** It discusses recent research breakthroughs, highlighting novel methods for improving retrieval efficiency.
- **Open challenges.** It examines ongoing challenges including scalability, bias, and ethical concerns in deployment.

## Notes

The survey is a general-purpose treatment of RAG rather than a software-engineering one, and this wiki records it for its account of the evolution and the open challenges rather than for domain-specific findings. Its identification of retrieval efficiency as the axis where recent breakthroughs cluster is the part that connects most directly to practice in this wiki's subject area, where retrieval cost and quality are what determine whether a coding agent finds the right code — see [[DefinedTerm/semantic-search]].

For the founding formulation of the technique see [[ScholarlyArticle/retrieval-augmented-generation-for-knowledge-intensive-nlp-tasks]]; for the argument that the static pipeline this survey describes is itself the limitation, see [[ScholarlyArticle/agentic-rag-survey]].
