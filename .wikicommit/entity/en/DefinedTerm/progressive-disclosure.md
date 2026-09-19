---
title: "Progressive Disclosure"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview'
    hash: sha256:3f2567f8a7cd1948e582601407ccfd2804e66152973859636da7ba44f9ff235f
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A context-management strategy in which an agent loads information in stages as it is needed rather than all at once, so that material which is never used costs nothing. In Anthropic's Agent Skills it is realised as three levels: always-loaded metadata, instructions loaded on trigger, and bundled resources read only on demand."
---

Progressive disclosure is the practice of having an agent load information in stages as it becomes
needed, instead of placing everything in the context window up front. Anthropic's documentation
presents it as the property its filesystem-based [[DefinedTerm/agent-skills]] architecture enables,
and states its purpose plainly: to ensure only relevant content occupies the context window at any
given time.

## Usage

As documented for that format, the strategy is realised in three levels. **Metadata** — the `name`
and `description` from a Skill's YAML frontmatter — is always loaded, included in the system prompt
at startup at a stated cost of roughly 100 tokens per Skill, and is what a request is matched
against. **Instructions** — the body of `SKILL.md` — are read from the filesystem only once a request
matches, at a stated budget of under 5,000 tokens. **Resources** — additional markdown files,
reference material and executable scripts — cost nothing until accessed, with reference files
entering context when read and scripts contributing only their output.

The documented consequences follow from that staging. Many Skills can be installed without a context
penalty, because an untriggered Skill occupies only its name and description. A Skill may bundle
dozens of reference files while a given task loads only the one it needs, the rest staying on disk at
zero cost. And scripts are more efficient than having the model generate equivalent code, since the
code itself never enters the context window — the documentation's example being a validation script
whose entire contribution is a short pass or error message.

## When It Applies

The strategy applies where a large body of guidance or reference material exists but only a small
part of it is relevant to any given task. It assumes two things: that the material can be split so
that a cheap, always-loaded summary is enough to decide whether the expensive part is needed, and
that the agent can fetch the rest on demand — in the documented case, a filesystem it can read with
shell commands.

Its failure mode is in that first assumption. Because the always-loaded description is the only
basis for deciding whether to load the rest, a description that does not say both what the material
does and when to use it leaves the deeper levels unreachable in practice; the same documentation
makes stating both a requirement of the field for exactly this reason.

How well-established it is: the account available here is one vendor's documentation of its own
format, where the term names a specific three-level arrangement with stated token costs.

## Related Terms

- [[DefinedTerm/agent-skills]] — the format this strategy is documented as underpinning
- [[DefinedTerm/context-engineering]] — the broader practice of managing what occupies a context window
- [[DefinedTerm/just-in-time-context-retrieval]] — a closely related approach to deferring retrieval
- [[DefinedTerm/compaction]] — a different response to the same constraint, reducing context already accumulated
