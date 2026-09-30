---
title: "Tool Design for AI Agents: Lessons from 50+ Claude Code Tools"
type: "schema:BlogPosting"
lang: en
tags: [tool-use, agent-tooling, prompt-caching, claude-code]
sources:
  - type: url
    url: 'https://codepointer.dev/p/tool-design-for-ai-agents-lessons'
    hash: sha256:798960d4831740d5de8d2d8de9ef9533000b374e32d6edc5fdbe5fa1c6862502
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A Code Pointer post that reads Claude Code's source to show how each of its 50+ tools carries its own prompt, assembled into the model-facing tool descriptions at runtime and locked per session, and draws design lessons for engineers building tool-use agents."
  author: ["Yongkyun Lee"]
  datePublished: "2026-04-02"
  publisher: "Code Pointer"
---

The post examines how [[SoftwareApplication/claude-code]] tells its model how to use its tools. Its
starting observation is that Claude Code's main system prompt covers tone, safety and behaviour but says
nothing about how to use any of the 50+ tools; instead each tool carries its own instructions in a
separate `prompt.ts` file, and those are assembled at request time into the `description` field of the
tool definitions sent through the Anthropic Messages API, alongside a `name` and a JSON Schema
`input_schema`.

The post traces that assembly through the code as a four-stage pipeline and then goes tool by tool,
quoting the prompt text and explaining what each line appears to guard against. It presents the result
as a set of patterns and takeaways for engineers building tool-use agents; the explanations of why a
given line exists are the author's reading of the code, sometimes explicitly speculative.

## Key Points

- Tool definitions pass through four stages: a registry that lists every tool, with many gated behind
  feature flags, user types or environment variables; filtering that removes tools the user has
  blanket-denied and, when tool search is on, deferred tools not yet discovered; schema rendering, which
  calls each tool's async `prompt()` method for its description and converts its Zod schema to JSON
  Schema; and caching, which locks the rendered schema for the session even if a feature flag flips
  mid-session.
- Because `prompt()` receives the other tools, agents and permissions as context, tools can refer to
  each other; the Bash tool's prompt, for example, steers the model to the dedicated Glob, Grep, Read and
  Edit tools instead of `find`, `grep`, `cat` or `sed`, and when search tools are embedded in the binary
  it drops Glob and Grep and stops telling the model to avoid `find` and `grep`.
- Prompts are built from live context: the Bash prompt serializes the current sandbox filesystem and
  network restrictions as JSON, and replaces user-specific temp paths with `$TMPDIR`, which the post
  explains as keeping prompt prefixes identical across users so they can share prompt-cache entries.
- Prompt complexity varies with the tool. The post contrasts Grep's static string with Bash's
  dynamically assembled prompt and suggests the gap roughly tracks how much damage each tool can do.
- The post describes internal and external users receiving different prompts — a short git section
  pointing to commit skills versus a full git safety protocol, an extra `old_string` minimality hint for
  the Edit tool, and a narrower encouragement to use plan mode.
- WebFetch passes fetched pages through a secondary model whose instructions depend on the domain:
  pre-approved domains get no quote limit, while all others get a strict 125-character cap on quotes.
- Several prompt lines are read as fixes for observed model habits: the WebFetch ban on reproducing song
  lyrics, which the post attributes to LLMs tending to reproduce copyrighted lyrics when asked; a ban on
  creating unrequested documentation files and on unrequested emoji in the Write tool; and the current
  month injected into the WebSearch prompt so the model does not search with a stale year.
- Keeping volatile content out of tool definitions is presented as a caching lesson: moving the agent
  list out of the Agent tool's description into a system-reminder message is reported, from a code
  comment, to address about 10.2% of fleet cache-creation tokens caused by tool-schema cache busts.
- Not every tool is loaded up front; deferred tools appear by name and the model calls ToolSearch to get
  their full schema, with MCP tools always deferred and a few tools never deferred.
- `CLAUDE_CODE_SIMPLE=1` keeps only Bash, Read and Edit, which the post reads as the three irreducible
  tools, and the default tool definition is conservative — not concurrency-safe and not read-only unless
  declared — so an incomplete tool definition fails safe rather than open.

## Context

The post is written for engineers designing tools for their own agents and uses Claude Code as a worked
example. Its claims about the code rest on the file paths and excerpts it quotes, and it states that
Anthropic has not published per-tool usage statistics, so its choice of four "core" tools is
illustrative. It connects to the wider writing on how tool definitions are presented to models —
[[DefinedTerm/tool-use-design-pattern]], [[DefinedTerm/tool-search]] and [[DefinedTerm/token-caching]].
