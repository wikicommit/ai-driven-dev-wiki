---
title: "Agentic SDLC Spec Kit"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, spec-driven-development, cli, open-source]
sources:
  - type: url
    url: 'https://github.com/tikalk/agentic-sdlc-spec-kit'
    hash: sha256:670bd390efe2da74f5244436ac5e4c1d9a95dd3d805fa2899166e4b754fc3fcb
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An opinionated fork of GitHub Spec Kit that layers the Agentic SDLC 12 Factors methodology over the spec-driven development process, adds a version-controlled team knowledge base, and ships its own extensions, presets and workflow automation. It is installed as the agentic-sdlc-specify-cli from the fork's own repository under agentic-sdlc-v* release tags."
  applicationCategory: "Spec-driven AI development toolkit"
  operatingSystem: "Linux, macOS, Windows"
  featureList: "Team AI Directives knowledge base synced across projects; levelup command producing reusable Context Directive Records; bundled architect, product, tdd, evals, git and workflow extensions; stackable agentic-sdlc / agentic-change / agentic-quick presets; DAG-aware wave-based task orchestration; SYNC/ASYNC dual execution loop; feature-level git worktree isolation with task branches; role-based bundles"
  author: "[[Organization/tikal]]"
---

Agentic SDLC Spec Kit is a fork of [[SoftwareApplication/github-spec-kit]] maintained by the Tikal
engineering team. Its stated vision is to combine the Agentic SDLC 12 Factors methodology with
[[DefinedTerm/spec-driven-development]]: the fork presents the 12 Factors as a strategic layer
sitting above the tactical SDD process, describing them as philosophical and strategic principles
for building software with AI coding agents that cover matters such as strategic mindset, context
scaffolding, dual execution loops and team capability, while SDD supplies the concrete
specification, planning, task-breakdown and implementation phases.

The fork describes the upstream repository as having focused on the core spec-driven development
process, and positions itself as extending that foundation into a complete, opinionated platform
for AI-native development — the project's own words for a shift from a development process to an
organizational methodology. It is published under the MIT license and installed as
`agentic-sdlc-specify-cli` from the fork's own repository, under release tags carrying an
`agentic-sdlc-v` prefix; `specify self check` and `specify self upgrade` are repointed to the fork
accordingly. Prerequisites are Linux, macOS or Windows, a supported AI coding agent, Python 3.11 or
later, Git, and `uv` or `pipx` for installation.

## Capabilities

The fork groups its additions under a strategic layer, CLI add-ons, bundled extensions, bundled
presets and execution enhancements. The strategic layer comes first: alongside
the 12 Factors, a `team-ai-directives` knowledge base of rules, personas, examples and skills is
version-controlled and synced across projects, wired in at project creation through a
`--team-ai-directives` flag that accepts a local directory, a GitHub or GitLab archive URL, or a
direct archive URL. A `levelup` command turns finished sessions into reusable Context Directive
Records that contribute back to that knowledge base, which the project describes as closing a
cross-project learning loop. Private knowledge bases are reached through a provider configuration
file naming hosts and the environment variable holding the token.

Next is a set of bundled extensions beyond core SDD: `architect` for architecture impact
analysis and decision records, `product` for product thinking and user-story refinement, `tdd` for
test-driven workflows, `evals` for evaluation-driven development, `git` for branch or worktree
automation, `levelup` for session knowledge management, and `workflow` for mission-driven SDLC
automation with supervision modes and safety guardrails.

Then bundled presets — stackable customizations of how the toolkit behaves rather than what
it can do. `agentic-sdlc` covers the full lifecycle of specify, plan, tasks, implement and converge
and is pre-installed, as is `agentic-quick` for session-based ad-hoc execution; `agentic-change`, a
lightweight change-proposal workflow, is opt-in. The distinction the project draws between the two
customization systems is that extensions add new capabilities while presets override the templates
and commands that core and extensions already ship. Both resolve through the same priority stack —
project-local overrides, then presets, then extensions, then core defaults — but at different
moments: templates are resolved at runtime, the stack walked top-down and the first match used,
while extension and preset commands are applied at install time, written into the agent's command
directories by `specify extension add` or `specify preset add`, with the highest-priority version
winning and the next-highest restored automatically on removal.
Bundles sit above both, packaging a curated, version-pinned set of extensions, presets, steps and
workflows so that a whole team role can be provisioned in one command from a priority-ordered
catalog stack.

Last is execution: task orchestration is DAG-aware, generating a task graph for wave-based
parallel or sequential execution; a dual execution loop classifies each task as `[SYNC]` for
immediate or `[ASYNC]` for deferred handling; and each feature can be isolated in its own git
worktree with a task-branch workflow layered onto the upstream `git` extension.

These surface to the coding agent as several command namespaces. `/spec.*` runs the core lifecycle —
establishing project principles, optional brainstorming, specify, clarify, plan, tasks, analyze,
implement and converge, with `converge` assessing the codebase against the spec, plan and tasks and,
once converged, running a test gate, diff analysis and a four-pillar quality assessment.
`/change.*` and `/quick.*` are the lighter change-proposal and session-based routes, and
`/workflow.*` covers mission assessment, execution, resumption and persistence. Where an integration
supports skills mode, the same commands are installed as agent skills rather than slash-command
prompt files. The fork lists support for a range of coding agents including Claude Code, GitHub
Copilot, Cursor, Gemini CLI, opencode, Qwen, Codex, Windsurf and Junie, and points at an
integrations reference for the full set.

## Adoption & Ecosystem

The project is maintained by Tikal's engineering team and developed in the open on GitHub, with its
own documentation site and issue tracker; upstream problems are directed to the upstream repository
instead. Its acknowledgements state that the project is heavily influenced by and based on John Lam's work
and research and on the original Spec Kit project.
