---
title: "Agentic Skill Decay"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, human-oversight, verification]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agentic-skill-decay/'
    hash: sha256:9ad04962aaf0ace13d47849dfc19a03332011498de015a9cc7914d7dcbacb20a
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "Addy Osmani's argument that coding agents skip much of the trial, failure and debugging through which engineers used to build expertise, so the repetitions that produce judgment now have to be sought out deliberately — and that each correction should be captured somewhere durable so it sharpens both the engineer and the agent."
  author: "Addy Osmani"
  datePublished: "2026-08-31"
---

This post argues that "mastery still comes from doing the reps." Before agents, the author says, the reps arrived as a side effect of writing code — trying approaches, debugging what went wrong, reviewing others' code and reading widely. Agents can now go from a problem straight to a working patch while skipping that work, so building the reps "has to be deliberate." The post is a concern about [[DefinedTerm/skill-atrophy]] framed for engineers early in their careers: "If you're three years into your career, plausible code may arrive faster than your ability to judge it."

It is explicitly not an argument for using agents less. The author says he uses them aggressively, sometimes running five or ten sessions at once, and that an episode of asking the wrong project to add dark mode clarified that "agent throughput scales faster than my attention." The argument is that agent work still depends on expertise for verification, and that expertise has to be built on purpose.

## Key Points

- Good agent work, in the author's experience, depends on two abilities: deep expertise (understanding the domain well enough to define a good outcome, including the user, product and business) and applied judgment (using taste to turn that into a clear, testable plan through the right context, constraints, tests and verification).
- The four skills worth practising to build those abilities are named as decision making, specifying, steering and verifying.
- "A completed task is not necessarily a rep": finishing a task does not mean anything was learned, and a task that went right without mistakes offers little to reflect on.
- The author recommends deliberate interventions: form a hypothesis before prompting, ask why repeatedly, read the diff and predict what might still fail, and occasionally work a problem through by hand — describing reading the diff as "the single highest-value minute in the whole loop" and the easiest to skip.
- Learning can be requested from the agent itself — asking it to explain a concept it just implemented, or to summarize the key learnings at the end of a task — but the author observes that most people do not ask for this and that AI labs largely optimize for reaching an outcome quickly.
- The author argues that people who use AI to ask conceptual questions and request explanations, rather than treating the model as "a code vending machine," build more understanding than those who only use it to generate output — and that someone who is merely good at prompting will be weaker at verification. He supports this with research from Anthropic, while cautioning that the evidence he cites is short-term and not conclusive.
- He argues that one need not have a decade of experience across the stack, but "you need to understand the problem domain enough to recognize what good means."
- "Verification is the floor and imagination is the ceiling": you can only prompt what you can picture, and only keep what you can confirm is good.
- "Skills and MCPs can encode a useful workflow. They cannot tell you when its assumptions no longer fit your system."
- Lessons should be put "where the next agent can find it" — a lessons file, memory, a lint rule, a type constraint, a documentation convention or a test — because a lesson left in a chat window can disappear when the session ends or is compacted; without this, starting a new session can feel like "onboarding a new hire that has amnesia." The author also cautions against over-investing in markdown files as the strategy.
- The post closes by locating the engineer's role in the outer loop: writing and refining plans, defining what done means, and planning where humans stay in the loop to check correctness, safety and user impact — see [[DefinedTerm/outer-loop]].

## Context

The examples are from the author's own experience: learning performance optimization through thousands of hours in the Chrome DevTools performance panel (work he notes a DevTools MCP can now do for an agent), building interactive 3D objects for an album site whose first versions used the wrong interaction pattern and performed badly on mobile, and a text editor whose generated UI had problems he recognized because he had made those mistakes before. He states he does not know how long code-level expertise will remain as valuable as it is today, given how quickly models are improving.

The post also says the author is glad that guidance on working with [[SoftwareApplication/claude-code]] starts with verification. It lists three other posts by the same author as related reading: [[BlogPosting/brownfield-agentic-engineering]], [[BlogPosting/audit-your-agent-files]] and [[BlogPosting/human-judgment-doesnt-leave-the-software-factory]].
