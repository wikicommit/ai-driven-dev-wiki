---
title: "Claude CodeのSkillsでハーネスエンジニアリングを実装した — ルール自動生成でコード品質を継続改善する"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, agent-skills, claude-code-configuration, agent-hooks]
sources:
  - type: url
    url: 'https://zenn.dev/shintaroamaike/articles/df3ecc0ddee047'
    hash: sha256:ed1e00178a0ca382854e79709eae5586c0b71d612ff7e82aac0e1c75dff42146
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "The author introduces AutoHarness, a set of Claude Code skills that generate and then keep revising a project's coding rules and a verification script, reports a small self-reported trial, and in a June 2026 revision recasts CLAUDE.md as the describe layer and hooks as the enforce layer."
  author: "ShintaroAmaike"
  datePublished: "2026-04-01"
---

This post starts from an observation about [[DefinedTerm/claude-md]]: [[SoftwareApplication/claude-code]] follows the rules written there, but someone still has to write them, and turning a team's tacit conventions into complete, maintained prose is costly. The author's answer is [[SoftwareApplication/autoharness-skill]], a set of Claude Code skills that analyse a project to generate its rules and a verification script, and then revise both when violations or feedback occur. The post explains the skills, reports a small trial of their effect, and positions the work as an instance of [[DefinedTerm/harness-engineering]].

The skills borrow their idea from Google DeepMind's AutoHarness paper, which the author summarises as automatically generating a harness that rejects an LLM agent's illegal moves. The author is explicit that only the inspiration — define illegal actions and exclude them — is borrowed, and that the paper's optimisation algorithm is fundamentally different from what the skills do. The post was revised in June 2026 to reflect changes in Claude Code, while the trial's figures were kept from the original April version.

## Key Points

- The skills map onto the paper's concepts loosely: the verification rules in the generated check script stand in for the paper's legality check, but are managed by hand rather than generated and optimised; the refinement loop is the update skill, run manually or, after the revision, through a PostToolUse hook.
- In a trial with three tasks on a shift-management codebase, each run five times with and without the harness (thirty agent runs in all), the author reports that conventions written in the harness file but not in the task instructions were followed in every run with the harness. Without it, the gap was largest for `pathlib.Path` and `Decimal` on the feature-addition and bug-fix tasks (0 of 5 runs each) and for type annotations on the bug-fix task (1 of 5); type annotations on the feature-addition task (3 of 5) and both type annotations and `pathlib` on the extension task (4 of 5, which the author calls a slight difference) showed smaller gaps.
- Functional outcomes differed little: bug-fix rates on the bug-fixing task and the CSV/JSON export and constraint handling on the extension task were about the same with and without the harness, which the author reads as rules mattering where they encode conventions rather than where the goal is already explicit.
- Average test counts were higher with the harness, which the author attributes to the harness file stating test requirements.
- The author calls the trial a reference only: n=5 per condition has no statistical significance, and most metrics, including estimated lint and type errors, were scored by the agents themselves rather than by running linters or mypy.
- The author interprets the convention differences as the agent following rules because they were in the prompt, not because the harness enforced them.
- The June 2026 revision adopts a distinction the author describes as having become common: `CLAUDE.md` and the harness rule file are a describe layer that the agent usually follows but can drop under long sessions or competing priorities, while [[DefinedTerm/agent-hooks]] are an enforce layer that runs outside the model's reasoning and cannot be forgotten or bypassed.
- Wiring the verification script to a PostToolUse hook on edits and writes, the author argues, returns lint and type-check results to the agent in the same turn, reproducing the paper's run, feedback and fix loop in outline though not its optimisation search. The suggested split is rule content in the rule file, checks that must hold in a hook.
- The revision also records that `CLAUDE.md` `@` imports are now documented officially and that slash commands and skills have been unified, so a skill file now also works as a slash command.
- On cost, the author notes that a rule file loaded into every session consumes tokens, and points to the guidance of keeping only project-wide rules in `CLAUDE.md` and moving workflow-specific rules into skills loaded on demand.

## Context

A column in the post compares the approach with how Claude Code's creator, Boris Cherny, is reported to use `CLAUDE.md`: teams at Anthropic keep a `CLAUDE.md` in Git, add lessons from mistakes and pull-request reviews to it, and keep it to around 2,500 tokens. The author presents the skills as semi-automating that practice, while noting the contrast that Cherny is reported to customise Claude Code very little. The author states the skills' limits plainly — rules can go stale when the stack changes, nothing happens until the initial setup is run — and names a re-evaluation with real linters and mypy wired through a PostToolUse hook, and automatic optimisation closer to the paper, as future work.
