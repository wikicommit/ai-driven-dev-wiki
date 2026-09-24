---
title: "TraceLab: Characterizing Coding Agent Workloads for LLM Serving"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, llm-serving, workload-characterization, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.30560'
    hash: sha256:90d9d93dde14b87925191228c1addb5b483ccd600b3080a99d134b04712cf1e3
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A University of Washington-led systems paper that releases a cross-provider trace of real day-to-day coding-agent use with Claude Code and Codex and analyses it from an LLM-serving perspective, characterising agentic loops, context growth, cost, tool calls and prefix-cache behaviour."
  author: ["Kan Zhu", "Mathew Jacob", "Chenxi Ma", "Yi Pan", "Stephanie Wang", "Arvind Krishnamurthy", "Baris Kasikci"]
  abstract: "The paper collects and releases a trace of roughly 4,300 coding-agent sessions containing about 350,000 LLM steps and 430,000 tool calls from its authors' day-to-day use of Claude Code and Codex. Its analysis shows that coding-agent workloads feature long autonomous loops, long contexts with short outputs, diverse and heavily tailed tool calls, and high but imperfect prefix-cache hit rates, pointing to optimisation opportunities such as lower-overhead tool calling, append-length-aware prefill, semantic-aware tool-latency prediction, and improved KV-cache management around human-paced gaps."
  keywords: ["coding agents", "LLM serving", "prefix caching", "KV cache", "tool calls", "workload trace"]
---

This paper, from researchers at the University of Washington with collaborators at Wuhan University
of Technology and Shanghai Jiao Tong University, sets out to fill a gap in the data available for
serving coding agents efficiently. It argues that existing public LLM-serving traces capture chat,
single-turn completion or short multi-turn interactions, and that capability benchmarks such as
[[Dataset/swe-bench]] and [[Dataset/terminal-bench]] contain relatively few narrowly scoped tasks,
so neither captures the long sessions, repeated tool calls, accumulated context and human-paced gaps
that shape the cost of serving coding agents.

To close that gap the authors release [[Dataset/tracelab]], built from the logs that
[[SoftwareApplication/claude-code]] and [[SoftwareApplication/openai-codex]] keep for each session
by default: about 4,300 sessions, roughly 350,000 LLM steps and 430,000 tool calls from 43
developers over about eight months and more than 20 model versions, which they describe as, to
their knowledge, the first large-scale cross-provider trace of real coding-agent use. They normalise
both agents' logs into a step-level schema — one LLM invocation plus the tool calls it produces —
that splits each step's input into prefix tokens read from the prefix cache and newly appended
tokens, anonymise it, and analyse it at the session, request and step level.

## Key Points

- The loop is largely autonomous: a session averages more than 9 requests (p99 of 137), and one
  request averages about 8 steps and 11 tool calls, with most steps triggered by tool results
  rather than the user. An average request takes 4.3 minutes end to end (median 38 seconds, p90 6.4
  minutes).
- Context mostly grows; major reductions are rare and are usually genuine
  [[DefinedTerm/compaction]] near the context limit. 9.7% of sessions undergo at least one
  compaction, far more often in Codex (18.4% of sessions) than Claude (4.5%), which the authors
  relate to Codex's shorter context length. Codex additionally shows frequent small context
  reductions at user-initiated steps.
- Steps have long contexts but short outputs: the median step carries about 119K prefix tokens, 875
  appended tokens and 214 output tokens, because frequent tool calls cut generation into many short
  steps.
- Prefix-token re-reads dominate cost. Priced at list rates, prefix tokens account for 59.5% of total
  cost against 11.2% for output tokens, which the authors say inverts the usual intuition that
  generation is the expensive part. A session costs $9.70 on average but $0.61 at the median.
- Human thinking time accounts for 92.3% of session wall-clock time; within a request, tool
  execution (59.8%) and LLM generation (41.0%) contribute comparable shares.
- Tool calls are heavily skewed: the top three tools (Bash, Read and Edit for Claude;
  exec_command, write_stdin and apply_patch for Codex) account for more than 80% of calls, and calls
  longer than one minute are about 4% of calls but 85% of total tool-call time. Latency also varies
  widely within a single tool type.
- The global prefix-cache hit rate is 95.7%, but misses concentrate on user-initiated steps after
  long idle gaps; after about an hour almost no steps hit. Only 19% of appended tokens are genuinely
  fresh, so the deployed caches prefill about 5.3 times more tokens than an eviction-free cache
  would. In an upper-bound estimate, retaining the cache across human thinking time would cut
  appended prefill by 45.9% and priced cost by 12.8%.
- From these observations the authors derive serving-system directions: denser or fused tool
  calling and lower-overhead tool-call approval paths, append-length-aware prefill routing, tool-latency
  prediction that uses the semantics of the requested operation rather than only the tool name,
  sparse attention for long prefixes, and cheaper KV-cache storage, better compression and smarter
  eviction or prefetching around idle gaps — including agent harnesses periodically refreshing the
  cache during long pauses.

## Notes

The paper positions itself against [[ScholarlyArticle/swe-chat-coding-agent-interactions-from-real-users-in-the-wild]]
and similar datasets that analyse behavioural or code-change outcomes of coding agents rather than
the interaction timeline and serving system behind them. Its authors note that the trace is drawn
from their own day-to-day research use, so results may not generalise to other organisations,
workflows or agent domains; that without providers' internal telemetry they can identify workload
patterns but only infer the mechanisms behind them, such as scheduling or cache policies; and that
future trace studies should extend the method to broader computer-use and automation agents.
