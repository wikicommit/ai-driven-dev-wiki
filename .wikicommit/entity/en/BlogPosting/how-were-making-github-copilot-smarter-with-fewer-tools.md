---
title: "How we’re making GitHub Copilot smarter with fewer tools"
type: "schema:BlogPosting"
lang: en
tags: [agent-tooling, model-context-protocol, tool-selection]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/how-were-making-github-copilot-smarter-with-fewer-tools/'
    hash: sha256:f7d183a85afba62c3cc3e62a03d3754e8c7a408220693408ee51c3e391925be0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A GitHub blog post on how GitHub Copilot Chat in VS Code was changed so that an agent with access to hundreds of tools stays fast and accurate: embedding-based adaptive tool clustering into virtual tools, embedding-guided tool routing, and a default built-in toolset cut from about 40 tools to 13."
  author: ["Anisha Agarwal", "Connor Peet"]
  datePublished: "2025-11-19"
  publisher: "[[Organization/github]]"
---

A post on GitHub's blog, published on November 19, 2025, about tool overload in
[[SoftwareApplication/github-copilot]] Chat in VS Code. Its starting point is that Copilot Chat can
reach hundreds of tools through the [[DefinedTerm/model-context-protocol]], and that giving an agent
too many tools does not necessarily make it smarter and sometimes only makes it slower — the post
points to the "Optimizing tool selection..." spinner as the visible sign of a model trying to reason
across too many tools at once.

The post describes two systems GitHub built in response — [[DefinedTerm/embedding-guided-tool-routing]]
and adaptive tool clustering, which groups tools into expandable [[DefinedTerm/virtual-tools]] — and a
reduced default toolset that trims the built-in tools from 40 to 13 core ones. GitHub reports that
across benchmarks including SWE-Lancer and [[Dataset/swe-bench-verified]], run with both GPT-5 and
Sonnet 4.5, these changes improved success rates by 2-5 percentage points, and that in online A/B
testing they reduced response latency by an average of 400 milliseconds.

## Key Points

- The default VS Code toolset has about 40 built-in tools, and with MCP servers included the number
  can grow into the hundreds; MCP servers can bring in enough tools to exceed some models' API
  limits.
- GitHub's stated aim was to show the model only the tools most relevant to a query without
  restricting the agent's capabilities or trading user experience for lower latency.
- The middle-ground approach is "virtual tools": similar tools grouped under one virtual tool the
  agent can expand as needed, which the post likens to directories of related tools.
- Asking an LLM to group and summarize all tools was abandoned: the number of groups could not be
  controlled and sometimes exceeded model limits, it was slow and token-expensive, and the model
  sometimes left tools uncategorized, forcing retries.
- Tools are instead clustered by cosine similarity over embeddings from GitHub's internal Copilot
  embedding model, which the post says produces precise, stable and reproducible groups; a model call
  still summarizes each cluster, and embeddings and summaries are cached locally.
- Without routing, the model often opens several wrong groups before finding the right tool — the
  post's example is a request to fix a bug and merge it into the dev branch, where the model tries
  search, documentation and local Git tools before the merge tool in the GitHub MCP group — and each
  wrong lookup costs a cache miss, a round trip and a chance of failure.
- Embedding-guided tool routing compares the query embedding with embeddings of all tools and
  clusters before any group is expanded, pre-selecting the most semantically relevant candidates.
- GitHub reports 94.5% Tool Use Coverage for embedding-based selection in benchmarks, against 87.5%
  for LLM-based selection and 69.0% for the default static tool list; online, 72% of Insiders tool
  calls were pre-expanded with embedding-based matching versus 19% of Stable tool calls with the old
  method. These are GitHub's own measurements of its own product.
- An oversized built-in toolset degraded performance even without hitting model limits: GitHub
  observed a 2-5 percentage point drop in resolution rate on benchmarks including SWE-Lancer with the
  full toolset, and says the agent ignored explicit instructions, misused tools and called
  unnecessary ones.
- The 13 core tools were chosen from usage statistics and performance data and cover repository
  structure parsing, file reading and editing, context search and terminal use; the remaining
  built-in tools sit in four virtual categories — Jupyter Notebook, Web Interaction, VS Code Workspace
  and Testing tools.
- GitHub reports that users with the reduced toolset saw an average 190 ms decrease in time to first
  token and an average 400 ms decrease in time to final token.
- The post frames tool selection as an early form of long-context reasoning, and names exploring how
  embeddings, memory and reinforcement signals could combine into agents that learn how to use tools
  as the next step.

## Context

The post is written by GitHub staff about GitHub's own product, and all reported figures come from
GitHub's internal benchmarks and A/B tests. The post's acknowledgments credit a researcher on the
team with helping to write it.
