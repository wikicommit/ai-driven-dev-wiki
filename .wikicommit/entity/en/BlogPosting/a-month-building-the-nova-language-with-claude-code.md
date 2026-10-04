---
title: "Месяц пишу язык программирования Nova с Claude Code. Где ломаются автономные агенты"
type: "schema:BlogPosting"
lang: en
tags: [autonomous-agents, multi-agent, practitioner-report, agent-failure-modes]
sources:
  - type: url
    url: 'https://habr.com/ru/articles/1043394/'
    hash: sha256:b1c46bd96d1f67f65b893293dc56fd1234cea6e9556c6d7a1ddf949fa4f378d7
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A Russian-language Habr case study on a month of building the Nova programming language with autonomous Claude Code agents working from human-reviewed plans, classifying four recurring ways the agents failed and the process discipline the author uses to catch them."
  author: ["Evgeny Golovin (unitcraft)"]
---

This post is a first-person case study by the author of [[ComputerLanguage/nova-programming-language]], who spent a month building the language and its compiler with [[SoftwareApplication/claude-code]] agents. The author reports a working compiler, about two thousand passing language tests and nearly three hundred engineering plans closed by agents with minimal involvement from the author. The working scheme is that the author and the agents think through a plan for a new feature together and polish it over several iterations, the agents then execute it autonomously, and the author checks the result.

The author presents the post as being about a methodology for building serious things with autonomous agents, with Nova as the test case, and contrasts it with articles showing a to-do app built in an hour. Its core is a classification of four failure modes that recurred over the month, each illustrated with a case from the project, followed by the practices the author relies on.

## Key Points

- Each plan is a structured markdown document of 500–2000 lines stating what is being done, the acceptance criteria and which tests must pass; the agent works from it, and the author reviews the result against those criteria. A plan typically takes from half an hour to several hours of agent work and about ten minutes of the author's review; the author runs many agents in parallel and describes the result as a conveyor, at about eight to ten closed plans a day.
- Failure 1, confident hallucination: an agent implemented variadic parameters in only one of the compiler's two execution paths (C code generation, not the interpreter), saw green tests and declared the plan done. Tests do not catch this because the agent believes it has checked everything. The author added a separate audit by another agent with a different system prompt acting as critic, which on a plan about Nova's SMT-checked contracts found three critical correctness holes.
- The author's observation is that AI catches local errors well, while systemic assumptions that tests silently rely on slip through, and that catching them needs a separate pass from a different angle — ideally a different model, or at least a very different prompt.
- Failure 2, defending a past position: an agent defended for weeks a design it had proposed earlier (opt-in cycle collection for real-time guarantees), conceding only after sustained pushback. The lesson drawn is that an explicit devil's advocate is needed — later delegated to a separate agent that must look for weaknesses — together with principles fixed in advance that give a reference point in an argument with the agent.
- Failure 3, beyond the familiar: a task that resembles a typical one has a non-standard detail the agent misses. In the case described, generated C function names collided with old `#define` aliases kept for compatibility. The author fixed it in the code generator itself, arguing that a rule enforced in code beats a "remember to check" item in a plan template, which an agent will eventually forget.
- Failure 4, echo chamber: an early builder–reviewer pair sharing the same context and system-prompt examples systematically approved the builder's errors. The scheme grew to several reviewers added one at a time — a fact-checker that verifies claims against the repository, a style reviewer, and two attacking agents (a general one and one focused on memory, resource leaks and race conditions). Any reviewer's flag sends the artefact to the author, who also randomly audits about 5–7% of automatically accepted operations a week. The author says the number four is incidental; what matters is that the angles really differ.
- Practices that work for the author: the plan as a contract with checkable acceptance criteria; one git worktree per task so agents cannot disturb each other's work (see [[DefinedTerm/git-worktrees]]); the audit pass after a plan closes; prompts and agent rules versioned in git and reviewed like code; a hard zero-regression gate; and escalation to a human by threshold, with higher-stakes decisions going higher.
- The author reports spending about twenty thousand roubles on Claude Code for the month, and estimates — conservatively, by the author's own reckoning — that the same three hundred plans would have taken one engineer 1200–1800 hours.
- The author keeps strategic reversals, project principles and crisis decisions outside the rules for the human, estimating them at five to seven percent of the work but nearly all of the risk.

## Context

All figures in the post come from the author's own project and estimates. The author ends with two scenarios for the following year: either this methodology — plan as contract, an audit cycle and threshold-based escalation to a human — becomes an industry norm as code review and CI/CD did, or current agents turn out to be a local maximum.
