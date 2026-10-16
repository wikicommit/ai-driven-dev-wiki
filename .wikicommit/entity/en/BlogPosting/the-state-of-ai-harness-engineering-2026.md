---
title: "The State Of AI Harness Engineering 2026"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, coding-agents, agent-harness, empirical-survey]
sources:
  - type: url
    url: 'https://marmelab.com/blog/2026/09/24/the-state-of-ai-harness-engineering-2026.html'
    hash: sha256:6b235f9874e2acd25e233753bd07b55e930baaa9faa7e3f929bdd45c29e53e5c
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "A Marmelab survey of what practitioners actually do in harness engineering for coding agents, built from an audit of open-source repositories and a reading of 57 publications, which finds that most projects write agent instructions but few enforce, test or measure them, and distils a set of practices and failed approaches."
  author: ["François Zaninotto"]
  datePublished: "2026-09-24"
  publisher: "Marmelab"
---

The post asks what people are actually doing in [[DefinedTerm/harness-engineering]] — which it
glosses as building the tools, context, memory and control loops that make an agent reliable — and
how well it is working. To find out, Marmelab audited 246 open-source repositories that either
describe themselves as harnesses or contain one, cloning each to read its real first commit date,
last activity and the number of files it versions under `.claude/`. Because self-described harness
repositories are a biased sample, it ran a counter-test on 145 large open-source projects unrelated to
AI, inspected the same way. From the combined set it kept 97 harnesses large enough to test, then
filtered out those that do not test their harness, iterate on it too little, have a single author, or
lived too briefly, leaving 11 finalists. It also collected 57 publications on the subject, and says it
used AI to gather, rank and aggregate trends from them. The scope is limited to harnesses for software
development and coding agents.

The authors frame the field as young and fast-moving: in their account, the only consensus is about
*what* harness engineering is, not *how* to build a reliable harness, and because a harness encodes
assumptions about what the model cannot do on its own, practices that suited early-2026 models are
already ageing. The post discloses that Marmelab builds harnesses itself and is the author of
[[SoftwareApplication/atomic-crm]], one of the 11 finalists, and that the study was made to compare its
own practices against the field's best.

## Key Points

- In the post's repository audit, the median harness repository is 8.7 months old, and 83% of the
  harness repositories were created in 2025 or 2026.
- 63% of the 145 large non-AI projects ship an agent instruction file, but only 4 declare a subagent
  and there are 14 hooks in total across all 145, which the authors read as open source having
  adopted the documentation without yet constraining agents.
- Only 12 of the 391 repositories examined commit a single `deny` rule in their Claude Code settings,
  and 22 declare a `PreToolUse` hook; in the median repository that uses subagents, only 1 in 4
  subagents has a restricted tool list.
- 189 repositories have an [[DefinedTerm/agents-md]] file at the root against 155 with a
  [[DefinedTerm/claude-md]] file, and in the large projects 36 of the 53 `CLAUDE.md` files are a
  symlink or short redirect to `AGENTS.md`; 46% of the repositories write instructions for at least
  two different agents.
- Of the 97 harnesses large enough to test, 60% have neither a test nor an eval, 21% test themselves,
  27% version evals and only 7 do both.
- At least 25% of the commits that touched a harness since January 2025 are explicitly signed by an
  AI, which the authors call a floor; in 52 of 79 repositories the harness is more AI-written than the
  code it governs.
- The post recommends testing a harness's scripts and rules with code — each rule twice, once where it
  must fire and once where it must not — and evaluating the harness end to end on a frozen set of
  tasks, changing one part at a time.
- It recommends building the harness in reaction to observed agent failures rather than assumptions,
  and keeping rules and the set of visible tools small; that a human rather than an agent should build
  the harness is labelled as the authors' opinion, not a finding, and they note that the one ablation
  study they found points the other way.
- It recommends doubling or replacing prose rules with executable guards — git hooks, linter rules,
  static analysis and custom scripts — that run both where the harness runs and in CI.
- It recommends letting the agent start its own instances of the app, drive it in a real browser and
  read its logs, then turning a successful check into a script that needs no LLM to run.
- Only 5 of the 391 repositories record anything about how their harness is used, and the post
  recommends observability over real sessions in addition to evals.
- It recommends treating the harness like a garden — giving each control an expiry condition and a
  record of the incident it exists for, and pruning stale rules — and admits that Atomic CRM itself
  ships 148 harness files with no recorded decisions.
- From the literature it lists approaches it found not to work: adding a reviewer agent, chains of more
  than four agent-to-agent handovers, writing permission rules in advance instead of approving each
  action, and blocking merges on every check at high throughput; it judges looping to work but the
  fresh-context variant of the [[DefinedTerm/ralph-loop]] to be unproven.

## Context

The post is explicit about the limits of its own evidence. It says the only thing it found properly
measured is that the same model run through different harnesses on the same tasks reached different
success rates, and that every strong measurement it quotes scores an autonomous coding agent on a public
benchmark, whereas a harness like Atomic CRM governs a process on a task it does not control — a link it
calls an analogy rather than a measurement. It treats some quoted figures as directionally solid but
unverified in magnitude, and notes where Atomic CRM's own practice departs from what it recommends, such
as keeping a reviewer role and requiring human review for every pull request. It also cites
[[BlogPosting/harness-engineering-for-coding-agent-users]] as the source of the formula
*Agent = Model + Harness*.
