---
title: "semantic search"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, context-engineering, terminology]
sources:
  - type: url
    url: 'https://cursor.com/blog/semsearch'
    hash: sha256:157e4d6a1147f217b21dc17ae116534a1fa413895b2162f592cc28adf71e1915
  - type: url
    url: 'https://en.wikipedia.org/wiki/Retrieval-augmented_generation'
    hash: sha256:4ed19c495c97a8260144ed3ec7c896c259f810946c6cfede70e9b72793d85ee4
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "In a coding agent, a retrieval tool that returns segments of code matching a natural-language query — Cursor's example is \"where do we handle authentication?\" — as a complement to the regex-based searching a tool like grep provides. Cursor reports it raising answer accuracy by 12.5% on average across the models it tested."
---

Semantic search, in the coding-agent sense described by [[Organization/anysphere]], is a retrieval tool that "retrieves segments of code matching natural language queries, such as 'where do we handle authentication?', in addition to the regex-based searching provided by a tool like grep." It is offered as one of the tools [[SoftwareApplication/cursor]]'s agent uses to build an understanding of a codebase when it receives a prompt, rather than as a replacement for lexical search: Cursor's stated conclusion in [[BlogPosting/improving-agent-with-semantic-search]] is that its agent "makes heavy use of grep as well as semantic search, and the combination of these two leads to the best outcomes."

## Usage

Cursor's argument for the tool is empirical, and its numbers are its own. It reports having trained its own embedding model and built indexing pipelines for fast retrieval, and claims that semantic search significantly improves agent performance especially over large codebases: on average 12.5% higher accuracy in answering questions (a range of 6.5%–23.5% depending on the model), code changes more likely to be retained in codebases, fewer iterations for users to reach a correct solution, and improved accuracy across every model tested including all frontier coding models.

Those figures come from two kinds of measurement, reported with different effect sizes. Offline evaluation against [[Dataset/cursor-context-bench]] compared two tool sets — one including semantic search, one not — across the most-used models in Cursor, with Cursor stating that semantic search significantly improved outcomes in every configuration. An online A/B test, in which both groups used the same model but only one agent had semantic search available, produced smaller numbers: code retention up 0.3% overall and 2.6% on codebases of 1,000 files or more, and a 2.2% increase in dissatisfied follow-up user requests when semantic search was unavailable. Cursor explains the gap by noting the A/B test covers all agent queries, and not all requests require search.

The training method Cursor describes is what distinguishes its model from generic code similarity. It uses agent sessions as training data: because an agent working through a task performs multiple searches and opens files before finding the right code, analysing those traces shows in retrospect what should have been retrieved earlier in the conversation. Cursor feeds the traces to an LLM which ranks what content would have been most helpful at each step, then trains the embedding model to align its similarity scores with those rankings — a feedback loop it describes as learning from how agents actually work through coding tasks.

Cursor frames the necessity as current rather than permanent: semantic search "is currently necessary to achieve the best results, especially in large codebases", and it says it continues to test and evaluate all the tools it gives the agent harness as models improve.

### The same combination outside code search

Cursor's grep-plus-semantic-search conclusion has a direct counterpart in general retrieval practice. Wikipedia's account of [[DefinedTerm/retrieval-augmented-generation]] describes **hybrid search** as one way to mitigate exactly the weakness Cursor's numbers imply: vector-database searches — which it identifies with the semantic search technique — "can miss key facts needed to answer a user's question", so one approach is to run a traditional full-text search as well, combine its results with the text chunks linked to the retrieved vectors, and feed the merged text into the model for generation, using scoring or reranking to order it. The same account also notes, on chunking, that code files are best chunked and vectorized as whole functions or classes.

## Related Terms

Semantic search is a retrieval strategy inside the broader problem of getting the right material into a model's window, covered under [[DefinedTerm/context-engineering]]; the tools that use it are covered under [[DefinedTerm/coding-agent]], and the surrounding machinery under [[DefinedTerm/agent-harness]].
