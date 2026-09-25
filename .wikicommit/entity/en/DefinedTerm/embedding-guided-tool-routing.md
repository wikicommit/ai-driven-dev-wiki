---
title: "Embedding-guided tool routing"
type: "schema:DefinedTerm"
lang: en
tags: [agent-tooling, tool-selection, embeddings]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/how-were-making-github-copilot-smarter-with-fewer-tools/'
    hash: sha256:f7d183a85afba62c3cc3e62a03d3754e8c7a408220693408ee51c3e391925be0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A tool-selection technique GitHub uses in Copilot Chat: before any tool group is expanded, the query's embedding is compared with embeddings of every tool and tool cluster so that the most semantically relevant tools are pre-selected and made visible to the model."
---

Embedding-guided tool routing is the name GitHub gives to a tool-selection step in
[[SoftwareApplication/github-copilot]] Chat in VS Code in which, before any tool group is expanded,
the system compares the embedding of the user's query against vector representations of all tools and
their clusters, pre-selecting the most semantically relevant candidates even when they sit deep inside
a group, and includes them directly in the model's candidate set.

## Usage

GitHub describes it in [[BlogPosting/how-were-making-github-copilot-smarter-with-fewer-tools]] as the
complement to [[DefinedTerm/virtual-tools]]. Once tools were grouped, the model would usually
eventually find the right tool, but often only after opening the wrong groups first. GitHub's example
is the request "Fix this bug and merge it into the dev branch", for which the model often opened
search tools, then documentation tools, then local Git tools, before realizing it needed the merge
tool inside the GitHub MCP tool group; with routing, the system can infer from the start that the
merge tool is likely to be needed and surface it directly.

GitHub measures the technique with Tool Use Coverage, defined as how often the model already has the
right tool visible when it needs it. In GitHub's benchmarks embedding-based selection reached 94.5%
coverage, against 87.5% for LLM-based selection and 69.0% for the default static tool list, which the
post describes as a 27.5% absolute improvement offline. In online testing, 72% of Insiders tool calls
were pre-expanded using embedding-based matching, compared with 19% of Stable tool calls under the old
method. The embeddings come from GitHub's own Copilot embedding model.

## When It Applies

The technique applies when an agent's tools are grouped behind expandable groups and the cost of
exploratory lookups — each wrong group lookup adds a cache miss, a round trip and a chance of failure
— is worth removing. In GitHub's implementation it relies on GitHub's internal Copilot embedding model,
which the post describes as optimized for semantic similarity tasks, and on tool embeddings that are
cached locally. The evidence for it is GitHub's own
offline benchmarks and online measurements of its own product, reported in a single post; GitHub names
exploring how embeddings, memory and reinforcement signals could combine as a future direction.

## Related Terms

- [[DefinedTerm/virtual-tools]]
- [[DefinedTerm/model-context-protocol]]
