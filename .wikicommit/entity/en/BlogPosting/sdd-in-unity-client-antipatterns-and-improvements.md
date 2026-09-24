---
title: "Unityクライアント環境におけるSDD活用事例 ── アンチパターンとその改善"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, context-window, agents]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62404/'
    hash: sha256:d49efd9233d456d1b205c748e19560ccabe3dc107352ab0e2e2f6f98094dd5ca
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Unity engineer's comparison of two attempts to hand the development of internal Unity client infrastructure to AI agents through spec-driven development: one that fell into a context-bloat anti-pattern, and a second that fixed it with split specs, minimal resident context, multi-model orchestration, deterministic quality gates and an isolated environment."
  author: ["Shinji Oikawa"]
  publisher: "[[Organization/cyberagent]]"
---

This post, on the developers' blog of [[Organization/cyberagent]], is by a Unity engineer at the group company GOODROID who works on the company's shared infrastructure and on promoting AI use. It describes moving the coding of two internal Unity client infrastructure libraries to [[DefinedTerm/spec-driven-development]] with AI coding agents, to the point that humans wrote no code, and compares the first attempt, which ran into an anti-pattern, with the second, which the author set up to fix it.

The workflow was based on [[SoftwareApplication/cc-sdd]]: humans drafted requirements, design and task documents with AI, and agents implemented against them. The author chose infrastructure code for the trial because it was largely written by one person, avoiding team-coordination costs, and because existing code and experience made accurate specifications likely.

## Key Points

- The first attempt, on a screen-transition library of 31 files and 4,040 lines, used a single large spec: `design.md` alone was 256KB and 5,200 lines. Measured with Claude Code's `/context`, the three spec documents took 73% of the standard context window, and close to 90% counting the space reserved for auto-compaction, so compaction ran frequently once implementation started.
- The author had extended the spec-implementation command to 17 steps, from bot authentication through self-review, testing, a pull request, waiting for human review over MCP, and merge. Under frequent compaction the agent skipped steps — skipping test runs, declaring completion partway — and each fix added more rules and memory, which made things worse: the post calls this a [[DefinedTerm/context-bloat-loop]].
- The post lists four further problems from the first attempt: long human idle time while one large spec was implemented; token consumption that hit contractual limits and capped how many work lines could run in parallel; test execution becoming probabilistic as the workflow grew, so that pull requests were merged with tests not passing; and work stopping on permission prompts under strict permission settings, which worsened as parallelism rose.
- The second attempt, on a data library of 92 files and 8,145 lines, split the work into 21 specs along technical boundaries. Average spec documents were 977, 331 and 228 lines, so a full spec set took about 17% of the context window.
- It kept resident context minimal: CLAUDE.md, memory and rules hold only about 30 lines of primary rules, with workflow detail moved into playbooks read on demand, and hooks used to keep the primary rules from being ignored.
- It ran Claude Code as the main agent and Codex as a sub-agent across providers, a [[DefinedTerm/multi-model-orchestration]] that the author reports raised token efficiency for implementation.
- It replaced agent-run testing with a [[DefinedTerm/deterministic-quality-gate]]: tests fixed with humans at design time and run in full by a `SubagentStop` hook and a GitHub Action before merge, which removed the need to confirm test passes in review.
- It ran agents without permission prompts ("YOLO environment") inside a self-built two-container Docker setup — a sandbox with no outbound access and a gateway that proxies a minimal allowlist of domains through Squid — with dedicated least-privilege accounts, built-in web search and fetch disabled, and search offered only through vetted MCP servers and proxies. The author built it rather than use existing isolated environments because they did not support the multi-model setup or the desired traffic restrictions.
- The new bottleneck was human review: 790 pull requests in a month, of which 426 were reviewed and handled by hand, which the author says was manageable only because of favourable conditions (one person, existing code, clear requirements).
- The author's conclusions: spec granularity matters most; quality assurance should be deterministic; resident context should be minimal; multi-model setups are an effective way to raise throughput; and a YOLO environment is a basis for maximizing permissions safely.

## Context

The account is one engineer's experience on two single-developer infrastructure libraries, and the post's figures (context-window shares, pull-request counts) are the author's own measurements; the author notes some effects, such as the drop in the rate of hands-off workflow completion, were judged by feel rather than measured. The author also flags that building an isolated Docker environment is an unfamiliar skill for Unity engineers, which may make it hard to roll out across a team.
