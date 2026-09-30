---
title: "Guides and sensors"
type: "schema:DefinedTerm"
lang: en
tags: [harness-engineering, coding-agents, verification]
aliases: ["Feedforward and feedback controls"]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html'
    hash: sha256:cf7369071f56e7b3b36f7b003d612f4aa69fef17a7135ba19f2e22f2ad7e1cc6
  - type: url
    url: 'https://martinfowler.com/articles/harness-engineering.html'
    hash: sha256:cf7369071f56e7b3b36f7b003d612f4aa69fef17a7135ba19f2e22f2ad7e1cc6
  - type: url
    url: 'https://martinfowler.com/articles/sensors-for-coding-agents.html'
    hash: sha256:f44d1ed873c9fc6ebc9d49f6d0ade56e0951706724aeb8b70a4d63de4064e2da
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "In Birgitta Böckeler's model of a coding agent's user harness, guides are feedforward controls that steer the agent before it acts and sensors are feedback controls that observe its output afterwards so it can self-correct; each is either computational or inferential."
---

Guides and sensors are the two kinds of control in the model of a coding agent's outer harness that
Birgitta Böckeler proposes in [[BlogPosting/harness-engineering-for-coding-agent-users]].
**Guides** (feedforward controls) anticipate the agent's behaviour and aim to steer it *before* it
acts, increasing the probability of a good result on the first attempt. **Sensors** (feedback
controls) observe *after* the agent acts and help it self-correct. Each can be of one of two execution
types: **computational** — deterministic and fast, run by the CPU, such as tests, linters, type
checkers and structural analysis — or **inferential** — semantic analysis, AI code review or
[[DefinedTerm/llm-as-a-judge]], typically run on a GPU or NPU, slower, more expensive and more
non-deterministic.

## Usage

The article's examples pair the two axes: coding conventions in [[DefinedTerm/agents-md]] or skills
are inferential guides; a tool with access to OpenRewrite recipes is a computational guide; a hook
running ArchUnit tests against module boundaries is a computational sensor; and skills holding review
instructions are inferential sensors. Sensors are described as particularly powerful when their
signals are optimised for LLM consumption, such as custom linter messages that include instructions
for the fix — which the author calls a positive kind of prompt injection.

Computational sensors are cheap and fast enough to run on every change alongside the agent, while
inferential controls add richer guidance and semantic judgment at a cost. The model has humans steer
the agent by improving the guides and sensors whenever an issue recurs, and places sensors across the
change lifecycle according to their cost — fast ones before integration, more expensive ones after it,
and some running continuously against the codebase or at runtime.

In a practical follow-up, [[BlogPosting/maintainability-sensors-for-coding-agents]], the same author
reports applying sensors to keep an AI-built application maintainable while deliberately using hardly
any guides. Computational sensors — linting with custom self-correction messages, dependency rules, and
mutation testing as a check on the test suite — impressed her most at the file and function level,
whereas raw coupling data on cross-file concerns was noisy and of little use without the semantic
interpretation of an inferential sensor, such as an LLM-based modularity review run on a slower cadence
to catch accumulated drift.

## When It Applies

The model is framed for users building an outer harness around a coding agent, not for the harness
agent builders provide. It assumes both kinds of control are present: according to the article,
feedback alone yields an agent that keeps repeating the same mistakes, and feedforward alone yields
one that encodes rules but never finds out whether they worked. How much can be built depends on the
codebase ([[DefinedTerm/harnessability]]). The author reports that sensors for internal code quality
are the easiest to build today and that sensors for functional behaviour remain largely unsolved.
Her follow-up experiments add open questions of their own: sensors can conflict with one another (rules
limiting file and function length pushed complexity into long chains of component properties), and it
is not yet settled how guides and sensors should be balanced once a set of sensors is trusted.
The vocabulary is one author's proposal, presented as a mental model rather than an established
standard.

## Related Terms

- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/harnessability]]
- [[DefinedTerm/harness-templates]]
- [[DefinedTerm/context-engineering]]
