---
title: "Shell + Skills + Compaction: Tips for long-running agents that do real work"
type: "schema:BlogPosting"
lang: en
tags: [agent-tooling, long-running-agents, agent-safety]
sources:
  - type: url
    url: 'https://developers.openai.com/blog/skills-shell-tips'
    hash: sha256:6cf194fe210d3406a52b938f8a74c09532aca483271de8328b4ccf2f8a059335
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An OpenAI developer blog post on combining three agentic primitives in the Responses API — skills, a hosted shell tool and server-side compaction — for long-running agents, with ten practical tips and three build patterns drawn from OpenAI's own work and from an early skills customer."
  author: ["Charlie Guo"]
  datePublished: "2026-02-11"
  publisher: "[[Organization/openai]]"
---

This post on [[Organization/openai]]'s developer blog introduces a set of what it calls agentic
primitives for long-horizon work in the Responses API, and then concentrates on the non-obvious
patterns it says have worked best so far, both inside OpenAI and in production at Glean, which it
describes as an early skills customer. The three primitives are skills — reusable, versioned
instructions, aligned with the [[DefinedTerm/agent-skills]] open standard, that can be mounted into
containers — an upgraded shell tool running in an OpenAI-hosted container with controlled internet
access, and server-side [[DefinedTerm/compaction]], which compresses conversation history
automatically so a long run does not hit the context limit.

The post's framing is that the three are complementary: skills move stable procedures and examples
out of the system prompt into a reusable bundle, the shell provides a full execution environment for
installing code, running scripts and writing outputs, and compaction preserves continuity across a
long run. Its summary of the division of labour is that skills encode the how, the shell executes
the do, and compaction keeps long runs coherent.

## Key Points

- A skill is described as a bundle of files plus a `SKILL.md` manifest; the platform exposes each
  skill's `name`, `description` and `path` to the model, which uses that metadata to decide whether
  to invoke the skill and then reads `SKILL.md` for the full workflow.
- Compaction is offered two ways: server-side compaction, which runs automatically in-stream once
  context crosses a threshold, and a standalone `/responses/compact` endpoint for explicit control
  over when compaction happens.
- A skill's description should be written like routing logic rather than marketing copy — saying
  when to use it, when not to, and what its outputs and success criteria are.
- Making skills available can initially reduce correct triggering; the post recommends explicit
  "don't call this skill when…" negative examples and edge-case coverage in descriptions. Its
  evidence is Glean's report that skill-based routing initially dropped triggering by about 20% in
  targeted evals and recovered after those were added.
- Templates and worked examples belong inside the skill rather than in the system prompt, because
  they load only when the skill is invoked and do not inflate tokens for unrelated queries; Glean is
  reported as attributing some of its biggest quality and latency gains in production to this.
- For long runs, the post recommends reusing the same container across steps, passing
  `previous_response_id` to continue in the same thread, and treating compaction as a default
  long-run primitive rather than an emergency fallback.
- By default the model decides when to use a skill; where a production workflow needs determinism,
  the post advises telling the model explicitly to use a named skill.
- Combining skills with open network access is described as a high-risk path for data exfiltration.
  The suggested default posture allows skills and shell but enables networking only with a minimal
  per-request allowlist for narrowly scoped tasks, treating tool output as untrusted (see
  [[DefinedTerm/guardrails]]).
- Network allowlists are two-layered: an admin-configured org-level allowlist sets the maximum set of
  destinations, and a request-level `network_policy` must be a subset of it, with a request naming
  domains outside the org allowlist returning an error. For authenticated calls, `domain_secrets`
  lets the model see only placeholders while a sidecar injects real credentials for approved
  destinations.
- `/mnt/data` is recommended as the handoff boundary for artifacts in hosted-shell workflows — in the
  post's phrasing, tools write to disk, models reason over disk, and developers retrieve from disk.
- Skills work with both the hosted shell and a local shell mode in which the developer executes
  `shell_call` and returns `shell_call_output`, so the post suggests iterating locally and moving to
  hosted containers for repeatability and isolation while keeping skills the same across both.
- Three build patterns are given: install dependencies, fetch data and write an artifact; encode a
  workflow in a skill and mount it into the shell so the agent produces artifacts deterministically;
  and, as an advanced pattern, use skills as carriers of enterprise workflows — for which the post
  cites Glean's report that a Salesforce-oriented skill raised eval accuracy from 73% to 85% and cut
  time-to-first-token by 18.1%.

## Context

The post is a vendor's guidance for its own platform, and its quantitative evidence is limited to
figures attributed to a single customer, Glean, without a described evaluation method. Its closing
image — skills becoming living standard operating procedures, updated as an organization evolves and
executed consistently by agents — is presented as where the approach is heading rather than as a
measured outcome. It sits alongside other accounts in this wiki of equipping
[[DefinedTerm/long-running-agent]]s with skills and context management, such as the loading behaviour
described under [[DefinedTerm/progressive-disclosure]].
