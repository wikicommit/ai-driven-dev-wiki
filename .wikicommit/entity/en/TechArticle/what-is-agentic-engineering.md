---
title: "What is agentic engineering?"
type: "schema:TechArticle"
lang: en
tags: [agentic-engineering, coding-agents, terminology, guide]
sources:
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/what-is-agentic-engineering/'
    hash: sha256:e6c2c65056d73b991e32cf28fde817d0bb3d43f3a9824b25ae882a93a180b6a6
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The opening chapter of Simon Willison's Agentic Engineering Patterns guide, defining agentic engineering, coding agents and agents, and distinguishing the practice from vibe coding."
  author: ["[[Person/simon-willison]]"]
  datePublished: "2026-03-15"
  publisher: ""
  proficiencyLevel: "Beginner"
---

This is the opening chapter of *Agentic Engineering Patterns*, a guide whose stated goal is to identify and describe patterns for working with coding agents that demonstrably get results and are unlikely to become outdated as the tools advance. The chapter's job is definitional: it establishes what the author means by [[DefinedTerm/agentic-engineering]], by [[DefinedTerm/coding-agent]], and by "agent," and separates the practice from [[DefinedTerm/vibe-coding]].

## Key Practices

**The definitions, in order.** *Agentic engineering* is "the practice of developing software with the assistance of coding agents." *Coding agents* are agents that can both write and execute code, with Claude Code, OpenAI Codex and Gemini CLI given as popular examples. And *agent* takes the definition the author says he has come to accept in the LLM field: **agents run tools in a loop to achieve a goal** — software that calls an LLM with a prompt and a set of tool definitions, calls whatever tools the LLM requests, and feeds the results back. He notes that defining the word has frustrated AI researchers since at least the 1990s.

**Code execution is identified as the defining capability.** Without the ability to run the code, anything an LLM outputs is of limited value; with it, agents can iterate toward software that demonstrably works.

**What is left for humans** is the chapter's central argument: writing code was never the sole activity of a software engineer, and the craft has always been figuring out *what* code to write. Any problem has dozens of potential solutions with different tradeoffs, and navigating those to fit a specific set of circumstances and requirements is the job. Practically, that means supplying agents with the tools they need, specifying problems at the right level of detail, and verifying and iterating until the results are robust and credible.

**Learning is relocated from the model to the harness.** The chapter's formulation is that LLMs do not learn from their past mistakes, but coding agents can — provided the human deliberately updates instructions and tool harnesses to reflect what was learned.

**The distinction from vibe coding** is stated as a deliberate defence of the original definition. Vibe coding was coined in February 2025 to describe prompting LLMs to write code while you "forget that the code even exists," and the chapter records that this was coincidentally three weeks before the original release of Claude Code. Extending the term to cover any LLM-produced code is called a mistake, on the grounds that a term is needed for unreviewed, prototype-quality LLM-generated code that distinguishes it from code the author has brought to a production-ready standard.

## Scope & Caveats

The chapter states plainly that the guide is a work in progress, that no chapter should be considered finished, and that existing chapters will be updated as understanding evolves. Its own page records a creation date of 15 March 2026 and a last-modified date one day later.

Its position within the guide places this chapter first among five under "Principles," ahead of sections on working with coding agents, testing and QA, understanding code, annotated prompts, and an appendix of prompts.
