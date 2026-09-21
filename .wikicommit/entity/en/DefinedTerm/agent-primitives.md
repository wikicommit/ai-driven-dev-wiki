---
title: "Agent Primitives"
type: "schema:DefinedTerm"
lang: en
tags: [agent-tooling, context-engineering, markdown, prompt-engineering]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/how-to-build-reliable-ai-workflows-with-agentic-primitives-and-context-engineering/'
    hash: sha256:f4175892bf17116173c4ae2a309b3b81b227800f09d53afa3ad1ade536e02a2d
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Reusable, configurable Markdown files that each give an AI agent one specific capability or rule — instructions, chat modes, prompts, specifications, memory and context helpers — proposed as the middle layer of a three-layer framework for making agent workflows repeatable. The term and the file set are one author's proposal on GitHub's blog, not a cross-vendor standard."
---

An agent primitive is a simple, reusable file or module that provides one specific capability or
rule for an AI agent. The term is proposed in
[[BlogPosting/how-to-build-reliable-ai-workflows-with-agentic-primitives-and-context-engineering]]
as the middle layer of a three-layer framework — Markdown prompt engineering underneath, context
engineering above — whose stated purpose is to turn ad-hoc prompting into a repeatable practice.
The primitives are ordinary Markdown files, and the argument attached to them is that writing a
perfect prompt by hand for every task is unsustainable, so the techniques that make a prompt work
should be committed to files instead.

The set the source names is six file types, each with its own suffix and scope: `.instructions.md`
for modular guidance with targeted scope, `.chatmode.md` for role-based expertise bounded by which
MCP tools the mode may use, `.prompt.md` for reusable workflows with built-in validation,
`.spec.md` for implementation-ready blueprints, `.memory.md` for knowledge preserved across
sessions, and `.context.md` for helpers that speed information retrieval. The source states that
VS Code natively supports the first three, and presents the other three as patterns its framework
adds.

## Usage

The primitives are meant to compose rather than to be used one at a time. The source's worked
example runs a request to implement secure user authentication through the whole set: a
`backend-dev` chat mode is selected, which auto-triggers `security.instructions.md` via an
`applyTo: "auth/**"` pattern, which loads context from a `.memory.md` section and a
`.context.md` file, generates a `user-auth.spec.md` from a structured template, and executes an
`implement-from-spec.prompt.md` workflow with validation gates. A `.prompt.md` file coordinating
several primitives this way is what the source calls an agentic workflow, and it states these are
designed to run in an IDE, a terminal or a CI pipeline alike.

Two design conventions carry most of the weight in that arrangement. Instructions are kept modular
rather than consolidated into one large file, with `applyTo` frontmatter patterns activating a file
only for matching paths — the source frames this as a
[[DefinedTerm/context-engineering]] measure, preserving context space for the work itself. Chat
modes are given only the MCP tools their domain needs, which the source presents as both a focus
measure and a security boundary, comparing it to professional licensing: an architect plans rather
than builds. Its named modes are architect, frontend engineer, backend engineer and technical
writer, each with an explicit statement of what it can and cannot do.

The source recommends building them in a fixed order — instructions, then chat modes, then reusable
prompts, then specification templates — and describes the intended payoff as accumulation: failures
captured in `.memory.md`, working patterns documented in `.instructions.md`, workflows refined in
`.prompt.md`, which it calls compound intelligence.

## When It Applies

The practice applies where the same kind of AI-assisted task recurs often enough that re-deriving
the prompt each time is wasteful, and where more than one person needs the same behaviour from the
agent. It assumes an agent that reads instruction files from the repository at all — the source's
examples are written for GitHub Copilot in VS Code, with files under `.github/instructions/`,
`.github/chatmodes/` and `.github/prompts/` — and, for the half of the framework about scaling, an
agent CLI runtime that can execute a prompt file outside the editor.

How it fails is stated indirectly, as the problem the third layer exists to solve: good primitives
still fail when irrelevant context competes for the model's limited attention, which is why the
source pairs them with session splitting, scoped instructions and mode boundaries rather than
treating the files alone as sufficient. The `applyTo` mechanism is what keeps an instruction file
from applying everywhere, and the source's warning against one massive instruction file is the
misapplication it names directly.

On how well-established the practice is: this is one author's proposal, published on GitHub's blog
in October 2025, and the source reports no evaluation of it. Three of the six file types are
conventions the author's framework introduces rather than formats VS Code recognizes natively, and
the tooling the source proposes for distributing them —
[[SoftwareApplication/apm-agent-package-manager]] — is the same author's project. See
[[DefinedTerm/agents-md]] and [[DefinedTerm/agent-skills]] for other file-based conventions
addressing a similar need.

## Related Terms

- [[DefinedTerm/context-engineering]] — the layer above, which the source pairs these with
- [[DefinedTerm/prompt-engineering]] — the layer below, which these are said to systematize
- [[DefinedTerm/agent-skills]] — another file-based convention for packaging agent capability
- [[DefinedTerm/agents-md]] — a file-based convention for standing instructions
- [[DefinedTerm/outer-loop]] — in this source's execution sense, where these files run outside the
  editor; that page records a second, unrelated sense of the same term
