---
title: "Effective Tokens"
type: "schema:DefinedTerm"
lang: en
aliases: ["ET"]
tags: [agent-efficiency, cost, token-cost]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/improving-token-efficiency-in-github-agentic-workflows/'
    hash: sha256:d822d379200b264d29bdaaa801e7ab7323005053aae56cc40cb282c1d50bf63c
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A cost-weighted token metric used by the GitHub Agentic Workflows team, which multiplies each token type by a weight reflecting its relative cost and scales the total by a per-model multiplier, so that consumption can be compared across model tiers."
---

Effective Tokens (ET) is a metric for the token consumption of an agent run in which each kind of
token is weighted by its relative cost and the result is scaled by the cost tier of the model that
consumed it. It was described by the team behind [[SoftwareApplication/github-agentic-workflows]] in
[[BlogPosting/improving-token-efficiency-in-github-agentic-workflows]] to deal with the observation
that raw token counts do not reflect cost: the same workflow run on a cheaper and a more expensive
model produces similar token counts at very different cost, so a switch of model tier looks like no
change in raw tokens. The post defines it as `ET = m × (1.0 × I + 0.1 × C + 4.0 × O)`, where *m* is a
model cost multiplier (0.25 for Haiku, 1.0 for Sonnet, 5.0 for Opus), *I* is newly processed input
tokens, *C* is cache-read tokens and *O* is output tokens.

## Usage

The weights encode the post's reasoning about token prices: output tokens carry four times the weight
of input tokens because they are the most expensive token type across all major providers, and
cache-read tokens carry a tenth because they are served from cache at a fraction of the cost of fresh
input. The authors state that the normalization means a 10% reduction in ET corresponds to a genuine
10% cost reduction whichever model is in use. They used it to compare runs of their own production
workflows before and after optimization, and to express aggregate savings — for one workflow, roughly
7.8 million ET saved over the observation period, assuming the pre-optimization rate.

The same post is explicit about what the metric does not capture. Because the workload of a workflow
running against a live repository varies from run to run, a lower ET can mean the workflow did less
work rather than the same work more efficiently; the authors track LLM API call counts alongside
token counts, reading steady turns per run with falling tokens per call as a genuine improvement. ET
also says nothing about output quality. In one of their workflows ET rose 5% after optimization,
which they attribute to a shift toward larger pull requests and a 14% rise in output tokens — the
most heavily weighted term — rather than to the optimization failing.

## When It Applies

ET is a working metric defined by one team, in one blog post, for measuring its own workflows. It
assumes that the weights and model multipliers track actual prices, and the post gives them as fixed
values. It suits comparing the cost of runs of the same
workflow across model changes and optimizations, and is misread when a fall in ET is taken as
evidence of efficiency without checking whether the workload or the quality of the output changed.

## Related Terms

- [[DefinedTerm/token-caching]]
- [[DefinedTerm/model-context-protocol]]
