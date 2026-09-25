---
title: "Claude Code Swarms"
type: "schema:BlogPosting"
lang: en
tags: [multi-agent, agentic-engineering]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/claude-code-agent-teams/'
    hash: sha256:b36f513e61d7ef1ac90ab862218ac5db53654893d583aba69626a3e5ac82e049
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A post introducing Claude Code's agent teams ('swarms'), explaining how a team lead coordinates independent teammates through a shared task list and direct messaging, where the pattern pays off, and its current rough edges."
  author: "Addy Osmani"
  datePublished: "2026-02-05"
---

This post announces and explains [[DefinedTerm/agent-teams]] in [[SoftwareApplication/claude-code]], a feature in research preview at the time of writing, in which a lead agent delegates to multiple teammates that work in parallel and coordinate with each other. It notes that the community had been calling these patterns "swarms", and that what began as developers discovering feature-flagged capabilities in Claude Code's binary and building workarounds with subagents and bash scripts had become a first-class feature.

The post frames agent teams as a fundamentally different architecture from the single-agent model, motivated by the observation that LLMs perform worse as context expands. It walks through setup, controls and task management, lists where the pattern works well and what to watch out for, and closes with a caution that activity does not always translate into value.

## Key Points

- The motivating failure mode is context degradation in a single agent on a complex task; the post's core claim is that the more information in the context window, the harder it is for the model to focus on what matters now, so giving each agent a narrow scope and clean context yields better reasoning within each domain.
- The approach only works when tasks are properly scoped: the post contrasts "Build me an app", which burns tokens, with implementing clearly defined API endpoints against a specification.
- Agent teams are distinguished from subagents: subagents report results back to a single parent and cannot talk to each other, while teammates message each other directly and coordinate through a shared task list, at a higher token cost because each teammate is a separate Claude instance.
- The post recommends subagents for quick, focused workers and agent teams when teammates need to share findings, challenge each other and coordinate on their own.
- Situations named as a good fit are competing hypotheses for debugging (teammates trying to disprove each other's theories to avoid anchoring), parallel code review through different lenses, cross-layer feature work, and research and exploration.
- The author argues that the skills of a strong engineering manager translate to agent orchestration: task sizing (the post suggests 5–6 tasks per teammate), file ownership to avoid overwrites, and loading task-specific context into the spawn prompt, since teammates do not inherit the lead's conversation history.
- Rough edges listed include the lead implementing instead of delegating, no session resumption for in-process teammates, lagging task status, one team per session with no nested teams, token costs that scale with teammates, split panes requiring tmux or iTerm2, permissions propagating from the lead, and slow shutdown.
- The post warns that multi-agent systems make it easy to produce large quantities of code quickly, and advises letting the problem guide the tooling: for sequential tasks, same-file edits or work with many dependencies, a single session or subagents are more effective.
- It suggests the [[SoftwareApplication/compound-engineering-plugin]] for a more structured workflow around agent teams.
- The author's closing argument is that the core skill is decomposing problems into structures agent teams can execute, with implementation increasingly becoming a matter of sufficiently precise specification.

## Context

The post presents itself as the author's practical guide and opinion, pointing to Claude Code's own documentation for the complete setup and usage guide. It connects agent teams to the author's earlier writing on the shift from conductor to orchestrator (see [[BlogPosting/future-of-agentic-coding-conductors-to-orchestrators]]) and on parallel agent workflows (see [[BlogPosting/your-ai-coding-agents-need-a-manager]]), and to his framing of [[DefinedTerm/agentic-engineering]].
