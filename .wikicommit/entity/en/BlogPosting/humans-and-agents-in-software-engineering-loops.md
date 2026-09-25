---
title: "Humans and Agents in Software Engineering Loops"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, harness-engineering, human-oversight]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html'
    hash: sha256:767b9a865639b9476811d14704d9d23901875bda1ac1263f9794e9aa70ba663c
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A March 2026 article by Kief Morris in the \"Exploring Gen AI\" series on martinfowler.com, arguing that humans should work \"on the loop\" — building and improving the harness that controls how agents produce software — rather than staying out of the process or inspecting everything agents produce."
  author: ["Kief Morris"]
  datePublished: "2026-03-04"
  publisher: "martinfowler.com"
---

This article, part of the "Exploring Gen AI" series on martinfowler.com, asks whether humans should
stay out of the software development process and vibe code, or stay in it inspecting every line an
agent writes. Its answer is a third position, which the author calls
[[DefinedTerm/humans-on-the-loop]]: humans should build and manage the working loop rather than
either leaving agents to it or micromanaging what they produce.

The argument rests on two loops. The **why loop** turns ideas into working software and iterates as
ideas evolve; humans run it because they are the ones who want what it produces. The **how loop** is
the process of building the software, in which intermediate artefacts — code, tests, tools,
infrastructure, designs, ADRs — are created and used, and which in reality contains several nested
loops, from specifying and delivering a feature down to generating and testing code. The article
examines where humans sit relative to the how loop, and ends with a further step it calls the
[[DefinedTerm/agentic-flywheel]].

## Key Points

- Intermediate artefacts, and the practices and patterns that produce them, are a means to the
  outcome people actually care about rather than deliverables in their own right.
- **Humans outside the loop** — leaving the how loop to agents — is described as the common
  definition of [[DefinedTerm/vibe-coding]], and the author says some interpretations of
  [[DefinedTerm/spec-driven-development]] are much the same.
- What matters is external quality (functional correctness and non-functional, operational quality
  such as not crashing, running fast, not leaking data, controlling hosting costs, passing
  compliance audits), and internal quality matters only when it affects external outcomes. The
  author argues it still does: agents understand and modify a cleanly designed, well-structured
  codebase more quickly and spiral less, and the time and cost of building systems matter.
- **Humans in the loop**, in the sense the article discusses, often means humans acting as
  gatekeepers inside the innermost loop, such as manually inspecting each line of code. The author
  argues this makes humans a bottleneck, since agents generate code faster than humans can inspect
  it, and suggests mixed reports on AI developer productivity may be partly due to people spending
  more time specifying and reviewing code than generation saves (see also
  [[DefinedTerm/human-in-the-loop]]).
- Applying "shift left" thinking, agents produce better code when they can gauge its quality
  themselves rather than relying on humans to check it, so humans should instruct them on what is
  wanted and how best to achieve it.
- **Humans on the loop** means making agents better at producing results instead of inspecting what
  they produce. The collection of specifications, quality checks and workflow guidance that control
  the loops inside the how loop is, in the author's terms, the agent's harness, and building and
  maintaining it — [[DefinedTerm/harness-engineering]] — is how humans work on the loop.
- The difference shows in what one does when unhappy with an agent's output: in the loop, fix the
  artefact (directly or by telling the agent); on the loop, change the harness that produced it.
- In the agentic flywheel, humans direct agents to manage and improve the harness, starting from
  interactive consideration of their recommendations and possibly moving to automatic approval of
  recommendations with certain scores.
- The author suspects that for standard, frequently done work this may come to look like humans
  out of the loop, but argues that engineering the harness yields robust, "maybe even anti-fragile"
  systems that continuously improve themselves rather than one-off "good enough" solutions.

## Context

The article presents the three positions as the author's own framing. It notes that something like
the on-the-loop concept has also been described as the "middle loop", including by participants of a
retreat on the future of software development, and it links to a separate martinfowler.com article
on harness engineering for the practice itself. A footnote observes that the
[[DefinedTerm/ralph-loop]] is often used colloquially to mean leaving agents looping until they
finish, whereas as originally described the operator plays an important role in steering them.
