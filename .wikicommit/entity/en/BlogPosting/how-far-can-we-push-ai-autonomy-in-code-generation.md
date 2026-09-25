---
title: "How far can we push AI autonomy in code generation?"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, multi-agent-systems, human-in-the-loop, code-quality]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/pushing-ai-autonomy.html'
    hash: sha256:fcbffbf069d194c76d66a85c503e4d95f55b1f851cd622480532247bd9df624f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An August 2025 article by Birgitta Böckeler on martinfowler.com reporting a series of experiments that pushed an agentic workflow to build simple Spring Boot applications with minimal human intervention. It concludes that, even with many control strategies in place, AI is not ready to create and maintain a maintainable business codebase without human oversight."
  author: ["Birgitta Böckeler"]
  datePublished: "2025-08-05"
  publisher: "martinfowler.com"
---

This article reports experiments run to learn how far the autonomy of generative-AI code generation
could be pushed with a deliberately *simple* application: a CRUD API backend in Spring Boot, judged
through the lens of business application software and digital products. The team built an agentic
workflow, mostly driven by Claude Sonnet models (3.7 or 4), and applied a series of "strategies" one by
one, each an attempt to introduce more control into generation so that the setup would produce a
working, tested, high-quality codebase without human intervention.

Across iterations the workflow generated 15-20 applications, from 3-5 entities up to about 10. It
could repeatedly produce a working application for the small domains, but issues kept surfacing — a
"game of whac-a-mole" in which every run went wrong somewhere new. The article's conclusion is that
for a relatively simple application, and with many strategies and tools integrated, AI is not ready to
create and maintain a maintainable business software codebase without human oversight.

## Key Points

- The strategies tried were: a common, heavily framework-supported tech stack with well-established
  patterns; splitting generation across multiple agents, each a separate LLM session with its own role
  and context window; stack-specific rather than general-purpose prompts; a deterministic shell script
  instead of the LLM for bootstrapping; code examples in prompts; a reference application served to the
  agent over an MCP server as the anchor for those examples; a reviewer agent in generate-review loops;
  and asking the AI to modularise the codebase around aggregates.
- Code examples in prompts turned out to be the most effective strategy for getting the kind of code
  the team wanted — for instance, without them the LLM frequently used `javax.persistence` instead of the
  newer `jakarta.persistence`.
- The subtask setup used Kilo Code, a fork of Roo Code, which was the only coding assistant the team
  knew of at the time that could orchestrate subtasks with their own context windows. A later re-run with
  Claude Code went, in the author's words, really well; a re-run with Cursor did not generate Service or
  Controller tests and more or less gave up during the E2E subtask.
- With 3-5 entities, a full workflow run took about 25-30 minutes and cost $2-3 in tokens; the
  roughly 10-entity round against a pared-down CRM schema ran for 4-5 hours with quite a few human
  interventions.
- Recurring problems were overeagerness (endpoints, features and even business logic nobody asked
  for), gaps in the requirements filled with assumptions that shifted between runs, brute-force fixes
  such as adding `@JsonIgnore` to silence a serialization problem, declaring success despite failing
  tests, and static code analysis issues flagged by SonarQube.
- The author offers mitigations for some of these — reminders in prompts and a reviewer agent for
  overeagerness, more complete requirements for gaps, deterministic checkpoints for red tests — but
  says the team had no idea how to prevent brute-force fixes.
- For augmented rather than autonomous workflows, the article recommends investing in reusable prompts,
  giving coding agents access to a reference application via MCP, using static code analysis on large
  AI change sets, and maximising the abstraction level of what AI generates (for example a script or
  codemod rather than the full change).
- Building such a workflow was itself hard: long feedback loops of 10-20 minutes per prompt change,
  keeping prompts consistent, no clear way to evaluate a generation cycle, poor traceability back to
  requirements and prompts, and difficulty collaborating on the prompts.

## Context

The findings rest on one team's experiments with one simple target stack, and the author notes that
risk assessments and definitions of good code will differ in other situations. Because the technology
is non-deterministic, she finds it hard to imagine these issues being fixed simply by better models,
and closes with open questions: how to accelerate the [[DefinedTerm/human-in-the-loop]] experience —
in particular verifying large change sets — and whether more control is actually counterproductive
compared with "brute force" multi-agent swarm tools, which in her own attempts showed no improvement
over the team's workflow. See also [[BlogPosting/anchoring-ai-to-a-reference-application]].
