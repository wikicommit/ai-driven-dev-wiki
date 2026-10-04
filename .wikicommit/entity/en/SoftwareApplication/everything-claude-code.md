---
title: "everything-claude-code"
type: "schema:SoftwareApplication"
lang: en
tags: [harness-engineering, claude-code, agent-config]
sources:
  - type: url
    url: 'https://qiita.com/nogataka/items/d1b3fcf355c630cd7fc8'
    hash: sha256:3fd5e6d04c8d269d9f789b575d8917216722eb38a320372721e33c225935ddf3
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A GitHub repository for Claude Code that describes itself as an \"agent harness performance optimization system\", bundling rules, skills, specialist agents, hooks, contexts and tests into one executable setup."
  featureList: "Language-specific rules; 125+ skills; 28 specialist agents; 25+ hooks with minimal/standard/strict modes; persistent contexts; test suite"
---

everything-claude-code (ECC) is a repository on GitHub that describes itself as an "agent
harness performance optimization system". A Qiita article on [[DefinedTerm/harness-engineering]],
[[BlogPosting/introduction-to-harness-engineering]], calls it the culmination of harness design and
reads it as more than a collection of [[DefinedTerm/claude-md]] templates: an executable system that
covers all five components the article assigns to a harness — rules, skills, hooks, memory and a
feedback loop.

## Capabilities

The article maps the repository's layout onto those components. Rules live in `CLAUDE.md`, an
[[DefinedTerm/agents-md]] defining the roles of 28 agents, and a `rules/` directory with
language-specific constraints (TypeScript, Python, Rust and a common set). Skills are a `skills/`
directory of more than 125 workflow definitions as of 23 March 2026 — among them TDD, deep research,
security review and continuous learning — alongside an `agents/` directory of 28 specialist agent
definitions such as a planner, a code reviewer and a TDD guide. Hooks are defined in `hooks/hooks.json`
(more than 25 event triggers), memory in a `contexts/` directory of session-persistent contexts for
development, research and review, and the feedback loop in a `tests/` verification suite.

Three design patterns are singled out:

- **Layered hooks.** Before a tool runs, hooks block bypassing git hooks with `--no-verify`, block
  changes to linter configuration (preventing rules from being weakened), run security monitoring and
  check MCP server health; after a tool runs, they format, type-check, warn about leftover `console.log`
  calls and run quality-gate checks; when a task stops, they persist session state, extract learned
  patterns and record token cost. What the article finds distinctive is hooks that block an agent's
  attempts to get around the rules, rather than only formatting after edits.
- **Self-optimization.** A `harness-optimizer` agent analyses the harness's own configuration and
  proposes improvements, and a `continuous-learning` skill extracts patterns from each session to keep
  updating the harness's knowledge base.
- **Graduated strength.** Hooks run in one of three modes — `minimal`, `standard` and `strict` — so
  enforcement can be matched to a project's maturity rather than every hook being active all the time.

## Adoption & Ecosystem

ECC is built around [[SoftwareApplication/claude-code]], and the article treats it as an external plugin. The same article cautions against
adopting a complete setup of this kind on the first day — a flood of hooks slows the agent and managing
the configuration crowds out development — and recommends adding components as problems appear. It
expects functions that external plugins such as ECC currently provide to be absorbed into agent tools
themselves, and points to the repository's popularity as a sign that good harness design is becoming
shared community knowledge.
