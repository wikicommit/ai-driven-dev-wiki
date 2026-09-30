---
title: "AI Assisted Code Reviews - Augmenting Pull Requests in .NET Projects"
type: "schema:BlogPosting"
lang: en
tags: [code-review, pull-requests, prompt-engineering, dotnet]
sources:
  - type: url
    url: 'https://blog.nimblepros.com/blogs/ai-assisted-code-reviews/'
    hash: sha256:d598110e709e5704d3ee30f7f1c53682c0a41a3d3b860dfc0ec989ae35cd0621
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A NimblePros blog post arguing that AI should take the mechanical, rule-based part of code review so human reviewers can focus on architecture and intent, with a walkthrough of a small .NET bot that reviews GitHub pull requests through an LLM and advice on writing review prompts."
  author: ["Barret Blake"]
  datePublished: "2026-04-07"
  publisher: "NimblePros"
---

This post by Barret Blake, an architect at NimblePros, argues that AI cannot and should not replace
human developers in code review, but can take over much of its mechanical work — style, naming,
obvious bugs, null checks — so that human reviewers can concentrate on architecture, intent,
correctness and nuance. In the author's framing, AI does well at anything governed by clear, defined
rules, and struggles with judging whether business logic matches the work ticket and with
architectural fit, because it works within a limited context and cannot take in a whole codebase at
once.

After briefly surveying existing options — [[SoftwareApplication/github-copilot-code-review]], which
can be requested on a pull request in GitHub, and, for Azure DevOps, which has nothing equivalent out of the box,
custom extensions and workflows from the Azure DevOps Marketplace that use a tool such as OpenAI or
Claude — the post walks through a third option: building a
lightweight pull-request review bot in .NET. A GitHub webhook triggers the bot when a pull request is
opened or updated; it fetches the unified diff, truncates very large diffs, sends the diff with a
review prompt to an LLM, and posts the answer back as a non-blocking review comment labelled as an
automated review that still needs human review before merging. The post keeps the prompt logic
separate from the GitHub code so the prompt can be iterated on independently.

## Key Points

- AI is presented as best at rule- and pattern-based issues (naming, missing documentation, async
  pitfalls, unused variables, null-related issues, obvious bugs and security issues) and weak at
  checking business-logic correctness against requirements and at architectural judgement across a
  whole codebase.
- A generic "review this code" prompt, the author says, produces generic, nearly useless feedback;
  prompts should be tailored to the organisation and project, since what suits one .NET project type
  will not fully suit another or a React single-page app.
- The post names four keys to a strong pull-request review prompt: the stack context (language,
  framework, version and architecture pattern), an explicit list of what to review, an explicit list
  of what not to review, and the output format.
- Further customisations it suggests include separate prompts for specific concerns such as
  async/await correctness, a system prompt that carries the team's values and reviewing tone, and a
  different, higher-level prompt for draft pull requests.
- The author insists on keeping humans in the loop: reviewers should not rubber-stamp AI feedback,
  and logging which prompts produce good results is what makes an automated review useful over time.
- The post concludes that AI review is now a tool like a linter or test suite, and that code should
  no longer ship without an AI code review step alongside human review.

## Context

The post builds on the author's previous post, "Testing AI-Powered Features in .NET", which
introduced the chat service the review bot uses to send prompts to an LLM. It states its advice as
guidance and reports no measurements. Its heading "Keep Humans In The Loop" and its framing of AI as
an augmentation of human review rather than a replacement place it alongside other writing on
[[DefinedTerm/human-in-the-loop]] workflows.
