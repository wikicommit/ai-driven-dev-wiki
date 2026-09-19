---
title: "Closing the knowledge gap with agent skills"
type: "schema:BlogPosting"
lang: en
sources:
  - type: url
    url: 'https://developers.googleblog.com/closing-the-knowledge-gap-with-agent-skills/'
    hash: sha256:99da78c38e52825287d818db6e10f2cf2d633b7e9479102298bccb809800d651
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [agent-skills, context-engineering, evaluation, agent-tooling]

properties:
  description: "A Google for Developers post reporting how a Gemini API agent skill was built and evaluated against a 117-prompt harness, and what the results say about when skills help."
  author: ["Philipp Schmid", "Mark McDonald"]
  datePublished: "2026-03-25"
  publisher: "[[Organization/google]]"
---

A Google for Developers post arguing that language models have fixed knowledge from a
training cut-off while software engineering practice moves quickly, leaving a gap the
model cannot close on its own. The authors give examples they observe at Google DeepMind:
their models do not know about themselves at training time, and are not necessarily aware
of subtle changes in best practices or of SDK changes. They position
[[DefinedTerm/agent-skills]] as a lightweight recent approach to that gap, among the many
solutions the authors say already exist, from web search tools to dedicated MCP services.

Rather than approaching the problem as model builders, the authors set out to show what
any SDK maintainer can do, and report on building a Gemini API developer skill (see
[[SoftwareApplication/gemini-api-developer-skill]]) and measuring its effect. The post's
contribution is the measurement: an evaluation harness the authors built for the purpose,
and a set of results that they read as showing skills work but depend on the model's
reasoning ability.

## Key Points

- The authors frame the problem as a knowledge gap created by fixed training cut-offs
  against fast-moving library and best-practice change, and report observing it at Google
  DeepMind in their own models' unawareness of themselves and of SDK changes.
- The skill they built explains the API's high-level feature set, describes current models
  and SDKs per language, demonstrates basic sample code for each SDK, and lists
  documentation entry points as sources of truth — a design the authors describe as
  primitive instructions that also push the agent to retrieve fresh information from the
  documentation rather than relying on what the skill states.
- They built an evaluation harness of 117 prompts generating Python or TypeScript code
  against the Gemini SDKs, spanning agentic coding tasks, chatbots, document processing,
  streaming content and specific SDK features. A prompt counts as a failure if the
  generated code uses one of their old SDKs.
- Tests were run both "vanilla" (prompting the model directly) and with the skill enabled;
  in the skill condition the model was given the same system instruction the Gemini CLI
  uses plus two tools, `activate_skill` and `fetch_url`.
- The headline result the authors report is that the Gemini 3 series achieves excellent
  results once the skill is added, starting from a low baseline *without* it — the
  without-skill figures they give are 6.8% for both 3.0 Pro and Flash and 28% for 3.1 Pro —
  while the older 2.5 series benefits far less. The authors read this as showing that
  strong reasoning support is what makes the difference. These are the authors' own
  measurements of their own skill against their own SDKs, and the post states the
  with-skill figures only in a chart.
- Across domains the skill helped for almost all categories on the best-performing model
  (`gemini-3.1-pro-preview`), with SDK Usage lowest at a 95% pass rate; the authors report
  no stand-out reason, noting the failures include prompts that explicitly request Gemini
  2.0 models.
- The post names two limitations. Citing Vercel's work, the authors note that direct
  instruction through `AGENTS.md` can be more effective than skills, and say they are
  exploring other ways to supply live SDK knowledge, such as MCPs for documentation.
- The second limitation is maintenance: the authors state there is no good skill update
  story beyond asking users to update manually, and warn that this could in the long term
  leave stale skill information in users' workspaces, doing more harm than good.

## Context

This is a vendor's account of its own skill, evaluated against its own SDKs with a harness
the same authors wrote, and the failure criterion — using an old Google SDK — is defined
in terms of the vendor's own product line. The comparison is between a model with and
without the skill, not between skills and the alternatives the post mentions, so the
post's own pointer to Vercel's contrary finding about `AGENTS.md` is not something it
tests here.

The maintenance problem the authors raise is a distinct concern from the knowledge gap the
skill addresses, and cuts against it: a mechanism introduced to keep an agent current can
itself go stale in a user's workspace. The broader practice of supplying an agent with
standing, file-based instructions is covered by [[DefinedTerm/agents-md]], and the
underlying concern by [[DefinedTerm/context-engineering]].
