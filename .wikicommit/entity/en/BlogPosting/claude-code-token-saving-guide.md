---
title: "Claude Code 省 Token 指南：慎用 1M 上下文，不开新会话或者总是开新会话都不对"
type: "schema:BlogPosting"
lang: en
tags: [coding-tools, context-window, cost, prompt-caching]
sources:
  - type: url
    url: 'https://baoyu.io/blog/2026-04-06/claude-code-token-optimization'
    hash: sha256:287e81a37d9c6dc213f594b3dd3f401600e6fe71f7d49622f3492c33f13b0a75
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An argument that the reflex of clearing a Claude Code session to save quota usually costs more than continuing it, because a new session pays full price to rebuild a large fixed prefix that an active session holds in cache — and that the 1M context window makes a cache miss proportionally far more expensive."
  author: "宝玉"
  datePublished: "2026-04-06"
---

The post opens on a complaint it takes as given — that Claude Code quota is being consumed faster than users expect — and argues that the most common reaction to it is counterproductive. Reaching for `/clear`, or starting a fresh session after each step of work, feels like travelling light; the post's claim is that it usually triggers a full-price context rebuild costing more than continuing the conversation would have.

The argument rests entirely on how [[DefinedTerm/token-caching]] works. A model is stateless and re-reads its whole input every turn, so the post divides that input into a fixed part (system instructions, tool definitions, CLAUDE.md project rules), the conversation history, and the new message. In an active session the first two are unchanged, so they hit the cache; starting a new session discards the accumulated cache and pays to rebuild a prefix the post puts at roughly 50,000 tokens. Because caching matches only an unchanged prefix, and because cache reads cost about a tenth of recomputation, the post inverts the usual advice: continuing is the default and starting a new session is a conditional optimization.

Its second target is the 1M context window, which the post says is becoming a leading cause of exhausted quota — not because long context is billed at a premium (it says that premium was removed) but because the cost of a cache miss scales with context length, so an hour away from the keyboard turns a 1M-token session into a full rebuild.

## Key Points

- The post's central inversion: "continue while the cache is hot and the task has not changed; restart when the cache has expired, the task has switched, or the context is full of noise" — with continuing as the default habit rather than clearing.
- It gives caching two conditions: matching is prefix-only and exact, so changing anything early invalidates everything after it; and cached entries expire, on windows the post relays from the Claude Code team — one hour for the main agent, five minutes for subagents — with each hit refreshing the timer.
- It quotes the Claude Code team's own characterization that Claude Code is the framework with the highest cache utilization, and separately relays an Anthropic employee's advice that a large session idle for about an hour is worth restarting, noting that the keyword in it is *idle*.
- Three counterintuitive economies are argued: keeping extended thinking on to get a complex task right once is likely cheaper than three cheaper rounds of correction, because each round resends the whole context; conversely, lowering effort on simple tasks pays off immediately; and passing a file path beats pasting the file, since the cheapest token is one that never enters the context.
- On the 1M window the post reports that Anthropic removed the long-context price premium so 1M and 200K cost the same, that the team has acknowledged the cache-expiry problem and is considering lowering the default to 400K, and that most everyday sessions compact at 80–120K and never approach even 200K. Its own recommendation is to keep the window but set a conservative auto-compaction threshold, via `CLAUDE_CODE_AUTO_COMPACT_WINDOW`; `CLAUDE_CODE_DISABLE_1M_CONTEXT` is given for the opposite choice, turning the larger window off altogether.
- Its six operating rules: prefer Sonnet for routine work (the post puts Opus input cost at about 1.7× Sonnet's and its token consumption rate at roughly double); never switch models mid-session, since caches are per-model; keep CLAUDE.md within the official 200-line guidance and move situational instructions into skills; prefer a CLI such as `gh` over an MCP server, which injects full schemas at both ends; spend tokens on planning first; and use `permissions.deny` to keep the model out of `node_modules`, build output and large data files.
- On delegation it distinguishes subagents — independent context, returning only a summary, so detailed output never burdens later turns, at the cost of a five-minute cache window — from agent teams, where each member is a separate instance with its own context and, the post argues, plan-mode consumption runs to several times that of a standard session (it puts a roughly sevenfold figure on this as a community estimate), with idle members still consuming.
- It reports three official clarifications: that consumption accelerating past 256K of context is *not* true (the post attributes the perception to restarted idle sessions causing large cache misses), that the malware-check prompt present since Sonnet 3.7 was evaluated at each model release without causing regression and has been removed in Opus 4.6, and that adaptive thinking has been ruled out as a cause — alongside the team's statement that it is still investigating and has not blindly trusted its internal metrics.
- Several of the post's figures are relayed from community reports rather than measured by the author — the per-session cost computed by another user on Bedrock, the roughly sevenfold plan-mode estimate for agent teams, the claim that a third-party Codex plugin completes comparable tasks on about a third of the tokens, and the thresholds at which context length is said to degrade output.

## Context

The post is written for Claude Code users rather than as a general account of prompt caching, and its explanatory device — a researcher re-reading the same 500-page report on each library visit — is aimed at readers who have not thought about why a stateless model re-charges for unchanged input.

Its stated perspective in closing is that quota tightening is likely an industry trend rather than a vendor-specific one; the author relays others' description of the present moment as the end of an era of subsidized compute, and argues — this part in the author's own voice — that understanding the cost structure is a better use of effort than betting on whichever provider subsidizes longest. The post ends by asking readers how long their own sessions run, which places it as a discussion piece in an ongoing community argument rather than a settled reference.
