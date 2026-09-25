---
title: "Anchoring AI to a reference application"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, mcp, technical-debt]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/anchoring-to-reference.html'
    hash: sha256:b601ee397808d7ca15740ec6016dabb27ff69994f59a8f5677d5598aef271cb6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A September 2025 article by Birgitta Böckeler in the \"Exploring Gen AI\" series on martinfowler.com, describing an experiment that gives a coding agent a compilable reference application as its source of code samples and then uses that reference's commits to detect and close drift in a codebase built from it."
  author: ["Birgitta Böckeler"]
  datePublished: "2025-09-25"
  publisher: "martinfowler.com"
---

This article, part of the "Exploring Gen AI" series on martinfowler.com in which Thoughtworks
technologists record their explorations of generative AI for software development, starts from a
problem with service templates: they are meant to be role models that always carry an organisation's
current coding patterns and standards, but once a team has instantiated a service from one, feeding
later template updates back into that service is tedious. The author asks whether generative AI can
help, and reports an experiment built on a [[DefinedTerm/model-context-protocol]] server in front of a
reference application.

The experiment has two parts: using the reference application as the provider of code samples a
coding assistant works from, and then using it to find and close the places where an existing codebase
has drifted from it — the technique the article calls [[DefinedTerm/code-pattern-drift-detection]].

## Key Points

- Giving an LLM examples of the output wanted leads to better results, which the author calls a well
  established prompting practice — also known as few-shot prompting or in-context learning.
- Writing code samples inside a natural-language Markdown prompt file is tedious and gives no way to
  tell whether they compile or stay consistent with each other; keeping them in a reference application
  that can be compiled and run, like a service template, makes it much easier to give the AI
  compilable, consistent samples. In the author's experiment an MCP server gave a coding assistant
  access to such samples for a Spring Boot web application's repository, service and controller
  classes.
- Codebases generated from a template, with AI or otherwise, and then extended and maintained, often
  drift away from the reference application.
- Exposing the reference application's git commits through the same MCP server and asking the agent
  first to look for the actual changes in the reference let the author scope what drift the agent
  looked for. Without that step, asking the AI simply to compare the reference controllers with the
  existing ones produced many irrelevant comparisons; the author reports that commit scoping had a good
  impact, on a deliberately simple test change that added a logger and `log.debug` statements to the
  reference's controllers.
- The process ran in two steps: the AI first produced a drift report that the author could review and
  edit, removing irrelevant findings, and was then asked to write code closing the gaps the report
  identified.
- A change as simple as adding a logger or switching logging frameworks can be made deterministically
  by codemod tools such as OpenRewrite, which the author says to consider before reaching for AI. AI
  brings something new where closing the drift needs coding more dynamic than regular-expression-based
  codemod recipes allow — for example, turning a wide variety of non-standardised log messages into a
  structured format.

## Context

The article presents this as one experiment by its author, grown out of a larger experiment she had
written about earlier; its findings rest on that experiment and one simple example rather than on any
measurement. The example MCP server is published in the repository accompanying that earlier article.
