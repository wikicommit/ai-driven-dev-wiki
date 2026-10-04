---
title: "AutoHarness Skill"
type: "schema:SoftwareApplication"
lang: en
aliases: ["AutoHarness", "autoharness-skill"]
tags: [harness-engineering, agent-skills, claude-code-configuration]
sources:
  - type: url
    url: 'https://zenn.dev/shintaroamaike/articles/df3ecc0ddee047'
    hash: sha256:ed1e00178a0ca382854e79709eae5586c0b71d612ff7e82aac0e1c75dff42146
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A set of three Claude Code skills that analyse a project to generate natural-language coding rules and a verification script, and then revise them when rule violations or feedback occur."
  applicationCategory: "Claude Code skill"
---

AutoHarness is a set of skills for [[SoftwareApplication/claude-code]], published as an MIT-licensed repository by its author, that automates writing and maintaining the project rules a coding agent is meant to follow. Its premise is that while Claude Code will follow rules written in [[DefinedTerm/claude-md]], someone still has to write and maintain them, and the skills aim to generate them from the project itself and grow them as problems are found. The author describes it as an attempt at [[DefinedTerm/harness-engineering]], introduced in [[BlogPosting/implementing-harness-engineering-with-claude-code-skills]].

The name and idea come from Google DeepMind's AutoHarness paper, which the author summarises as automatically generating a harness that rejects an agent's illegal moves. The skills borrow only that inspiration — define what is not allowed and exclude it. In the author's mapping, the skills' verification rules correspond to the paper's legality check but are managed by hand rather than automatically generated and optimised.

## Capabilities

- `/autoharness-init` analyses the project's configuration (such as `pyproject.toml`, `tsconfig.json` or `.eslintrc`) and generates `.claude/rules/harness.md`, a natural-language rule file covering type annotations, naming and forbidden patterns, and `.claude/rules/harness_check.py`, a script that runs lint, type checks and tests and returns the results as JSON. It also adds an `@.claude/rules/harness.md` import to `CLAUDE.md` so the rules are loaded automatically.
- `/autoharness-update` analyses failures and updates both the rules and the verification script. The author states that it also runs without being typed, triggering when a code-generation task wraps up, when type errors or test failures occur, or when the user gives feedback about the output.
- Setup consists of copying the three skill directories from the repository into the project's `.claude/skills/`.
- The verification script can be run in CI, and the author's June 2026 revision recommends also connecting it to a PostToolUse hook on edits and writes, so that check results return to the agent in the same turn (see [[DefinedTerm/agent-hooks]]).

## Adoption & Ecosystem

The only evidence of effect given is the author's own small trial (five runs per condition, metrics largely self-reported by the agents), in which conventions written into the rule file were followed in every run with the skills, while without them `pathlib.Path` and `Decimal` went unused in all runs of the feature-addition and bug-fix tasks; on the extension task the gap was slight, and functional outcomes were similar across conditions. The author treats this as indicative only. Stated limitations are the token cost of loading the rule file in every session, rules going stale if the technology stack changes, and no effect until the initial setup has been run. Re-evaluating with real linters and mypy, and automatic optimisation closer to the paper's method, are named as future work.
