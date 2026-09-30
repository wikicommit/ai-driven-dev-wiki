---
title: "Claude Code で1体のAIレビューに欲張って失敗し、3エージェントに分けた話"
type: "schema:BlogPosting"
lang: en
tags: [agentic-code-review, sub-agents, claude-code]
sources:
  - type: url
    url: 'https://tech-lab.sios.jp/archives/53091'
    hash: sha256:ad600fed8b9b62a03a62c07d1ed68806968ad524260b789712fdd5d404cb3432
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A SIOS Tech Lab post recounting how asking one Claude Code review agent to check seminar slides from every angle failed, and how the author split the job into three sub-agents that differ in perspective, scoring starting point and the input they are given."
  author: ["龍：Ryu"]
  datePublished: "2026-06-24"
  publisher: "SIOS Technology, Inc."
---

The post (its title translates roughly as "How I got greedy with a single AI reviewer in Claude Code,
failed, and split it into three agents") is a practitioner's account of using AI review on seminar
slides. Its starting complaint is that asking one AI to "review this" returns inoffensive impressions —
"well organised overall, and the flow is natural" — that leave nothing to fix. The author's diagnosis
is that one reviewer asked to look at everything mixes perspectives whose pass lines point in opposite
directions, so they cancel out into "probably fine on the whole".

The remedy is three [[SoftwareApplication/claude-code]] sub-agents, each defined in its own file
under `.claude/agents/`. The author prepares slides in three stages — an *outline* that fixes audience
and takeaway, a text-only *storyboard* that fixes what each slide says and in what order, and the
finished *slide* deck — and the agents are handed different inputs from them, because what an agent
can judge depends on what it is given: the harsh reviewer gets the slides, the logic reviewer gets the
storyboard together with the relevant range of slides, and the audience-reaction agent gets only the
slides of the chapter in question. The centre of the post is a failure: running the harshest of the three
repeatedly on an outline made the outline longer and its score lower, which is what led to the
second agent (see [[DefinedTerm/review-loop-non-convergence]]). The post publishes all three agent
definitions in full as an appendix.

## Key Points

- A single reviewer told to check everything gives bland, unactionable feedback, because checks with
  opposite pass lines — logic versus the sharpness of the wording — cancel each other out.
- **harsh-review-agent** scores from 0 ("the bin") and looks for evidence of why the material deserves
  0: praise is forbidden, AI-typical "dead words" such as "optimisation", "seamlessly" and "DX
  promotion" are listed and condemned, and a raw score somewhere in the 10s to 30s is treated as normal for
  AI-generated material. The author uses it only once the slides exist.
- Running the harsh reviewer on an outline for three fix-and-resubmit cycles grew the outline from 685
  to 772 lines while its score fell from 47 to 44: because the agent is built to always find evidence,
  each addition made to answer a finding drew new findings of its own, such as "too dense".
- When the author sorted the harsh reviewer's findings into logical breakdowns and matters of taste,
  the majority turned out to be taste; the author concluded it was a fastidiousness filter, not a detector of
  logical failure.
- **logic-reviewer** scores from 100 and may report only five kinds of logical breakdown — a failed
  link from premise to conclusion, a term whose meaning shifts, a promise made by a title or opening
  that the body never fulfils, a missing dependency, and internal contradiction — and must report 100
  when it finds none, without "just in case" remarks. It can be used from the outline stage onward.
- **audience-reaction-agent** plays one persona in the audience, reads only the scope it is given and
  nothing after it, ignores the speaker's intent notes in the storyboard, gives no score and does not
  condemn; the author's point is that designing what the agent is *not* given is what makes its
  reaction resemble a real listener's.
- All three produce read-only, one-way reports saved by date and type; the agents do not edit the
  material, and the author decides what to adopt: earlier decisions come first, clear logic errors are
  fixed at once, and where agents disagree the author takes the one closer to their own intent or
  proposes a new option.
- From his own trials, the author reports that an agent reviewing slides for visual crowding caught 1
  of 7 cases, and that piling up reviewers that all push to cut things erodes the argument itself.

## Context

The post is one developer's account of their own setup, published on their employer's engineering blog,
and its evidence is the author's own runs and scores rather than any measured comparison. The author sums the approach
up as splitting by perspective, inverting the starting point, and narrowing the input, and says it is
not specific to slides: the author also uses the harsh and logic reviewers on blog posts, and the logic
reviewer on outlines, proposals and specs. The post leaves open whether defending the author's own claims
against the reviewers could also be delegated to an agent, saying the right balance has not been found yet.
Its account of review findings being weighed by a person, rather than applied wholesale, sits close to
[[DefinedTerm/review-finding-triage]], and its use of several narrowly scoped agents is an instance of
[[DefinedTerm/sub-agent-architecture]].
