---
title: "Improving token efficiency in GitHub Agentic Workflows"
type: "schema:BlogPosting"
lang: en
tags: [agent-efficiency, cost, mcp, continuous-ai, observability]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/improving-token-efficiency-in-github-agentic-workflows/'
    hash: sha256:d822d379200b264d29bdaaa801e7ab7323005053aae56cc40cb282c1d50bf63c
review_status: reviewed
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A GitHub blog post on how the team behind GitHub Agentic Workflows instrumented the token usage of its own production workflows, used agentic auditor and optimizer workflows to find inefficiencies, and cut consumption mainly by pruning unused MCP tools and moving data fetching to the GitHub CLI."
  author: ["Landon Cox", "Mara Kiefer"]
  datePublished: "2026-05-07"
  publisher: "[[Organization/github]]"
reviewed_by: "joyk0117"
---

A post on the GitHub blog, dated May 7, 2026 and updated on May 13, 2026, describing how the
team that maintains [[SoftwareApplication/github-agentic-workflows]] set out to reduce the token
consumption of the agentic workflows it runs in its own repositories. Its premise is that agentic
workflows running automatically in CI can accumulate cost out of view, but that they are easier
to optimize than interactive sessions because their work is fully specified in YAML and repeats on
every execution. The team began optimizing systematically in April 2026, and the post reports what
it instrumented, the optimizations it applied, and preliminary results.

The approach has three parts. The team first captured token usage for every run in one normalized
format through the API proxy that the workflows' security architecture already places between agents
and credentials. It then built two daily agentic workflows — an auditor that flags expensive or
anomalous workflows and an optimizer that proposes concrete fixes as GitHub Issues — and applied their
recommendations, chiefly removing unused MCP tools and replacing GitHub MCP data fetching with the
GitHub CLI. Finally it measured the effect with a cost-weighted metric, [[DefinedTerm/effective-tokens]],
and discusses at length why a lower token count does not by itself show that a workflow became more
efficient.

## Key Points

- Each agent framework (Claude CLI, Copilot CLI, Codex CLI) logged usage in a different format; the
  team used the workflows' API proxy to record every API call in a `token-usage.jsonl` artifact with
  input, output, cache-read and cache-write tokens, model, provider and timestamps.
- A Daily Token Usage Auditor aggregates recent usage by workflow and flags workflows whose usage rose
  sharply, the most expensive ones, and anomalous runs; a Daily Token Optimizer then reads a flagged
  workflow's source and logs and opens a GitHub Issue proposing specific optimizations. Both are
  themselves agentic workflows whose own usage appears in the daily reports.
- The post names unused MCP tool registrations as the most common inefficiency found: agent runtimes
  typically send every registered tool's name and JSON schema with each request, which for a GitHub
  MCP server with 40 tools can add 10–15 KB per turn. In the team's smoke-test workflows, removing
  unused tools cut per-call context by 8–12 KB with no change in behavior.
- A larger structural change was replacing GitHub MCP calls for data fetching with GitHub CLI calls,
  on the reasoning that an MCP tool call is also an LLM reasoning step while a `gh` command is a
  deterministic request with no LLM involvement. Two strategies are described: pre-agentic setup steps
  that download data the agent always needs to workspace files before it starts, and a transparent
  proxy that lets the agent run `gh` commands at runtime without seeing an authentication token.
- The post argues that measuring efficiency gains is hard for three reasons: tokens cost differently
  across models and token types (hence the Effective Tokens metric); the workload is a live repository,
  so one run may handle a five-line fix and the next a 200-line pull request; and output quality has no
  ground truth, so the team could only track process signals such as turns per run and tool-call
  completion rates.
- Across a dozen production workflows in the `gh-aw` and `gh-aw-firewall` repositories, nine received
  optimizer-recommended changes. For the five with at least eight runs before and after, the reported
  reductions in Effective Tokens were 62% for Auto-Triage Issues, 19% for Daily Compiler Quality, 37%
  for Daily Community Attribution, 43% for Security Guard and 59% for Smoke Claude. These are the
  authors' own preliminary measurements on their own workflows.
- The authors draw three patterns from these results: many agent turns are deterministic data
  gathering that can be moved out of the LLM loop ("the cheapest LLM call is the one you don't make");
  unused tools are expensive to carry, though removing them did not reduce cost for a workflow whose
  context was dominated by other material; and a single misconfigured rule can cause a runaway loop —
  their example is a bash allowlist that blocked every compile attempt and left an agent in a 64-turn
  fallback loop.
- They also note that not every recommended optimization produced measurable savings: one workflow's
  Effective Tokens rose 5%, which they attribute to a shift toward larger pull requests during the
  post-optimization period rather than to the optimization failing.

## Context

The authors write as the maintainers of the system they are optimizing, and the auditor and optimizer
workflows, MCP tool pruning and CLI substitution they describe are, in their words, available in the
GitHub Agentic Workflows framework. They present their results as preliminary and their quality
measures as process signals rather than outcome signals, stating that measuring tokens per unit of
correct work would need instrumentation that does not yet exist at scale for agentic CI workflows.
As next steps they describe moving from optimizing single workflows to analysing a run as a chain of
episodes, and from single workflows to the whole portfolio of workflows a repository runs, where
duplicated reads and overlapping automations become visible.
