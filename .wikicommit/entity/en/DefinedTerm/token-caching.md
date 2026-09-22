---
title: "Token Caching"
type: "schema:DefinedTerm"
lang: en
tags: [llm-internals, coding-agents, cost]
sources:
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/how-coding-agents-work/'
    hash: sha256:a8be3f0926e2b75d77e83036446bf575cf49b7dff42641018af0909da9d387eb
  - type: url
    url: 'https://baoyu.io/blog/2026-04-06/claude-code-token-optimization'
    hash: sha256:287e81a37d9c6dc213f594b3dd3f401600e6fe71f7d49622f3492c33f13b0a75
  - type: url
    url: 'https://www.anthropic.com/engineering/april-23-postmortem'
    hash: sha256:269dd6e147333715b02167db5eedbc394fe254ceebed15d9cf7f2a05a25c87f5
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A cheaper provider rate for input tokens whose prefix has already been processed recently, because the expensive calculations behind that prefix can be cached and reused. It is why coding agents are built to append to a conversation rather than revise its earlier parts."
---

Token caching is the practice, offered by most model providers, of charging a cheaper rate for
**cached input tokens** — common token prefixes that have already been processed within a short time
period — because the underlying infrastructure can cache and reuse many of the expensive calculations
that produced them. As the first source describes it, it is a matter of what an unchanged prefix is charged
at rather than of what the model can do.

## Usage

Its relevance to coding agents follows from how [[DefinedTerm/chat-templated-prompt]] works. Models
are stateless, so the software around them replays the whole conversation on every turn, and the
input grows as the session lengthens. Token caching offsets part of that growth — but only for the
prefix that has not changed. The design consequence is stated directly in the first source: coding agents
are built with this optimization in mind and **avoid modifying earlier conversation content**, so
that the cache is used as efficiently as possible.

That constraint is worth noting because it is a design pressure the source states outright while
saying nothing about how it is resolved: efficient cache use and rewriting earlier conversation
content pull against each other, and the agents the source describes resolve it by not rewriting.

[[BlogPosting/claude-code-token-saving-guide]] works out what the mechanism costs in practice for one
agent. It describes caching as having two conditions. The first is that matching is **prefix-only and
exact**: the match must run from the very beginning of the input, so changing something early
invalidates everything after it, while appending to the end leaves the whole preceding prefix valid.
That is why the post says input is ordered with the unchanging material first — system instructions and
tool definitions, then conversation history, then the new message. The second is that a cached entry
**expires**; that post puts the window at one hour for a main agent and five minutes for a subagent,
with each hit refreshing the timer, so an interaction that keeps up a steady rhythm can hold a cache
open indefinitely. It also reports that cache reads cost about a tenth of recomputation, and that
caches are isolated per model, so switching models mid-session starts a new cache from nothing.

## When It Applies

The practical consequence the second source draws is that the cost of a **cache miss scales with
context length**, which inverts some intuitions about saving money. Clearing a session and starting
fresh feels cheaper but discards the cached prefix — which that post puts at roughly 50,000 tokens of
system prompt, tool definitions and project configuration for Claude Code — and pays full price to
rebuild it. On the same reasoning, a very large context window is not free even when priced the same
per token as a smaller one: a missed 1M-token cache is a far larger bill than a missed 200K one. The
post's recommendation follows directly: continue an active session while the cache is warm, and treat
starting a new one as a conditional move for when the task has changed, the cache has expired, or the
context has filled with material irrelevant to the work at hand.

How well established this is differs between the two halves. That an unchanged prefix is billed more
cheaply is a documented provider behaviour both sources treat as given. The specific figures — the
tenfold ratio, the one-hour and five-minute windows, the 50,000-token floor — come from a single
practitioner post relaying vendor statements and community reports rather than from a measurement it
performed, and the post itself notes the vendor was still investigating the consumption behaviour
users were reporting.

A third source shows the same mechanism failing from the other direction, where the cache misses
are a symptom rather than a cost decision.
[[BlogPosting/update-on-recent-claude-code-quality-reports]] describes an optimization in
[[SoftwareApplication/claude-code]] that was meant to exploit an eviction that had already
happened: a session idle for more than an hour would be a cache miss anyway, so clearing old
thinking from it once would cut the uncached tokens sent on resume. A bug made it clear that
history on every turn for the rest of the session instead, and because each request then dropped
thinking blocks that the previous one had contained, the prefix kept changing and the requests kept
missing. Anthropic gives that as its best explanation for separate user reports that usage limits
were draining faster than expected.

What this adds to the picture above is that prefix stability is not only a billing optimization a
harness chooses to pursue — it is a property that other changes can silently break. The prefix-only
exact matching described above is what turns a per-turn modification of earlier content into a
per-turn full-price rebuild, and the cost is invisible in the way a latency regression is not: the
agent kept working, and what users noticed first was consumption.

## Related Terms

[[DefinedTerm/chat-templated-prompt]], [[DefinedTerm/compaction]], [[DefinedTerm/context-rot]],
[[DefinedTerm/context-reset]], [[DefinedTerm/sub-agent-architecture]]
