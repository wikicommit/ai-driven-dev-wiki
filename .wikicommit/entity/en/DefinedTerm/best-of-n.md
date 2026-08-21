---
title: "Best-of-N parallel strategy"
type: "schema:DefinedTerm"
lang: en
tags: [multi-agent, agentic-coding, git-worktree, terminology]
sources:
  - type: url
    url: 'https://nyosegawa.com/en/posts/coding-agent-workflow-2026/'
    hash: sha256:bb7d36388cc5d0dc91fc90185585f6fff68833b1b198e732c6e2d6d41a285f45
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Running the same task through N agents in parallel, each in its own isolated worktree, then picking the best of the N results or composing good parts of several — treating model nondeterminism as a feature rather than a defect."
  termCode: ""
  inDefinedTermSet: ""
---

The Best-of-N parallel strategy runs the *same* task through several agents at once — each working from the same spec and prompt in its own git worktree — and then either selects the best of the N implementations or composes good parts of several. [[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] describes it as using LLM nondeterminism as a feature rather than a bug, and distinguishes it explicitly from multi-agent division of labour, which runs *different* tasks in parallel.

## Usage

The arithmetic it offers is the argument. If a single agent has a 25% success rate on a task, four in parallel gives 68% — one minus 0.75 to the fourth — and eight gives 90%. API cost scales linearly with the degree of parallelism, but that post's assessment is that the absolute cost difference is negligible against the gain.

Its stated fit is problems with no single right answer: architectural decisions, algorithm selection, and UI design, where having several genuinely different attempts to compare is worth more than one attempt refined.

The failure case is task shape rather than agent quality. That survey relays an insight from a 16-agent parallel C-compiler project: when tests are independent the parallelism works naturally, but on a single large task — its example being compiling the whole Linux kernel — all the agents converge on the same bug and overwrite each other's changes. The mitigation it names is mutual exclusion through a text-file-based task lock.

## Related Terms

Best-of-N is the same-task counterpart to [[DefinedTerm/multi-agent-orchestration]]'s different-task split, and depends on the same worktree isolation. Choosing among the resulting candidates is where [[DefinedTerm/llm-as-judge]] and cross-model review come in — the same survey's "AI on AI review" patterns include switching models when one gets stuck, implementing in one tool and reviewing in another, and keeping implementation and review agents as separate [[DefinedTerm/subagents]].
