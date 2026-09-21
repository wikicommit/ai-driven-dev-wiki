---
title: "エンジニア2人 × AI で回すプロダクト開発 — “開発プロセスの半分以上をAIが主導的に行う” 体制の実践"
type: "schema:BlogPosting"
lang: en
tags: [agents, agent-config, code-review, spec-driven-development]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62110/'
    hash: sha256:63c389aa849ff61307fb6c1aeae2debc609bb205fea277d3393d798eacf874da
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A CyberAgent engineer's account of rebuilding a two-person team's development process so that AI leads requirements definition, technical design, task splitting, implementation and review, with the humans reduced to deciding and confirming — built on 37 Skills and 24 SubAgents over about a month and a half."
  author: ["りゅうせい"]
  datePublished: "2026-02-16"
  publisher: "[[Organization/cyberagent]]"
---

This post describes how a two-engineer team rebuilt its development process around AI after the team that once ran the product shrank from six engineers to two without a matching reduction in the work expected of it. The author's framing of the response is a role swap: stop using AI as an auxiliary tool, make the AI the leader and the human the supervisor, whose only two jobs become deciding and confirming.

The post's most distinctive argument is a refusal of the usual productivity claim. It states that with current AI a single implementation task often gets *slower*, because the agent has to investigate prior implementations and documents, draw up a plan and check consistency against business requirements before writing anything — so for simple work the total time goes up. The gain, on this account, comes from elsewhere: because the human supervises rather than leads, several tasks can run at once, and the necessary premise is that the human is doing something else while they run — in a meeting, or at lunch. The author is equally explicit that this does not make the work easier, arguing it demands more concentration and more frequent context switching.

The concrete claim is that the setup was built from a standing start in about a month and a half — the author says the team's foundation in early December was "AI-driven? what's that?" — and that by late January the repository held 37 Skills and 24 SubAgents, allowing two engineers to sustain the output of the previous six-person team.

## Key Points

- The stated division of labour gives the human three acts: writing the outline of business requirements, answering the AI's questions during generation, and lightly checking or correcting its output. Everything between is the AI's.
- Two mechanisms carry the structure: a **Skill**, defining expertise or required behaviour — what order to do things in, what the quality bar is, what to do on failure — and a **SubAgent**, a specialist agent for one area, which may itself use Skills. A main agent uses a Skill to act as orchestrator over SubAgents.
- The requirements flow starts from a Linear issue holding only an outline, which the post says need not be filled in completely. An orchestrator Skill then runs three SubAgents in sequence: an analyzer that fetches the issue and interrogates ambiguity, a generator that writes the business requirements document, and a validator that scores it on ten criteria and auto-repairs up to three times when it falls below 80.
- The stated reason for splitting one agent into three is context separation: giving one agent everything makes its context balloon and performance drop, whereas specialist agents stabilize output quality and let a failed phase be redone on its own.
- The questioning loop is built on Claude Code's AskUserQuestion tool, which lets the AI put multiple-choice questions to the human mid-run and keep looping until nothing is unclear. The author's claim for it is that the AI does not only do what it is told but asks for what is missing, pressing on exactly the points a human tends to defer.
- Task files are written to be self-contained — task summary, as-is/to-be, schema, API spec, full Given-When-Then test items, dependencies — explicitly so that implementation need not consult the design document. The stated reason is that separate AI sessions implement these tasks in parallel, so inter-task context dependency must be zero.
- Implementation runs TDD, then a `code-simplifier` agent is run unconditionally after CI passes, then technical and specification reviews run in parallel; both must score at least 80 with no Critical or High findings, or an automatic repair loop runs. The post gives the governing parameters as at most 4 implementation iterations and 3 review iterations.
- Parallelism is implemented with `git worktree`, one worktree and branch per task off a shared epic branch, each with its own Claude Code session.
- On GitHub, Skills and SubAgents like those used locally are run under **Codex** rather than Claude Code, the stated reason being that a different agent yields review from more angles. That workflow detects which languages changed, runs the matching reviews in parallel, and auto-approves the pull request when every score clears 80.
- Branch strategy makes the AI approval a precondition rather than a substitute for human review: feature branches merge into an epic branch on AI approval alone, and only once every feature branch has merged and the AI approves the epic does a human review it.
- Two obstacles are named as the limits on going further: tacit knowledge, since AI faithfully implements only what is written and so reproduces the holes in a specification; and human capacity, since two people cannot read every pull request when many tasks run at once.
- The response to the first is a five-layer hierarchy of tacit knowledge embedded in the codebase — product context, coding conventions, quality standards (golden files), references, and workflow — which the author says lets the AI work down the layers as a new human team member would.
- The claims throughout are the author's own account of their own team, and are almost entirely unquantified: the "six people's worth of output" comparison is stated as an outcome rather than a measured one, and the post concedes the setup itself cost considerable effort to build. The one before/after figure it does give is for the requirements phase, where human working time is put at several hours before and about 10–20 minutes after.

## Context

The post situates itself against what the author takes to be the common state of practice — teams that have adopted Skills and SubAgents but where the human is still the leader — and against a widespread expectation it says it does not share, that AI makes individual tasks finish faster and makes the work easier.

Its stated future work is to extend the same flow past pull-request review: end-to-end test environments, automatic determination of what to release, release automation, and error monitoring that produces a fix pull request on its own. The author gives the destination as "write an issue in Linear, and AI leads it through to production release".

On parallel implementation specifically, the post notes that its thinking has a good deal in common with practices already shared publicly elsewhere, and points readers to that material rather than restating it.
