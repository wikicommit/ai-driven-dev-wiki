---
title: "Virtual tools"
type: "schema:DefinedTerm"
lang: en
tags: [agent-tooling, tool-selection, model-context-protocol]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/how-were-making-github-copilot-smarter-with-fewer-tools/'
    hash: sha256:f7d183a85afba62c3cc3e62a03d3754e8c7a408220693408ee51c3e391925be0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "GitHub's name for a group of functionally similar tools presented to a coding agent as a single tool it can expand on demand, so the model sees what is available without being shown every individual tool."
---

Virtual tools are, in GitHub's description for [[SoftwareApplication/github-copilot]] Chat in VS Code,
a way of functionally grouping similar tools under one "virtual tool" that the chat agent can expand
as needed — GitHub likens them to directories containing related tools. The model is given a general
sense of what is available without being flooded with hundreds of tool names, and because similar
tools tend to be used and activated together, GitHub says grouping them also reduces the cache miss
rate it would expect if the model searched for tools individually.

## Usage

GitHub introduced the approach, as reported in
[[BlogPosting/how-were-making-github-copilot-smarter-with-fewer-tools]], as a middle ground between
exposing every tool — the default VS Code toolset has about 40 built-in tools and
[[DefinedTerm/model-context-protocol]] servers can push the total into the hundreds — and filtering
the toolset in a way that restricts what the agent can do.

The groups are formed by what GitHub calls adaptive tool clustering. An earlier attempt fed all tools
to an LLM and asked it to group and summarize them, which GitHub abandoned because the number of
groups could not be controlled and sometimes exceeded model limits, the process was slow and costly
in tokens, and the model sometimes failed to categorize some tools. Instead, embeddings for each tool
are generated with GitHub's internal Copilot embedding model and grouped by cosine similarity, which
GitHub says gives precise, stable and reproducible groups. A model call still writes a summary of each
cluster, and tool embeddings and group summaries are cached locally so recomputing them is cheap.

The same idea is applied to Copilot's own built-in tools: a core set of 13 tools is shown up front,
and the remaining built-in tools are grouped into four virtual categories — Jupyter Notebook Tools,
Web Interaction Tools, VS Code Workspace Tools and Testing Tools — that the model expands only if
necessary.

## When It Applies

Virtual tools address the case where an agent has more tools than it can reason over efficiently —
GitHub reports that MCP servers can bring in enough tools to exceed some models' API limits. Grouping
alone leaves a failure mode: the model may open several wrong groups before finding the right one,
each costing a cache miss, an extra round trip and a chance of failure. GitHub pairs virtual tools
with [[DefinedTerm/embedding-guided-tool-routing]] for that reason. The technique and its reported
results come from a single vendor describing its own product.

## Related Terms

- [[DefinedTerm/embedding-guided-tool-routing]]
- [[DefinedTerm/model-context-protocol]]
