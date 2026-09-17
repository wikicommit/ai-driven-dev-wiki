---
title: "Agentic Engineering"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agentic-engineering/'
    hash: sha256:400d58d9e25dd34745df0153942cb3f9205ef0dd5fb9fd999012c47e33996bca
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A term for disciplined, AI-agent-assisted software development with continued human oversight — planning and specifying before prompting, reviewing every diff, testing relentlessly, and owning the resulting system — proposed by Andrej Karpathy and adopted by Addy Osmani as the name for that disciplined practice, distinct from vibe coding (which keeps its original, reckless meaning) and from Simon Willison's 'vibe engineering' proposal for the same disciplined endpoint."
---

Agentic engineering is a term for a disciplined style of AI-agent-assisted software development in which a human writes a plan or spec before prompting, directs an AI agent on well-scoped tasks, reviews its output with the same rigor applied to a human teammate's pull request, tests relentlessly, and remains responsible for the resulting system's architecture, correctness, and long-term maintainability. Andrej Karpathy suggested the term in early February 2026, and Addy Osmani adopted it in this post as the name for that disciplined practice — distinct from "vibe coding," which keeps its original meaning (Karpathy's own year-earlier coinage for a deliberately reckless, unreviewed AI-driven workflow) rather than being retired, and from Simon Willison's earlier proposal for the same disciplined endpoint, "vibe engineering."

## Usage

The term is proposed to stop "vibe coding" being applied to two fundamentally different activities: its original reckless-prototyping sense, and disciplined, agent-assisted development with human oversight. Agentic engineering is the name Osmani now prefers for that disciplined endpoint — the same endpoint he had previously called "AI-assisted engineering" and that Willison had proposed calling "vibe engineering" — contrasted against vibe coding's reckless end of the spectrum: vibe coding involves no code review and targets fast prototypes, while agentic engineering means AI handles the implementation under the human's ownership of architecture, quality, and correctness. In practice, the source describes it as: starting with a written plan or spec before prompting; directing an agent on a well-scoped task and reviewing its output at the rigor of a human PR; testing relentlessly, since a solid test suite is what lets an agent iterate to a trustworthy result rather than declaring broken code "done"; and the human continuing to own documentation, version control, CI, and production monitoring.

## When It Applies

The source frames agentic engineering as disproportionately benefiting engineers with strong existing fundamentals (system design, security patterns, performance tradeoffs), since recognizing good AI output requires already knowing what good code looks like; it assumes a supporting test suite is in place, since testing is described as the mechanism that turns an unreliable agent into a reliable system. Its stated failure mode is a junior engineer leaning on AI before building those fundamentals, risking skill atrophy — producing and shipping code without understanding or being able to debug it. As of this post, the term is presented as a fresh, actively-debated proposal rather than settled usage: Karpathy suggested it days before the post was written, after the author says the community spent months debating Willison's "vibe engineering" alternative.

## Related Terms

[[DefinedTerm/vibe-coding]], [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/skill-atrophy]], [[DefinedTerm/ai-coding-agent]]
