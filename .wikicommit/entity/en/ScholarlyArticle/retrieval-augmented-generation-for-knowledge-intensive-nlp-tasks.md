---
title: "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks"
type: "schema:ScholarlyArticle"
lang: en
tags: [context-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2005.11401'
    hash: sha256:66544032f03e5d93e3beeb354e800a173532b2e4ef9979d86f69c0c3a6e5c8bc
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The paper that introduced retrieval-augmented generation: a general-purpose fine-tuning recipe combining a pre-trained seq2seq model's parametric memory with a dense vector index of Wikipedia as non-parametric memory, accessed by a pre-trained neural retriever."
  author: ["Patrick Lewis", "Ethan Perez", "Aleksandra Piktus", "Fabio Petroni", "Vladimir Karpukhin", "Naman Goyal", "Heinrich Küttler", "Mike Lewis", "Wen-tau Yih", "Tim Rocktäschel", "Sebastian Riedel", "Douwe Kiela"]
  keywords: ["retrieval-augmented generation", "knowledge-intensive NLP", "open-domain question answering", "non-parametric memory"]
---

This is the paper that introduced [[DefinedTerm/retrieval-augmented-generation]]. Its authors — from Facebook AI Research, University College London and New York University — start from a specific limitation of large pre-trained language models: they store factual knowledge in their parameters and reach state-of-the-art results when fine-tuned on downstream tasks, but "their ability to access and precisely manipulate knowledge is still limited", so on knowledge-intensive tasks they lag behind task-specific architectures, and providing provenance for their decisions and updating their world knowledge remain open problems.

The proposal is a general-purpose fine-tuning recipe for models that combine pre-trained parametric and non-parametric memory for language generation. The parametric memory is a pre-trained seq2seq model; the non-parametric memory is a dense vector index of Wikipedia accessed with a pre-trained neural retriever — Dense Passage Retriever (DPR) supplying latent documents conditioned on the input, with BART as the seq2seq model conditioning on those documents together with the input to produce output. The paper positions this against prior work on architectures with non-parametric memory trained from scratch for specific tasks: here both components are pre-trained and pre-loaded with extensive knowledge, so "the ability to access knowledge is present without additional training."

## Key Contributions

- **Two model formulations.** RAG-Sequence uses the same retrieved document to generate the whole target sequence, while RAG-Token can draw a different latent document for each target token, so different documents can be responsible for different tokens. The paper notes the two are equivalent when the target sequence has length one.
- **Results on open-domain question answering.** The models achieve state-of-the-art results on open Natural Questions, WebQuestions and CuratedTrec, and strongly outperform recent approaches using specialised pre-training objectives on TriviaQA.
- **Unconstrained generation beating extraction.** Despite these being extractive tasks, the authors find that unconstrained generation outperforms previous extractive approaches.
- **Parameter efficiency.** The paper reports that RAG-Sequence scores 44.5 exact match on Natural Questions where T5-large, the T5 model closest in parameter count at 770M, scores 28.9 — arguing that hybrid parametric/non-parametric models "require far fewer trainable parameters for strong open-domain QA performance". It notes the non-parametric index contributes no trainable parameters but does consist of 21M 728-dimensional vectors, 15.3B values, storable at 8-bit floating point precision to manage memory and disk footprint.
- **Generation quality on knowledge-intensive generation.** On MS-MARCO and Jeopardy question generation the authors report responses that are more factual, specific and diverse than a BART baseline. On FEVER fact verification they reach within 4.3% of state-of-the-art pipeline models that use strong retrieval supervision.
- **Swappable knowledge.** The paper demonstrates that the non-parametric memory can be replaced to update the models' knowledge as the world changes — the property that makes retrieval an alternative to retraining.

## Notes

The paper is candid about a failure mode it observed and did not solve. In preliminary experiments on some tasks such as story generation, the retrieval component would "collapse" and learn to retrieve the same documents regardless of input; the generator would then learn to ignore the documents, and the model would perform equivalently to BART. The authors suggest this could stem from a less explicit requirement for factual knowledge in such tasks, or from longer target sequences producing less informative gradients for the retriever, and note that other work had also found spurious retrieval results when optimizing a retrieval component for downstream performance.

Its relevance to this wiki is upstream rather than direct: the paper is about knowledge-intensive NLP, not about software development, but the pattern it names is the ancestor of the retrieval machinery coding agents now use — see [[DefinedTerm/semantic-search]] for the codebase-specific case and [[DefinedTerm/agentic-rag]] for the agent-mediated successor that later surveys propose.
