---
title: "Embracing the parallel coding agent lifestyle"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agents, code-review, agent-tooling]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Oct/5/parallel-coding-agents/'
    hash: sha256:27a558fb1c27fb41f4cd14d4f2ca868bc5608598aa43aa8c8c499603246a88ce
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A firsthand account of coming round to running several coding agents at once, organised as four categories of task that parallelise without adding much cognitive overhead to the one change the author is actually reviewing."
  author: ["Simon Willison"]
  datePublished: "2025-10-05"
---

The post opens with the objection rather than the practice. The author reports hearing for a while
from engineers running several coding agents at once — multiple [[SoftwareApplication/claude-code]]
or Codex CLI instances, sometimes in one repo, sometimes across separate checkouts or
[[DefinedTerm/git-worktrees]] — and being sceptical of it, on the grounds that AI-generated code
has to be reviewed and so the natural bottleneck is how fast he personally can review
(compare [[DefinedTerm/review-bottleneck]]). If keeping up with one model is already hard, he asks,
what is gained by running more than one if it only leaves you further behind.

What changed is not the objection but its scope. He reports that he can still only focus on
reviewing and landing one significant change at a time, and that what he found instead was an
increasing number of tasks that can be fired off in parallel *without* adding much cognitive
overhead to that primary work. The body of the post is four categories of such task, presented as
patterns he has found effective rather than as a method.

The categories run from work that is never kept to work that is. Research tasks answer a question
or produce a recommendation without any modification he intends to keep — his example is settling
whether two libraries actually work when wired together, and he notes that a library too new to be
in the training data is not an obstacle, since the agent can be told to check out its repository and
read the code. Questions about an existing system are next: he argues that codebase size does not
matter here, because agents are extremely effective with tools like grep and can follow a codepath
through dozens of files, and that the explanations are worth keeping because they make good context
for later prompts. Then small, very low-stakes maintenance — a deprecation warning in the test suite
handed off wholesale — which he describes as requiring a knack best developed by trying things. Last
is work he has specified himself: he argues that reviewing code that arrives out of nowhere is
expensive because the goals have to be reconstructed first, and that code built from his own
detailed specification is far cheaper to confirm.

## Key Points

- The bottleneck on agent-assisted work is the author's own review capacity, and this is stated as
  the reason he was initially sceptical of running agents in parallel rather than as a reason it
  cannot work.
- The resolution he reports is a division of labour rather than more review: one significant change
  under active review at a time, with additional tasks chosen specifically because they add little
  cognitive overhead to it.
- Research and proof-of-concept work parallelises well because nothing produced is intended to be
  kept, so it never enters the review queue.
- A library being too new to appear in a model's training data is not a blocker for this kind of
  spike: the agent can be directed to check out the dependency's repository and read its source.
- Questions about how an existing system works are answered by current reasoning models in a minute
  or two, and the author states that codebase size does not limit this because agents use tools like
  grep effectively and can follow codepaths across dozens of files.
- LLM-generated explanations of one's own system are worth stashing, because they make good context
  to paste into later prompts (compare [[DefinedTerm/context-engineering]]).
- Low-stakes maintenance chores — his example is a deprecation warning surfacing in the test suite —
  are worth delegating precisely because they carry small cognitive overhead rather than small
  technical difficulty.
- Spotting these opportunities is described as a knack developed by attempting small tasks and
  learning from both the successes and the failures; this is offered as the author's own instinct,
  not a rule.
- Reviewing an unsolicited change requires first deriving its goals, whether the project needs it,
  and whether its approach suits planned future work — all before reading the code.
- Code generated from a specification the reviewer wrote themselves is substantially cheaper to
  review, because the goal, approach and detailed specification were already decided.
- The author's reported daily drivers at the time of writing are Claude Code on Sonnet 4.5,
  [[SoftwareApplication/openai-codex]]'s CLI on GPT-5-Codex, and its cloud counterpart for
  asynchronous tasks, which he says he frequently launches from his phone.
- He reports also trying [[SoftwareApplication/github-copilot-coding-agent]] and
  [[SoftwareApplication/google-jules]], describing the latter as Google's then-free alternative to
  the cloud agent above.
- His local setup is several terminal windows in different directories running a mixture of agents in
  [[DefinedTerm/yolo-mode]], restricted to tasks where he is confident malicious instructions cannot
  reach the context.
- He states that he ought to be running local agents in Docker containers to limit the blast radius
  and has not made a habit of it — recorded as an intention rather than his practice.
- He had not adopted git worktrees at the time of writing, using a fresh checkout instead when he
  wants two agents isolated against one repo.
- Riskier tasks go to asynchronous cloud agents, where he bounds the worst case as his source code
  being exfiltrated — he allows the agent network access — and notes this matters less to him
  because most of what he works on is open source.
- GitHub Codespaces running an editor's agent mode is reported as surprisingly effective and
  particularly good for workshops and demos, because it works for anyone with a GitHub account and
  needs no extra API key.
- The author dates the models becoming good enough to drive these tools effectively to only the few
  months before writing, naming the Claude 4 and GPT-5 generations in particular.
- He reports trying the practice of handing an agent a genuinely difficult task against a large
  codebase with no intention of landing its output, purely to learn which files it touches and how it
  frames the problem — a habit he credits to Josh Bleecher Snyder, who calls it sending out a scout.

## Context

The post sits in the author's continuing series on his own use of LLMs and is explicitly presented as
unfinished thinking: he says he is still settling into patterns, expects to keep iterating on them,
and closes by encouraging other practitioners to publish their own. Its evidence throughout is his
own recent practice — which tools he runs, what he delegates, what he has not got round to — rather
than measurement, and the security posture is given as personal risk judgment, including the
admission that he runs without approvals and feels he should containerise. It also positions itself
against three other practitioners' published accounts of parallel-agent workflows, which it
recommends rather than summarises; the details of those accounts are theirs and are not established
here. An earlier post of the author's on directing models very explicitly is cited as the origin of
the fourth pattern, and [[BlogPosting/designing-agentic-loops]] is the immediately preceding entry in
the same series.
