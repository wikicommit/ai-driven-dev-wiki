---
title: "everything-claude-code"
type: "schema:SoftwareApplication"
lang: en
tags: [harness-engineering, claude-code, agent-config, multi-agent]
sources:
  - type: url
    url: 'https://qiita.com/nogataka/items/d1b3fcf355c630cd7fc8'
    hash: sha256:3fd5e6d04c8d269d9f789b575d8917216722eb38a320372721e33c225935ddf3
  - type: url
    url: 'https://velog.io/@sammy0329/Claude-Code%EB%A5%BC-200-%ED%99%9C%EC%9A%A9%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-spec-kit-Everything-Claude-Code-Oh-My-ClaudeCode-%EC%99%84%EB%B2%BD-%EA%B0%80%EC%9D%B4%EB%93%9C'
    hash: sha256:72acff284adbf85c43f84d89f0d728dc7b8061e0e89dd2aac0bbb415897290e6
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A GitHub repository for Claude Code that describes itself as an \"agent harness performance optimization system\", bundling rules, skills, specialist agents, hooks, contexts and tests into one executable setup."
  featureList: "Language-specific rules; 125+ skills; 28 specialist agents; 25+ hooks with minimal/standard/strict modes; persistent contexts; test suite"
---

everything-claude-code (ECC) is a repository on GitHub that describes itself as an "agent
harness performance optimization system". It was published as open source by Affaan Mustafa, whose
project zenith.chat — built, according to a February 2026 Korean guide, entirely with Claude Code — won
an Anthropic x Forum Ventures hackathon in September 2025; the guide says the repository collects
settings refined over more than ten months of real use, and likens it to an operating system for
Claude Code rather than a collection of configuration files. A Qiita article on [[DefinedTerm/harness-engineering]],
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

The Korean guide, from February 2026, describes the same repository from its plugin
install and its two companion guides. Its organising idea is to use Claude not as a coding tool but as
a virtual development team: the main session acts as project manager and delegates detailed work to
role-specific sub-agents. At the time of that post the `agents/` directory held 12 agents (planner,
architect, TDD guide, code reviewer, security reviewer, build-error resolver, an E2E runner using
Playwright, refactor cleaner, documentation updater, and a Go code reviewer and Go build resolver). Each agent is defined
with YAML frontmatter naming its tools and model, and the stated design principle is to keep each
agent's tools to a minimum to sharpen its focus and avoid role conflicts between agents — the planner,
for example, gets only Read, Grep and Glob. Slash commands such as `/plan`, `/tdd`, `/code-review`,
`/build-fix`, `/e2e` and `/learn` (which extracts patterns from a session and saves them as a skill)
drive the development routine; everything under `rules/` is inserted into Claude Code's system prompt
and always applies; and the hooks the guide shows block a `console.log` left in an edited TS/JS file,
block the creation of unnecessary `.md`/`.txt` files other than README and `CLAUDE.md`, and run
Prettier after edits. The author's Shortform Guide covers setup, basics and philosophy; the Longform
Guide covers token optimisation, memory persistence across sessions, continuous learning, verification
loops and parallelisation with [[DefinedTerm/git-worktrees]].

Three design patterns are singled out by the Qiita article:

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

ECC is built around [[SoftwareApplication/claude-code]], and the Qiita article treats it as an external plugin.
The Korean guide installs it through Claude Code's plugin marketplace, and notes that the rules are not
deployed by the plugin and have to be copied into the user's rules directory by hand. That guide also
passes on a warning against turning on every MCP server at once — a 200K-token context window can shrink
to 70K — with the guideline of 20–30 configured MCP servers, no more than 10 enabled per project and no
more than 80 active tools, and the advice to wrap CLIs as skills in place of MCP servers. It recommends
ECC where production-level quality matters, for its enforced TDD, code-review guardrails and security
rules, names a steep learning curve as its limitation, and compares it with
[[SoftwareApplication/oh-my-claudecode]], which orchestrates agents automatically where ECC leaves the
judgment to the user. The Qiita article cautions against
adopting a complete setup of this kind on the first day — a flood of hooks slows the agent and managing
the configuration crowds out development — and recommends adding components as problems appear. It
expects functions that external plugins such as ECC currently provide to be absorbed into agent tools
themselves, and points to the repository's popularity as a sign that good harness design is becoming
shared community knowledge.
