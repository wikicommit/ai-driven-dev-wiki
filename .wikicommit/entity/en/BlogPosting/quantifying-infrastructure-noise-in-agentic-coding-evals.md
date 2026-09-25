---
title: "Quantifying infrastructure noise in agentic coding evals"
type: "schema:BlogPosting"
lang: en
tags: [evaluation, benchmarks, agentic-coding]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/infrastructure-noise'
    hash: sha256:9b90b3bbedd0a21cb782473b01e46d26c615e6e342bfbc0dc3d3f8087925a2c6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An Anthropic engineering post reporting that infrastructure configuration alone can move agentic coding benchmark scores by several percentage points — 6 points between the most- and least-resourced setups on Terminal-Bench 2.0 — and recommending how evals should specify and enforce resources."
  author: ["Gian Segato"]
  datePublished: "2026-02-05"
  publisher: "[[Organization/anthropic]]"
---

The post argues that agentic coding benchmarks such as [[Dataset/swe-bench]] and [[Dataset/terminal-bench]] are not measuring model capability alone. Unlike a static benchmark, which scores a model's output directly, an agentic eval gives the model a full environment in which it writes programs, runs tests, installs dependencies and iterates, so the runtime becomes part of the problem-solving process — "two agents with different resource budgets and time limits aren't taking the same test." Anthropic reports that in its internal experiments, the gap between the most- and least-resourced setups on Terminal-Bench 2.0 was 6 percentage points (p < 0.01), which it notes can exceed the margins separating top models on leaderboards.

The finding came out of calibrating Anthropic's own Terminal-Bench 2.0 setup on a Google Kubernetes Engine cluster, where scores did not match the official leaderboard and as many as 6% of tasks were failing on pod errors. The post names the resulting confounder — what this wiki calls [[DefinedTerm/infrastructure-noise]] — and closes with the line that "a few-point lead might signal a real capability gap—or it might just be a bigger VM."

## Key Points

- Container runtimes enforce resources through two separate parameters: a guaranteed allocation reserved up front and a hard limit at which the container is killed. Anthropic's Kubernetes setup set both to the per-task spec, leaving no headroom for transient spikes, while the Terminal-Bench leaderboard used a different, more lenient sandboxing provider that tolerated temporary overallocation.
- Anthropic ran Terminal-Bench 2.0 under six resource configurations, from strict enforcement of the per-task specs (1x) to completely uncapped, holding the Claude model, harness and task set constant.
- Infra error rates fell monotonically as headroom grew, from 5.8% at strict enforcement to 0.5% uncapped; the drop from 1x to 3x (5.8% to 2.1%) was significant at p < 0.001.
- From 1x through 3x, success scores moved within the margins of noise (p = 0.40): most tasks that crashed at 1x would have failed anyway.
- Above roughly 3x, success rose faster than infra errors fell — about 4 points of success against 1.6 points of infra errors between 3x and uncapped — because extra resources let the agent try approaches that only work with generous allocations, such as pulling in large dependencies or running memory-intensive test suites. The total lift from 1x to uncapped was 6 percentage points (p < 0.01).
- The post's reading is that up to about 3x, extra resources fix reliability problems, while above it they change what the eval measures: tight limits reward lean, efficient strategies and generous limits reward agents that exploit all available resources. Its example is the `bn-fit-modify` task, where installing the standard Python data-science stack succeeds under generous limits but runs out of memory under tight ones.
- The effect was replicated across different Anthropic models, with a consistent direction and varying magnitude; the post says the same trends seem to hold for other models but that it has not rigorously tested them.
- A crossover experiment on SWE-bench, varying available RAM up to 5x across 227 problems with 10 samples each, showed the same monotonic effect at a smaller magnitude: 1.54 percentage points higher at 5x than at 1x.
- Resources are not the only hidden variable: time limits can matter, and Anthropic reports having observed anecdotally, without formally quantifying it, that pass rates fluctuate with time of day, likely because API latency varies.
- It recommends that evals specify both a guaranteed allocation and a hard kill threshold per task rather than a single pinned value, calibrating the band so that scores at the floor and ceiling fall within noise of each other; on Terminal-Bench 2.0 a 3x ceiling cut infra errors by roughly two-thirds while keeping the score lift within noise.
- It concludes that, until resource methodology is standardized, leaderboard differences below 3 percentage points deserve skepticism until the eval configuration is documented and matched.

## Context

The post is an evaluation-methodology argument from a model developer about the benchmarks its own models are compared on. Its figures come from Anthropic's internal experiments on its own infrastructure, and it is explicit about the limits of its evidence: the time-of-day effect is anecdotal, and results on non-Claude models are described as not rigorously tested. It frames its recommendations for three audiences — labs, which it says should treat resource configuration as a first-class experimental variable; benchmark maintainers, for whom publishing recommended resource specs, as Terminal-Bench 2.0 does, goes a long way while specifying enforcement methodology would close the gap; and consumers of benchmark results, for whom small score differences on agentic evals carry more uncertainty than the reported precision suggests.
