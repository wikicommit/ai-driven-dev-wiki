---
title: "Continuous AI in practice: What developers can automate today with agentic CI"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, ci-cd, agent-safety]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/generative-ai/continuous-ai-in-practice-what-developers-can-automate-today-with-agentic-ci/'
    hash: sha256:994d27bdd399c24187602b4764046df3b5e7b67fb9de1d565cff3b8821304ac3
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "GitHub's 5 February 2026 post introducing Continuous AI, a pattern in which background agents run in a repository the way CI jobs do but for tasks requiring judgment rather than rules. It sets out the safety model, the case for natural language alongside YAML, and the seven categories GitHub Next reports having tested in real repositories."
  author: ["GitHub Staff"]
  datePublished: "2026-02-05"
  publisher: "GitHub"
---

This post introduces [[DefinedTerm/continuous-ai]], a pattern GitHub Next has been exploring in
which background agents operate in a repository the way CI jobs do, but only for tasks that require
reasoning instead of rules. Its argument opens by conceding that continuous integration is not
failing — it is doing exactly what it was designed to do, handling work that can be expressed
deterministically, where a test passes or fails and a build succeeds or does not.

The gap it identifies is work that depends on understanding intent. The examples given are a
docstring that says one thing while the implementation says another, text that passes accessibility
linting but still confuses users, a dependency that adds a flag and changes behavior without a major
version bump, a regex compiled inside a loop, and UI behavior visible only through interaction. The
post quotes Idan Gazit, head of GitHub Next, that any task requiring judgment goes beyond
heuristics, and that anywhere something cannot be expressed as a rule or a flow chart is where AI
becomes helpful.

## Key Points

- The pattern is summarized in one line: natural-language rules plus agentic reasoning, executed
  continuously inside the repository.
- It is explicitly not positioned as a product or a CI replacement — the post states that traditional
  CI remains essential and that natural language complements YAML rather than replacing it. Where a
  problem can be expressed deterministically, extending CI is called exactly the right approach.
- Safety is described as a first principle of the design. Agents operate read-only by default and
  cannot create issues, open pull requests or modify content unless explicitly permitted — the
  mechanism the post calls [[DefinedTerm/safe-outputs]].
- The model assumes agents can fail or behave unexpectedly: outputs are sanitized, permissions are
  explicit, activity is logged and auditable, and the blast radius is described as deterministic.
- Developers are kept in the loop by design. Agentic workflows are said not to make autonomous
  commits; they produce the same artifacts developers would, and the post states that agents do not
  merge code and everything remains visible and reviewable. Pull requests are described as the most
  common output because, in Gazit's words, the PR is the existing noun where developers expect to
  review work.
- The post pushes back on brevity as a measure of these workflows, stating that developers rarely
  author them in a single pass and instead collaborate with an agent to refine intent, add
  constraints and define acceptable outputs.
- Seven categories are presented under the claim that these are not theoretical examples and that
  GitHub Next has tested the patterns in real repositories: reconciling documentation with behavior;
  generating recurring project reports that synthesize across issues, pull requests, commits and CI
  results; keeping translations current by regenerating them when source text changes and opening a
  single pull request; detecting dependency drift; automated test-coverage burn down; background
  performance improvements; and automated interaction testing using agents as play-testers.
- The dependency-drift demo is described as an agent installing dependencies, inspecting CLI help
  text, diffing it against previous days, finding an undocumented flag and filing an issue before
  maintainers noticed — which the post says requires semantic interpretation rather than just diffs,
  and is why classical CI cannot handle it.
- The test-coverage category is the one carrying reported figures: in one experiment coverage went
  from about 5% to near 100%, with more than 1,400 tests written across 45 days for about $80 worth
  of tokens, the agent producing small daily pull requests so developers reviewed incrementally.
- The performance example is a regex compiled inside a function call so that it recompiles on every
  invocation, which an agent recognizes, rewrites to pre-compile, and opens a pull request explaining.
- The interaction-testing category is described as using agents to play a simple platformer
  thousands of times to detect UX regressions, with the post arguing the pattern generalizes to
  onboarding flows, multi-step forms, retry loops, input validation and accessibility patterns.
- On the translation case the post is candid that machine translations might not be perfect out of
  the box, arguing the value is a draft ready for review rather than a finished result.

## Context

The post is GitHub's account of its own research prototype, which it describes as using a
deliberately simple pattern: write an agentic workflow, compile it into a GitHub Action, push it,
and let it run on any Actions trigger. Its categories are presented as tested
in real repositories rather than theoretical; most are described without measurements, the
test-coverage experiment being the one reported with figures. Gazit is quoted framing the shift in
eras — the first era of AI for code being about code generation, the second about taking
cognitively heavy chores off developers — and inviting readers to consider which parts of their work
they want to retain: their judgment, their taste.
