---
title: "CodeScaleBench"
type: "schema:Dataset"
lang: en
tags: [agentic-coding, benchmark, evaluation, context-engineering, metrics]
sources:
  - type: url
    url: 'https://sourcegraph.com/blog/context-engineering'
    hash: sha256:004e8195be79c691c84abc9a3ab6d698b8815f7ee396e367c8aca94f56715dc3
  - type: url
    url: 'https://sourcegraph.com/blog/agentic-coding'
    hash: sha256:0555e00c666984a838cc1b7db05eafdeedd950e02544b3d77491c6bc5a918d1c
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Sourcegraph's benchmark for measuring how coding agents perform on large-codebase and multi-repository tasks, where retrieval quality affects execution time, retries, and cost. Its published results compare the same agent under two retrieval configurations across 370 enterprise-scale tasks."
  creator: "[[Organization/sourcegraph]]"
  datePublished: "2026-03"
  measurementTechnique: "Same agent run under two retrieval configurations across enterprise-scale tasks, scored on file recall, Precision@5, F1@5, task completion, and tool-call and wall-clock cost"
---

CodeScaleBench is a benchmark built by [[Organization/sourcegraph]] to measure how coding agents perform on large-codebase and multi-repository software engineering tasks. [[BlogPosting/agentic-coding-in-2026-a-practical-guide-for-big-code]] describes its focus as the regime "where retrieval quality affects execution time, retries, and cost" — that is, it is designed to isolate the contribution of context retrieval rather than of the model.

That focus is what distinguishes it from the general agentic benchmarks already common in the field. Where [[Dataset/swe-bench]] measures whether an agent can resolve a repository issue, CodeScaleBench holds the agent constant and varies what it can see, which makes it a measurement instrument for [[DefinedTerm/eighty-percent-problem]] specifically.

## Composition

The published construction, as reported in [[BlogPosting/context-engineering-a-practical-guide-for-ai-agents]], is a set of 370 enterprise-scale tasks over which the same agent is run under two configurations: a baseline of local grep, file, and read tools, and the publisher's own MCP-based retrieval layer. Scoring covers both retrieval quality — file recall, Precision@5, F1@5 — and task-level outcomes, including whether a task completes within benchmark limits and at what cost in tool calls and wall-clock time.

The material available here does not describe how the 370 tasks were selected or validated, which repositories they are drawn from, or whether the benchmark is publicly runnable.

## Use in Evaluation

The results published in March 2026, as summarised in the same post, report file recall rising from 0.127 to 0.277, Precision@5 from 0.140 to 0.478, and F1@5 from 0.099 to 0.262 between the two configurations. The post's own reading is that "the deltas matter less than what they unlocked": several difficult tasks moved from timing out on the baseline to completing within benchmark limits. Its two named examples are a Kubernetes monorepo task that hit the baseline's two-hour timeout but completed in 89 seconds with the retrieval layer, scoring 0.90 out of 1.0; and a cross-file refactor that took the baseline 96 tool calls and 84 minutes but took 5 tool calls and 4.4 minutes with it, at double the reward.

The obvious limitation is that these are a vendor's measurements of its own retrieval product, published on that vendor's blog, with the comparison drawn against a deliberately minimal baseline of local file tools rather than against a competing retrieval system. The absolute retrieval figures are also low in both configurations — a Precision@5 of 0.478 means fewer than half the top five results are relevant — which the posts do not discuss.
