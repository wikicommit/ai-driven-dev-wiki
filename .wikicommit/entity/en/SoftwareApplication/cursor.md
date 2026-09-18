---
title: "Cursor"
type: "schema:SoftwareApplication"
lang: en
tags: [ai-assisted-programming, coding-tools]
sources:
  - type: url
    url: https://simonwillison.net/2025/Mar/19/vibe-coding/
    hash: sha256:653ba52b66ad62da601ae6fd257897841726d7ac6a07029edc6d0e1c5b12188f
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
  - type: url
    url: 'https://arxiv.org/pdf/2606.12231'
    hash: sha256:08aa95b018a1374f9de491d626d4f394b8efec41d830ef1726a1b8db6a69d9d6
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A popular tool for building software with an LLM, initially intended for professional developers and carrying far fewer safety rails than sandboxed alternatives. Published by Anysphere, it is also studied as an AI IDE, with project-specific rules kept under .cursor/rules/."
  applicationCategory: "AI IDE (per the 2026 rule-taxonomy study); IDE Assistant (per the 2025 agentic-programming survey)"
  author: "Anysphere"
---

Cursor appears in [[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] as a popular tool
used for [[DefinedTerm/vibe-coding]] that was not originally designed for it. Simon Willison notes
that it was initially intended for professional developers, and treats that origin as the
explanation for how little it constrains what generated code can do.

A survey on AI agentic programming, [[ScholarlyArticle/ai-agentic-programming-survey]], describes
Cursor as extending IDE-assistant functionality with conversational interaction, memory of previous
edits, and structured command execution. Elsewhere in its comparative analysis, the same survey
reports Cursor's underlying model as Claude 3.5 Sonnet or GPT-4, with a 128,000-token default
context window and persistent memory implemented as semantic search over project history, and
classifies Cursor, in its own taxonomy, as an IDE Assistant that is reactive and tool-using but not
multi-turn or adaptive.

## Capabilities

The post's one direct characterisation is comparative: Cursor has far less in the way of safety
rails than [[SoftwareApplication/claude-artifacts]], whose sandbox prevents unreviewed code from
reaching the network or from causing harm outside the project.

Karpathy's account of vibe coding, quoted in the same post, names Cursor Composer driven by a
Sonnet model as the setup he was working in, and describes talking to it by voice rather than
typing. That is his description of his own workflow at the time rather than a statement about what
the product generally offers.

A later post on long-running agents describes Cursor as also shipping background cloud agents: long-running tasks that run on Anysphere's cloud infrastructure rather than the developer's own laptop, so an eight-hour refactor or a codebase-wide migration survives a closed lid. A task can be started locally, sent to run in the cloud once it looks like it will take longer, and re-attached to later from another device; each background agent runs in its own isolated git worktree and merges its result back via pull request (see [[DefinedTerm/git-worktrees]]). The same post names Composer 2, described as Cursor's proprietary frontier coding model, which ships in Cursor 3.

That post also describes the coordination system behind Cursor's production long-running agents: a Planner/Worker/Judge role split reached after two earlier coordination designs (equal-status agents sharing files with locks, then optimistic concurrency control) each ran into bottlenecks or coordination failures (see [[DefinedTerm/planner-worker-model]]). It reports that a GPT model outperformed Opus specifically for extended autonomous work, because Opus tended to stop early and take shortcuts — different models suited to different roles in the same system.

[[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] treats Cursor as an
[[DefinedTerm/ai-ide]] — an editor built with AI as a core architectural component rather than a plugin
over an existing one — and as one of five such tools that let developers define
[[DefinedTerm/ai-ide-rules]]. Cursor's rule files live under `.cursor/rules/`; that study also lists a
legacy `.cursorrules` format among Cursor's rule-file locations, noting that such legacy formats were
later superseded by the directory-based mechanism. That study records
Cursor's release date as 6 April 2023, noting that the date corresponds to the version in which it
transitioned to its VS Code-based architecture.

## Adoption & Ecosystem

Willison groups Cursor with other popular vibe coding tools, which places a tool built for
professionals among the ones newcomers reach for. The safety concern he raises follows from exactly
that mismatch: the conditions he sets out for vibe coding — low stakes, care with secrets and
private data, hard billing limits — have to be met by the person rather than by the tool when the
tool does not enforce them.

In the rule-taxonomy study's practitioner survey, Cursor was the most widely adopted AI IDE among its
99 respondents, named by 57 — closely followed by the VS Code plus Copilot setup at 51, which that
study counts as a plugin arrangement rather than an AI IDE. On the mining side, Cursor also accounted
for the largest share of that study's project dataset: 46 of the 83 projects it analysed, drawn from an
initial 18,790 candidates before keyword, rule-file and manual filtering.
