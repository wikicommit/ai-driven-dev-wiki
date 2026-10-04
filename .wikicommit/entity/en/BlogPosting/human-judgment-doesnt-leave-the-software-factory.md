---
title: "Human judgment doesn't leave the software factory. It relocates."
type: "schema:BlogPosting"
lang: en
tags: [software-factory, human-oversight, verification, agentic-engineering]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/human-judgment-doesnt-leave-the-software/'
    hash: sha256:c4cc398bbcb3b786b12103edd73235c1799a0c14110e69dfb8a172809051a0b4
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "Addy Osmani's argument that in a software factory — a repeatable, event-driven loop around software work — human judgment is not removed but relocated: upstream to product intent, system design and the quality bar, and downstream to evidence, risk and ownership of what ships."
  author: "Addy Osmani"
  datePublished: "2026-08-21"
---

This post defines a [[DefinedTerm/software-factory]] as "a repeatable loop around software work" and argues that building one does not take people out of software development. "The percentage of code physically typed by humans may fall dramatically," the author writes, but human ownership need not fall with it: someone still chooses the problem and the architecture, sets the quality bar, decides which verification signals deserve trust, and decides when the evidence is sufficient to ship. "Human judgment is being relocated" — and the best factories, on his account, will be defined not by how completely they eliminate human involvement but by how intelligently they place it.

The post opens by questioning whether a factory is needed at all. The author says a stock coding harness such as Claude Code or Codex, with multiple sessions, good specs with verification built in, and constraints, gets surprisingly far; a factory becomes useful when the work has to be repeatable and event-driven, fed by a queue such as Slack triggers, GitHub issues, Linear or a backlog and run in an isolated cloud environment. Part of the post draws on a sample factory he built and published as a reference setup, run against a movies demo app.

## Key Points

- The author's summary prescriptions: keep humans in the loop up front on product intent, system design and the quality bar; review code where it is needed most, especially where automated back-pressure breaks or maintainability trade-offs must be made; run quality checks as early and continuously as possible; and remember that the number of checks is not quality, tightening or relaxing constraints deliberately.
- A factory earns its keep when the hard part is making runs behave consistently, handing work between agents, keeping two sessions from claiming the same issue, preserving evidence, and stopping production when human review falls behind.
- He describes a triage label used this way as doing three jobs at once — the queue, the lock and, because a session only picks up work marked ready, a place a human can park work without rejecting it permanently — citing Warp's practice of triaging every issue into one of four states.
- In a good factory the human can shape work early, steer it during implementation, take it through a handoff or stop it from shipping, rather than only approving a final diff.
- Human cognitive bandwidth does not scale with the number of agents, which he says can feed cognitive or comprehension debt; see [[DefinedTerm/comprehension-debt]]. He recommends optimizing the factory for its reviewer.
- "Just because a software factory is showing that everything is green doesn't mean that it's actually green": an agent asked to pass a test may change the test or the logic without following the intent behind it.
- A factory that reads untrusted input such as GitHub issues or Slack messages may receive adversarial content; he cites Vercel running its factory's agents in isolated sandboxes that hold only the secrets a task needs, as a layered defence.
- Tasks can take two to four times as long once verification, retries, browser checks and human review are included; in his sample factory the verifiers caught real problems, but he cautions that a factory running many checks nobody finds valuable is not thereby high quality.
- He proposes a [[DefinedTerm/verification-budget]], modelled on performance budgets: fast checks such as linting and type checking run early, while the full test suite, mutation testing, browser testing and security checks run around the draft pull request.
- He describes Vercel's factory as classifying each agent run as success, flawed, blocked or manual, with only success shipping, and adds that the taxonomy should be paired with per-stage timing: in his own factory a feature with no rejections took 7 minutes while one with two rejections and a human decision took 56. A manual run, he argues, "isn't finished when the factory stops but when the human knows what to do next."
- Verification buys trust, and trust buys autonomy, so autonomy is not a single setting for every project; see [[DefinedTerm/agentic-autonomy-levels]].
- Code often preserves a decision but not why it was made, so he suggests asking agents to record their trajectory or lessons for later reference.

## Context

The post is written from the author's own practice of running parallel agent sessions across client applications, open-source projects and personal tools. He recounts two of his own mistakes: typing a dark-mode prompt into the session for the wrong project, and merging a favouriting feature whose tests passed, then finding days later that he could not explain how it worked and had to relearn it step by step. He also asks which abandoned projects deserve another life now that agents make finishing them cheap, arguing that whether something should exist remains a human question.

It names Factory, Warp and HumanLayer as working on factory products for teams that would rather buy than build. It refers to an earlier post by the same author on autonomy — see [[BlogPosting/agentic-autonomy-levels]] — and lists [[BlogPosting/brownfield-agentic-engineering]], [[BlogPosting/agentic-skill-decay]] and [[BlogPosting/audit-your-agent-files]] as related reading. The post notes it was originally published on the author's Substack.
