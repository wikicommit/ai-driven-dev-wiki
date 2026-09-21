---
title: "Progressive Disclosure"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview'
    hash: sha256:3f2567f8a7cd1948e582601407ccfd2804e66152973859636da7ba44f9ff235f
  - type: url
    url: 'https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills'
    hash: sha256:e884d6fd1fe5becb8f432c99a20cf8b36e39d087e507037696b411e11d077ef5
  - type: url
    url: 'https://arxiv.org/pdf/2603.05344'
    hash: sha256:29a5dfd46c7505affc599f6922ebba2f67d01e7f3a343df5347a42f435a08edc
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A context-management strategy in which an agent loads information in stages as it is needed rather than all at once, so that material which is never used costs nothing. It is realised as a cheap always-loaded index over expensive content fetched on demand — three levels of metadata, instructions and bundled resources in Anthropic's Agent Skills, and keyword-searched tool discovery for external tools in OpenDev."
---

Progressive disclosure is the practice of having an agent load information in stages as it becomes
needed, instead of placing everything in the context window up front. Anthropic's documentation
presents it as the property its filesystem-based [[DefinedTerm/agent-skills]] architecture enables,
and states its purpose plainly: to ensure only relevant content occupies the context window at any
given time. The same vendor's engineering account of that format
([[BlogPosting/equipping-agents-for-the-real-world-with-agent-skills]]) goes further and names it the
core design principle that makes the format flexible and scalable, offering the analogy of a
well-organized manual that opens with a table of contents, then specific chapters, and finally a
detailed appendix.

## Usage

As documented for that format, the strategy is realised in three levels. **Metadata** — the `name`
and `description` from a Skill's YAML frontmatter — is always loaded, included in the system prompt
at startup at a stated cost of roughly 100 tokens per Skill; of those two fields the documentation
names the `description` as what a request is matched against when deciding whether to trigger the
Skill. **Instructions** — the body of `SKILL.md` — are read from the filesystem only once a request
matches, at a stated budget of under 5,000 tokens. **Resources** — additional markdown files,
reference material and executable scripts — cost nothing until accessed, with reference files
entering context when read and scripts contributing only their output.

The engineering post traces the same three levels through one request. The context window begins with
the core system prompt, the metadata of every installed skill, and the user's message; the agent then
triggers the relevant skill by invoking a Bash tool to read that skill's `SKILL.md`; it chooses to read
a further bundled file — in the post's example, the `forms.md` shipped alongside a PDF skill — and only
then proceeds with the task. The decision to read the third-level file is described as the agent's own,
made because the instructions it has just loaded refer to it.

The documented consequences follow from that staging. Many Skills can be installed without a context
penalty, because an untriggered Skill occupies only its name and description. A Skill may bundle
dozens of reference files while a given task loads only the one it needs, the rest staying on disk at
zero cost. And scripts are more efficient than having the model generate equivalent code, since the
code itself never enters the context window — the documentation's example being a validation script
whose entire contribution is a short pass or error message, and the engineering post's a script that
reads a PDF and extracts its form fields without either the script or the PDF being loaded. Because an
agent equipped with a filesystem and code execution never has to read a skill in full, that post states
the material bundled into one is effectively unbounded.

## When It Applies

The strategy applies where a large body of guidance or reference material exists but only a small
part of it is relevant to any given task. It assumes two things: that the material can be split so
that a cheap, always-loaded summary is enough to decide whether the expensive part is needed, and
that the agent can fetch the rest on demand — in the documented case, a filesystem it can read with
shell commands.

Its failure mode is in that first assumption. Because the always-loaded description is the only
basis for deciding whether to load the rest, a description that does not say both what the material
does and when to use it leaves the deeper levels unreachable in practice; the same documentation
makes stating both a requirement of the field for exactly this reason. The engineering post reaches the
same point from the author's side, advising particular attention to a skill's `name` and `description`
because they are what the agent uses in deciding whether to trigger it.

The authoring judgment the strategy demands is where to place the split. That post's guidance gives
length as the trigger — split a `SKILL.md` into separate referenced files once it has become unwieldy —
and adds that where contexts are mutually exclusive or rarely used together, keeping those paths
separate reduces token usage. Size prompts the division; which material is needed together guides
where it falls.

How well-established it is: two independent accounts are available here, and they differ in kind. One
vendor's documentation and engineering writing about its own format supplies the three-level
arrangement and its stated token budgets but reports no measurement of the strategy's effect. The
OpenDev report supplies the measurement and no such staged format, and is itself a single system's
design report written by its author rather than a controlled comparison. Neither account is a
general evaluation of the strategy.

## Another Realisation

The strategy is not tied to a document format.
[[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] applies the same staging to
an agent's *tools*, and reports a figure for it. That report frames the problem in tokens: a system
with a hundred external tools whose schemas average two hundred tokens spends twenty thousand tokens
on tool definitions alone, so including every schema is wasteful while excluding external tools
limits what the agent can do. [[SoftwareApplication/opendev]]'s answer is lazy discovery — the
context starts with zero external tool schemas, and the agent calls a `search_tools` tool that scores
registered tool names and descriptions against a keyword query and returns matches, whose schemas
then enter subsequent calls. Three detail levels let the agent choose how much context to spend on
the answer, and invoking a tool by its qualified name discovers it without a prior search. The report
states that eagerly including every external schema had consumed up to 40% of the context before the
first user message, and that lazy discovery brought that baseline to under 5%, growing only as
capabilities are actually used.

That report applies the same two-phase treatment to its own skills — a metadata index of name,
description and trigger conditions at startup, with full content loaded only on invocation — and
generalises the pattern as a lesson, that eager loading fails at scale and the answer in both cases
is to load metadata indexes at startup and defer full content to the point of use. The trade it names
is the one implicit in the documented format as well: discovery costs an extra round trip, which pays
off for workflows using few of the available items and accumulates, though bounded, for workflows
using many.

## Related Terms

- [[DefinedTerm/agent-skills]] — the format this strategy is documented as underpinning
- [[DefinedTerm/context-engineering]] — the broader practice of managing what occupies a context window
- [[DefinedTerm/just-in-time-context-retrieval]] — a closely related approach to deferring retrieval
- [[DefinedTerm/compaction]] — a different response to the same constraint, reducing context already accumulated
