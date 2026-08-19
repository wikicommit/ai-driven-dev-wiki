---
title: "retrieval-augmented generation"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2005.11401'
    hash: sha256:66544032f03e5d93e3beeb354e800a173532b2e4ef9979d86f69c0c3a6e5c8bc
  - type: url
    url: 'https://en.wikipedia.org/wiki/Retrieval-augmented_generation'
    hash: sha256:4ed19c495c97a8260144ed3ec7c896c259f810946c6cfede70e9b72793d85ee4
  - type: url
    url: 'https://arxiv.org/pdf/2410.12837'
    hash: sha256:5b2969986c406dda926c6c42810d0a4661ec8b5bb51b7fc27fa2469c19ebdfcd
  - type: url
    url: 'https://arxiv.org/pdf/2501.09136'
    hash: sha256:044c9dc18233e488fe537a45dbd983d1d9e3c9ef3d4205b5598c00897eb34767
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A technique that lets a language model retrieve and incorporate information from external data sources at inference time, rather than relying only on what is in its weights. Introduced in a 2020 paper as a combination of pre-trained parametric memory with a non-parametric dense vector index; the term now also covers a wide family of retrieval pipelines built on that idea."
  termCode: "RAG"
---

Retrieval-augmented generation (RAG) is a technique that enables large language models to retrieve and incorporate new information from external data sources: the model first refers to a specified set of documents, then answers the query, with those documents supplementing what is already in its training data. The effect is to make domain-specific or updated information usable without retraining. The term was introduced in [[ScholarlyArticle/retrieval-augmented-generation-for-knowledge-intensive-nlp-tasks]] in 2020, which framed it as combining pre-trained **parametric** memory — the seq2seq model's own weights — with **non-parametric** memory, a dense vector index of Wikipedia accessed through a pre-trained neural retriever.

## Usage

### The pipeline

The Wikipedia account of the common implementation describes a chain of stages. Reference data is converted into embeddings — numerical representations in a large vector space — and stored in a vector database; the data may be unstructured text, semi-structured, or structured such as knowledge graphs. Given a query, a document retriever selects the most relevant documents, whose text is fed into the model through prompt engineering of the original query; the model then generates output conditioned on both. Extra steps such as re-ranking retrieved information, context selection and fine-tuning are used to improve results, and the practice of prepending retrieved context so the model prioritises it over its training knowledge has been called "prompt stuffing".

Several improvement axes are catalogued there. On the **encoder** side, sparse vectors encode word identity and are dictionary-length and mostly zeros while dense vectors encode meaning more compactly; retrieval is tuned through dot-product similarity scoring, approximate nearest neighbour search in place of exact k-nearest neighbours, Late Interactions that compare words more precisely after retrieval, and hybrid schemes combining dense and sparse representations. On the **retriever** side, techniques include pre-training with the Inverse Cloze Task, supervised optimization that aligns retrieval probabilities with the generator's likelihood distribution by minimizing KL divergence, and reranking. **Chunking** strategies are fixed-length with overlap, syntax-based sentence splitting, and format-aware chunking — the Wikipedia account noting that code files are best chunked and vectorized as whole functions or classes. **Hybrid search** combines a vector-database search with a traditional full-text search and feeds the merged, rescored text to the model, on the grounds that vector search alone can miss key facts.

### As a foundation and as a constraint

The trajectory the two surveys here describe is one of escalating machinery around the same core idea. [[ScholarlyArticle/comprehensive-survey-of-retrieval-augmented-generation]] traces RAG's evolution from foundational concepts to the state of the art, covering retrieval-augmented language models and applications across question-answering, summarization and knowledge-based tasks, and names scalability, bias and ethical concerns in deployment as ongoing challenges.

[[ScholarlyArticle/agentic-rag-survey]] treats the static pipeline as the limitation rather than the achievement: traditional RAG systems, on its account, "are constrained by static workflows and lack the adaptability required for multi-step reasoning and complex task management", and [[DefinedTerm/agentic-rag]] is the paradigm it surveys — embedding autonomous agents into the pipeline to manage retrieval dynamically.

### Stated limitations

The sources agree that RAG mitigates rather than removes the underlying problem. Wikipedia records that RAG does not prevent hallucination — quoting *Ars Technica* that "it is not a direct solution because the LLM can still hallucinate around the source material in its response" — and that a model can generate misinformation even from factually correct sources if it misinterprets the context. It also notes RAG reduces but does not eliminate the need for retraining, and that models may answer rather than signal uncertainty when they lack sufficient information, an issue IBM is cited as attributing to a model's inability to assess its own knowledge limits.

The founding paper records a failure mode of its own from preliminary experiments, which it calls **retrieval collapse**: on some tasks such as story generation the retrieval component would learn to retrieve the same documents regardless of input, after which the generator learned to ignore the documents and the model performed equivalently to its non-retrieval baseline. Its suggested explanations are a less explicit requirement for factual knowledge in such tasks, or longer target sequences yielding less informative gradients for the retriever.

## Related Terms

Within this wiki's subject area, RAG is the general form of the retrieval problem that [[DefinedTerm/semantic-search]] addresses for codebases, and it sits inside the broader concern of [[DefinedTerm/context-engineering]] — getting the right material into a model's window. [[DefinedTerm/agentic-rag]] is the agent-mediated successor proposed for it, and [[DefinedTerm/model-context-protocol]] is a separate answer to the adjacent problem of standardizing how an agent reaches external systems at all.
