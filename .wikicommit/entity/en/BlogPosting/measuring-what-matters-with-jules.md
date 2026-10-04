---
title: "Measuring What Matters with Jules"
type: "schema:BlogPosting"
lang: en
tags: [agent-evaluation, agentic-coding, benchmarks]
sources:
  - type: url
    url: 'https://developers.googleblog.com/measuring-what-matters-with-jules/'
    hash: sha256:3408d4ef087197f194bffde1e189e65678ca24ad257a645d358a9c5f9bd161f6
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A Google Developers Blog post arguing that proactive coding agents, which pursue open-ended goals rather than well-defined tasks, should be evaluated on their insight policy. It describes a preliminary benchmark that recovers goals by clustering a team's historical bug fixes, and reports early results on it."
  author: ["Nghi Bui", "Georgios Evangelopoulos", "Zack Elliott"]
  datePublished: "2026-06-22"
  publisher: "[[Organization/google]]"
---

This post, written by two research scientists and a software engineer and published on Google's developer blog, argues that coding agents are moving from reactive assistants that complete tasks when prompted to proactive engines that continuously absorb context, spot emerging risks and surface diagnostic insights before developers ask. The authors frame the change as a shift from well-defined *tasks* to *goals*: a goal requires the agent to explore the codebase, discover what is relevant and surface observations that guide developers toward a higher-level objective.

Its argument about evaluation follows from that. Public benchmarks such as [[Dataset/swe-bench]] test whether an agent can complete a task like fixing a narrowly defined bug, and the authors state that no benchmarks exist for goals. Drawing on a recent paper of their own, they propose grading a proactive agent on its *insight policy*: deciding what matters, what evidence supports it, and whether to interrupt the developer or stay silent. The post's illustration of a proactive engine shows context streaming in, the engine maintaining development state and a model of the developer, emitting insights in four forms — notify, question, draft, or stay silent — and learning from the developer's response.

Most of the post describes how the authors built a preliminary evaluation for this, drawing on their work on continuous AI systems at Google Labs, and what it showed. The results are explicitly preliminary, measured on an initial sample of internal Google code.

## Key Points

- The authors' proposal for a ground truth is to mine a team's real bug-fixing history using two heuristics they name temporal proximity and semantic similarity.
- Their hypothesis is that several related bugs filed and fixed within a short period are often symptoms of a single underlying engineering effort: bugs about sandbox timeout errors, broker config failures and flaky network-isolation tests, for example, all point to a goal such as "Strengthen sandbox execution reliability", while each bug on its own is too task-specific to be a goal.
- The preliminary benchmark used 705 bugs (1,178 CLs) from internal Google codebases, clustered to reveal the higher-level goals developers were working toward.
- The individual bugs in each cluster became the ground-truth targets, and the codebase was reverted to its exact pre-fix state so the agent started where the human engineer had.
- The agent could investigate the codebase for up to three rounds, which the authors call its exploration budget (N), before producing its final insights.
- An LLM judged each predicted insight against the targets on a scale from 1 (irrelevant) to 5 (exact match); success was measured by the agent's average top score and by Hit@K, how often a highly accurate match appeared among its top K insights.
- With a single exploration round the agent consistently identified a highly relevant insight, averaging 4.5 out of 5, which the authors read as the core diagnostic logic working on straightforward problems.
- Raising the exploration budget from two rounds to three lifted Hit@5 from 33% to 57%, which the authors take as showing that extra passes help the agent find secondary signals it initially missed.

## Context

The post describes itself as reporting preliminary results on an initial sample. Its stated next steps are extending the evaluation to public GitHub data, pairing issues with the pull requests that resolved them so the method applies beyond Google, and taking in richer context streams such as issue trackers, conversations and design documents rather than the codebase alone.
