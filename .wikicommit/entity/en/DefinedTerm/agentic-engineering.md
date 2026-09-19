---
title: "Agentic Engineering"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agentic-engineering/'
    hash: sha256:400d58d9e25dd34745df0153942cb3f9205ef0dd5fb9fd999012c47e33996bca
  - type: url
    url: 'https://arxiv.org/pdf/2606.05608'
    hash: sha256:0793091fcad2dc48f9eb6412001558cc2e993e5d5904e18d8fd0c943453879be
  - type: url
    url: 'https://www.andrewconnell.com/articles/vibe-coding-vs-agentic-engineering/'
    hash: sha256:7e8c13f25dd70015f9995dcbf564e7a460760543e3cd12d89b9175dcdf1bf151
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A term for disciplined, AI-agent-assisted software development with continued human oversight — planning and specifying before prompting, reviewing every diff, testing relentlessly, and owning the resulting system — proposed by Andrej Karpathy and adopted by Addy Osmani as the name for that disciplined practice, distinct from vibe coding (which keeps its original, reckless meaning) and from Simon Willison's 'vibe engineering' proposal for the same disciplined endpoint."
---

Agentic engineering is a term for a disciplined style of AI-agent-assisted software development in which a human writes a plan or spec before prompting, directs an AI agent on well-scoped tasks, reviews its output with the same rigor applied to a human teammate's pull request, tests relentlessly, and remains responsible for the resulting system's architecture, correctness, and long-term maintainability. Andrej Karpathy suggested the term in early February 2026, and Addy Osmani adopted it in this post as the name for that disciplined practice — distinct from "vibe coding," which keeps its original meaning (Karpathy's own year-earlier coinage for a deliberately reckless, unreviewed AI-driven workflow) rather than being retired, and from Simon Willison's earlier proposal for the same disciplined endpoint, "vibe engineering."

## Usage

The term is proposed to stop "vibe coding" being applied to two fundamentally different activities: its original reckless-prototyping sense, and disciplined, agent-assisted development with human oversight. Agentic engineering is the name Osmani now prefers for that disciplined endpoint — the same endpoint he had previously called "AI-assisted engineering" and that Willison had proposed calling "vibe engineering" — contrasted against vibe coding's reckless end of the spectrum: vibe coding involves no code review and targets fast prototypes, while agentic engineering means AI handles the implementation under the human's ownership of architecture, quality, and correctness. In practice, the source describes it as: starting with a written plan or spec before prompting; directing an agent on a well-scoped task and reviewing its output at the rigor of a human PR; testing relentlessly, since a solid test suite is what lets an agent iterate to a trustworthy result rather than declaring broken code "done"; and the human continuing to own documentation, version control, CI, and production monitoring.

A second, independent account of the term comes from
[[ScholarlyArticle/agentic-software-restructuring-paradigm]], and it is worth keeping separate from the
one above because it is about a different thing. Where the blog account describes a disciplined *human
practice* of directing and reviewing coding agents, that paper treats agentic engineering as a *field*:
an expansion of the software engineering discipline whose core object of study is agent systems rather
than static source code, whose control model is LLM-driven rather than human-predefined, and whose
human role is intent architect rather than code author. It attributes the formal introduction of the
term in that sense to LangChain in April 2026, quoting a definition of it as a multi-agent coordination
model in which AI agents function as digital team members — each with defined roles, shared memory and a
unified observability layer — to drive software through the entire delivery pipeline rather than merely
to generate code faster. The paper's own argument is that this expands software engineering rather than
replacing it, since the agent is itself software, and that building, deploying and governing agent
systems is the discipline's next frontier.

That paper contrasts the two practices across nine dimensions: the core artifact moves from static
source code to a dynamic agent system, the control centre from the human engineer to the LLM reasoning
engine, the decision mechanism from pre-designed logic to runtime-generated reasoning, the development
cycle from linear design-code-test to an autonomous iterative loop, the human role from code author to
intent architect, coordinator and auditor, the complexity ceiling from fixed human cognition to model
capacity, the output unit from functioning software to delivered outcomes, error handling from
programmer-defined to model-adaptive, and evolution from manual refactoring to self-modification. It
names the new human differentiators as intent articulation, architectural oversight, quality
calibration and ethical governance.

A third account, by Andrew Connell, states the term as a one-sentence definition and then spends
its length on the contrast: agentic engineering is the practice of using AI-powered coding agents
as force multipliers under your direction, while you retain full responsibility for architecture,
code quality, and engineering judgment. That matches the disciplined-practice sense above rather
than the field-level one, and it is reached from the other side — the piece is framed as an
argument about what [[DefinedTerm/vibe-coding]] is not, with the two set out in a table whose rows
are who it is for, whether the code is reviewed, risk level, best use cases, where engineering
judgment sits, and whether maintainability is a priority.

The work Connell assigns to agents is the monotonous and tedious part rather than the design. His
four examples are breaking a long, hard-to-read file into smaller modules; generating initial test
coverage and edge cases, especially before a large refactor; having an agent review a pull request
for bugs, security issues and inconsistencies before teammates see it; and the repetitive,
pattern-based changes of a framework upgrade or library migration, with the developer taking the
tricky edge cases. His image for the relationship is a head chef and a sous chef: the agent is
skilled, capable and fast, but it does not decide the menu.

## When It Applies

The source frames agentic engineering as disproportionately benefiting engineers with strong existing fundamentals (system design, security patterns, performance tradeoffs), since recognizing good AI output requires already knowing what good code looks like; it assumes a supporting test suite is in place, since testing is described as the mechanism that turns an unreliable agent into a reliable system. Its stated failure mode is a junior engineer leaning on AI before building those fundamentals, risking skill atrophy — producing and shipping code without understanding or being able to debug it. As of this post, the term is presented as a fresh, actively-debated proposal rather than settled usage: Karpathy suggested it days before the post was written, after the author says the community spent months debating Willison's "vibe engineering" alternative.

The academic account sets its own conditions differently, because it is describing a field rather than
a personal practice. It is explicit that the field is early: it reports the [[Dataset/evoclaw]]
benchmark's finding that agent success rates fall from above 80% on isolated tasks to at most 38% under
continuous software evolution, and concludes that agentic engineering is real and transformative today
as an augmentation paradigm but that fully autonomous software development remains a multi-year
research challenge. That paper is a position paper synthesising other work rather than reporting
measurements of its own, and the nine-dimension contrast it draws is presented as an analytical
framing.

Connell's conditions are close to the first account's and stated as an argument for learning the
practice rather than as limits on it. He holds that the approach is the natural next step in a
line of tools developers have always adopted — he names IntelliSense, integrated documentation
and compile-time checks — and that a developer who wants to stay relevant needs to understand
these tools and how to use them effectively. His stated entry point is deliberately small: take
one tedious task from the current sprint, hand it to a coding agent, and review every line it
produces.

## Related Terms

[[DefinedTerm/vibe-coding]], [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/skill-atrophy]], [[DefinedTerm/ai-coding-agent]]

- [[ScholarlyArticle/agentic-software-restructuring-paradigm]] — source of the second, field-level
  account above
- [[DefinedTerm/agentic-software]] — the kind of artifact that account says the discipline now builds
- [[DefinedTerm/four-stage-evolution-of-agentic-engineering]] — the same paper's roadmap for the field
- [[DefinedTerm/agentic-engineer]] — a separate term, and a different question: what qualifies an AI
  agent as a software engineer, rather than what the discipline is
