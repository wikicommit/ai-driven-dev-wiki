---
title: "Agentic Engineering Patterns"
type: "schema:CreativeWorkSeries"
lang: en
tags: [agentic-engineering, coding-agents, design-patterns]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Feb/23/agentic-engineering-patterns/'
    hash: sha256:2e0749860bb2041b583e646cdfe9ae5c095aa1e10ca0a52b54ac9fbcf3fcb72b
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/'
    hash: sha256:82427000ff79e2ae15e0d63780b17b5d0cc29168bf8875648c41d0828ac03166
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/what-is-agentic-engineering/'
    hash: sha256:5887de1aff52ec544bd35326f452d4de9e1c58a331298d155e4a1c9f23c87af6
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A chapter-shaped guide by Simon Willison, begun in February 2026, collecting patterns for getting the best results out of coding agents. Its chapters are published in a format designed to be updated over time rather than frozen at first publication."
  about: "[[DefinedTerm/agentic-engineering]]"
  author: ["Simon Willison"]
  url: "https://simonwillison.net/guides/agentic-engineering-patterns/"
  startDate: "2026-02-23"
  creativeWorkStatus: "Chapters continue to be added; the guide describes itself as a work in progress"
---

Agentic Engineering Patterns is a collection of practices for getting the best results out of coding
agents such as Claude Code and OpenAI Codex, published on Simon Willison's blog from February 2026.
It is organised as a sequence of chapters, each a self-contained pattern. The post introducing it
states the goal as producing something that helps answer the question "how do I get good results out
of this stuff" all in one place, against a body of the author's own existing writing on AI-assisted
programming that he describes as relatively unstructured.

Its form is the part its author treats as novel. He describes the collection as not exactly a book
but "kind of book-shaped", and publishes it using a shape of content he calls a *guide*: a collection
of chapters, where a chapter is effectively a blog post with a less prominent date, designed to be
updated over time rather than frozen at the point of first publication. He presents guides and
chapters as his answer to publishing evergreen content on a blog, a problem he reports having been
trying to solve for a while. That format — rather than any single publication event — is why the
collection is recorded here as a series.

Its stated debt is to the chapter-shaped pattern format popularized by the software design-patterns
literature of the 1990s, which the introduction post describes as a loose inspiration rather than a
model followed closely. See [[BlogPosting/writing-about-agentic-engineering-patterns]] for the post
that introduced the project.

## Scope & Structure

The guide's chapters are grouped under six headings. **Principles** holds "What is agentic
engineering?", "Writing code is cheap now", "Hoard things you know how to do", "AI should help us
produce better code", and "Anti-patterns: things to avoid". **Working with coding agents** holds "How
coding agents work", "Using Git with coding agents", and "Subagents". **Testing and QA** holds
"Red/green TDD", "First run the tests", and "Agentic manual testing". **Understanding code** holds
"Linear walkthroughs" and "Interactive explanations". **Annotated prompts** holds two worked examples,
and an **Appendix** collects prompts the author reuses.

The project began with the two chapters published alongside its announcement — "Writing code is cheap
now" and "Red/green TDD" — with a stated intended cadence of one to two chapters a week. The author
says he does not really know when he will stop, because there is a lot to cover.

## Status

The guide's opening chapter describes the project as very much a work in progress, like the field it
attempts to cover, and states that no chapter should be considered finished: the author says he will
continue adding chapters as new techniques emerge and will update existing ones as understanding of
the patterns evolves. The editorial goal stated there is to identify and describe patterns for working
with these tools that demonstrably get results and that are unlikely to become outdated as the tools
advance.

Its stated editorial constraint is that the prose is written by the author rather than generated: he
holds a strong personal policy against publishing AI-generated writing under his own name, and says it
will hold for this project, while using LLMs for proofreading, fleshing out example code, and other
side tasks.

## Related

[[DefinedTerm/agentic-engineering]], [[DefinedTerm/ai-coding-agent]], [[DefinedTerm/vibe-coding]],
[[BlogPosting/writing-about-agentic-engineering-patterns]]
