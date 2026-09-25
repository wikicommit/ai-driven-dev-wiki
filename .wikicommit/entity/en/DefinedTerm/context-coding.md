---
title: "Context Coding"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, context-engineering, terminology]
sources:
  - type: url
    url: 'https://guangzhengli.com/blog/zh/vibe-coding-and-context-coding'
    hash: sha256:1fb990c1b96d538c33025bac005806f001ffce5a54b8a29877454d271c67a3dd
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A name proposed in a 2025 practitioner's blog post for AI-assisted programming in general, as distinct from vibe coding, on the view that beyond the model's own capability its progress comes from supplying the LLM with more suitable context."
---

Context Coding — glossed by the post that proposes it as programming based on, or driven by, context
— is a name one practitioner's blog post puts forward for AI-assisted programming in general, as
distinct from [[DefinedTerm/vibe-coding]] in its original, narrow sense of programming purely through
conversation without reading the code. As [[BlogPosting/ai-coding-tools-evolution-and-vibe-coding]]
argues, apart from the models themselves getting better at programming, the other major source of
progress in AI programming has been the [[DefinedTerm/context-engineering]] of the tools, so that,
with the model held fixed, every improvement in AI-assisted programming rests on passing the LLM more
suitable context — whether through chat, RAG, rules, MCP or whatever comes next.

## Usage

The post uses the name to read the recent history of coding tools as a sequence of context strategies.
[[SoftwareApplication/github-copilot]] brought the code in the open editor window and around the cursor
to the model; [[SoftwareApplication/cursor]] added retrieval over an index of the whole codebase and
let users attach files and folders themselves; [[SoftwareApplication/claude-code]] analyses a project's
overall structure first and then searches with Unix tools such as grep rather than a vector index. The
post names other advances too — stronger models, and Cursor's dedicated Tab-completion model — but
reads the success of these products as resting on better context engineering: what context each tool
put in front of the model, and how much control it gave the user over that.

Applied to a developer's own practice, the post takes a new team member's onboarding as the model for
what context to supply: the technology stack, directory structure and meaning of file names, the
project's common commands, the location of shared utilities and core modules, and the team's coding
conventions — kept in an instruction file such as `CLAUDE.md` or `.github/copilot-instructions.md`,
since the model starts every session with no memory. It extends the same reasoning to current
documentation fetched through MCP and to debugging, where the model is asked to add logging so that it
sees what a developer would see in a debugger.

## When It Applies

In the post, Context Coding is the author's name for AI-assisted programming that is not vibe coding in
Karpathy's narrow sense — where the AI's code is no longer reviewed and only the result is judged. The
advice it gives depends on the instruction files that hold this context being kept current.

The post names two ways it goes wrong. Context is not better the more there is of it: information that
goes out of date — directory layouts, frequently refactored files and utilities — without being updated
in the instruction files does more harm than not supplying it at all, and keeping those files current
is hard, especially for large teams. And no amount of context yet makes up for the model's weakness at
abstraction: even with every coding convention written into the rules, the author does not expect an
LLM to reliably produce code at a good level of abstraction.

How established it is: the name is one author's proposal, made in a personal blog post, and supported
by that author's own experience with three tools rather than by any measurement. The post presents it
as a preferred label for a practice already widely followed, not as a new technique.

## Related Terms

- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/vibe-coding]]
- [[DefinedTerm/ai-assisted-programming]]
- [[DefinedTerm/context-driven-engineering]] — a similarly named practice from a different source
