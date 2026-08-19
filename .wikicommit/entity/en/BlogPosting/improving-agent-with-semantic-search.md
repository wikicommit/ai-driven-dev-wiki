---
title: "Improving agent with semantic search"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, context-engineering]
sources:
  - type: url
    url: 'https://cursor.com/blog/semsearch'
    hash: sha256:157e4d6a1147f217b21dc17ae116534a1fa413895b2162f592cc28adf71e1915
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Cursor research post of 6 November 2025 reporting that giving its coding agent semantic search alongside grep raised answer accuracy by 12.5% on average, and describing how its embedding model is trained on agent session traces ranked by an LLM."
  author: ["Stefan Heule", "Emily Jia", "Naman Jain"]
  datePublished: "2025-11-06"
  publisher: "[[Organization/anysphere]]"
---

"Improving agent with semantic search" is a post filed under *research* on [[Organization/anysphere]]'s blog, dated 6 November 2025 and written by Stefan Heule, Emily Jia and Naman Jain. Its claim is that [[DefinedTerm/semantic-search]] earns its place in a coding agent's toolset alongside lexical search rather than replacing it, and it argues the point with the company's own offline evaluations and an online A/B test.

## Key Points

- The framing: when a coding agent receives a prompt, answering well requires building an understanding of the codebase by reading files and searching. Semantic search retrieves code segments matching natural-language queries — the example given is "where do we handle authentication?" — in addition to regex-based searching from a tool like grep.
- Cursor reports having trained its own embedding model and built indexing pipelines for fast retrieval.
- Its headline claims for adding semantic search: 12.5% higher accuracy in answering questions on average, ranging 6.5%–23.5% by model; code changes more likely to be retained in codebases; fewer iterations for users to reach a correct solution; and improved accuracy across all models tested, including all frontier coding models.
- Offline evaluation ran on [[Dataset/cursor-context-bench]], an evaluation dataset the company maintains for retrieving information in codebases with known correct answers, over all the most-used models in Cursor including its own Composer. The comparison held the model constant and varied whether semantic search was among the available tools; Cursor states that in every configuration semantic search significantly improved outcomes.
- The online A/B test gave both groups the same model, with only one group's agent able to use semantic search. Reported effects were smaller: code retention up 0.3%, rising to 2.6% on codebases of 1,000 files or more, and a 2.2% increase in dissatisfied follow-up user requests when semantic search was absent. The post attributes the smaller effect to the test covering all agent queries, not only those requiring search.
- The custom retrieval model is trained from agent sessions rather than generic code similarity. Because an agent performs multiple searches and opens several files before finding the right code, the traces reveal in retrospect what should have been retrieved earlier; an LLM ranks what content would have been most helpful at each step, and the embedding model is trained to align its similarity scores with those rankings.

## Context

The post's conclusion is deliberately hedged in two directions. It states that semantic search "is currently necessary to achieve the best results, especially in large codebases" — a claim about the present rather than a permanent one — and that Cursor's agent "makes heavy use of grep as well as semantic search, and the combination of these two leads to the best outcomes", so the post does not argue that lexical search is obsolete. It closes by saying the company continues to test and evaluate all the tools it gives the agent harness as models improve.

Every figure here is Cursor's own, measured on Cursor's own benchmark and user base, for a feature Cursor sells; none of it is independently replicated in this source. The A/B test result is the more externally meaningful of the two, and it is also the smaller.
