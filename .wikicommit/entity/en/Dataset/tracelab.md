---
title: "TraceLab"
type: "schema:Dataset"
lang: en
tags: [coding-agents, llm-serving, workload-characterization]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.30560'
    hash: sha256:90d9d93dde14b87925191228c1addb5b483ccd600b3080a99d134b04712cf1e3
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A released, anonymised trace of roughly 4,300 real coding-agent sessions — about 350,000 LLM steps and 430,000 tool calls — collected from 43 developers' day-to-day use of Claude Code and Codex, intended for studying and optimising how coding agents are served."
  creator: ["Kan Zhu", "Mathew Jacob", "Chenxi Ma", "Yi Pan", "Stephanie Wang", "Arvind Krishnamurthy", "Baris Kasikci"]
  url: "https://github.com/uw-syfi/TraceLab.git"
  variableMeasured: ["session identifier", "tool-call identifier", "project identifier", "user identifier", "timestamps", "token usage", "message and tool input/output character counts"]
  temporalCoverage: "2025-09/2026-06"
---

TraceLab is a trace of real coding-agent usage collected and released by the authors of
[[ScholarlyArticle/tracelab]], a University of Washington-led study, to support research on serving
coding agents efficiently. It contains about 4,300 sessions comprising roughly 350,000 LLM steps and
430,000 tool calls, gathered from 43 developers over about eight months of their day-to-day use of
[[SoftwareApplication/claude-code]] and [[SoftwareApplication/openai-codex]], across more than 20
model versions. The authors describe it as, to their knowledge, the first large-scale cross-provider
trace of real coding-agent use.

## Contents

The trace is normalised into a step-level schema in which each row is one step: a single LLM
invocation together with the tool calls it produces. Each step's input is decomposed into prefix
tokens (history read from the prefix cache) and append tokens (newly added input, including user
messages, tool results and tokens introduced by cache misses), alongside output tokens, and each step
keeps an ordered list of timestamped events — user messages, tool results, reasoning and output
text, and tool calls — from which its timeline can be reconstructed.

By provider, the trace holds 2,676 Claude sessions from 37 users (October 2025 to June 2026) and
1,589 Codex sessions from 22 users (September 2025 to June 2026), for 357,161 LLM steps and 432,510
tool calls in total. It covers 23 models: within Claude, mostly opus-4-7 (63.1%), and within Codex,
mostly gpt-5.5 (47.5%) and gpt-5.4 (26.0%). Total input amounts to 54.90 billion tokens, of which
52.56 billion are prefix tokens and 2.34 billion append tokens, with 186.9 million output tokens;
the authors estimate its API list-price equivalent at about $40.4K.

## Provenance

The data comes from the session logs that Claude Code and Codex persist by default, which record
metadata, user messages, encrypted reasoning, intermediate output, tool calls and tool results. The
authors built a pipeline that extracts these logs, reconciles the two agents' differing event
structures, token accounting and tool-timing metadata into the unified schema, and anonymises the
result. To protect user privacy only a sanitised trace is released: session, tool-call, project and
user identifiers are replaced with stable pseudonyms, and raw user messages and tool input/output
text are dropped, keeping only their character counts along with token usage and timestamps. The
dataset, the collection pipeline and the analysis code are published in the project's GitHub
repository, with a project website at <https://tracelab.cs.washington.edu>.

Because the sessions come from the authors' own research workflows — system building, evaluation
and analysis — the authors caution that results drawn from it may not fully generalise to other
organisations, development workflows or agent domains.

## Use

[[ScholarlyArticle/tracelab]] uses the trace to characterise coding-agent workloads for LLM serving,
reporting among other findings a 95.7% global prefix-cache hit rate with misses concentrated after
human-paced gaps, and prefix-token re-reads accounting for 59.5% of priced cost.
