---
title: "Five levels of AI-assisted software development"
type: "schema:DefinedTerm"
lang: en
tags: [autonomy-levels, ai-adoption, spec-driven-development]
aliases: ["Five-level model of AI-assisted development", "Die fünf Level der KI-gestützten Softwareentwicklung"]
sources:
  - type: url
    url: 'https://www.codecentric.de/wissens-hub/blog/die-fuenf-level-der-ki-gestuetzten-softwareentwicklung'
    hash: sha256:dd91892144c608f0d58b8c74f1aeb1279be77b47d81570f9b36bd4c5b2259d5a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A five-level model of AI support in programming, modelled on the levels of autonomous driving, that Goetz Markgraf of codecentric presented at a conference talk and described in a February 2026 blog post: AI code assistance, AI code generation, agentic AI development, spec-driven development, and autonomous product evolution."
---

The five levels of AI-assisted software development are a model proposed by Goetz Markgraf, a
consultant at codecentric, for describing how far AI takes part in programming, drawn as a parallel to
the levels of autonomous driving. He first presented it in a talk at a conference on AI-assisted coding
and described it in a February 2026 blog post, arguing that without such a classification people talk
past one another about "AI in programming". The five levels are **AI code assistance** (level 1),
**AI code generation** (level 2), **agentic AI development** (level 3), **spec-driven development**
(level 4) and **autonomous product evolution** (level 5).

## Usage

In Markgraf's account:

- **Level 1, AI code assistance** — web-based AI chats such as ChatGPT, Claude or Gemini. The
  developer asks a question, copies the answer into their own code by hand, and builds the context
  themselves by copy-and-paste or uploading documents; the AI acts as a kind of "StackOverflow on
  demand". His driving parallel is a simple cruise control.
- **Level 2, AI code generation** — IDE plugins such as [[SoftwareApplication/github-copilot]],
  JetBrains AI Assistance or [[SoftwareApplication/continue-dev]] propose completions, offer chat, and
  can generate whole code blocks from an instruction; the developer critically reviews each proposal.
  The parallel is adaptive cruise control.
- **Level 3, agentic AI development** — an agent such as [[SoftwareApplication/cursor]], Windsurf,
  [[SoftwareApplication/claude-code]] or [[SoftwareApplication/opencode]] takes on a task from a
  natural-language instruction and works through several steps on its own: finding and reading files,
  writing code, possibly running tests and fixing errors. The developer supervises, intervenes and
  checks the result. The parallel is lane-keeping with automatic lane changes on the motorway.
- **Level 4, spec-driven development** — human and AI first work together to understand the task and
  write a detailed plan (a spec), after which the AI generates fairly complex code or changes existing
  code largely on its own. It uses the same agents as level 3 and differs only in how they are used;
  the final result must still be reviewed intensively and tested by hand. The parallel is autonomous
  driving in defined areas, such as a parking-garage service or motorway traffic jams. See
  [[DefinedTerm/spec-driven-development]].
- **Level 5, autonomous product evolution** — a whole product is written and developed further
  exclusively by AI, including operation and monitoring, and nobody looks at the code. He calls it
  still largely hypothetical: tools such as v0, Bolt, Lovable, Emergent or Replit generate whole
  applications from descriptions, but in his view do not yet produce production-ready solutions or run
  them on their own. The parallel is full driving automation with no steering wheel.

Markgraf says the model carries no ranking — level 3 is not automatically better than level 2 — but
that efficiency rises with each level. He reports that speakers who followed him at the conference
spontaneously adopted the model to place their own topics within it.

### AI readiness

The post pairs the model with the preconditions it calls **AI readiness**: the readiness and ability
of a team, a codebase and an organization to use AI effectively and without risk. Its examples are
clean code and a clear architecture, made known to agents at levels 3 and 4 through instruction files;
automated tests, which it calls the most important safety net, including not letting the AI switch
off or delete tests; documentation such as README files, a `docs/` folder in Markdown or arc42;
team skills, including jointly maintained instruction files and a Definition of Ready or Done;
isolating agents from the host from level 4 onwards, for example with Docker containers, to limit the
damage from [[DefinedTerm/prompt-injection]]; and a paid AI subscription whose terms rule out using the
processed code for training.

## When It Applies

The model is one practitioner's orientation aid rather than an empirically derived scale: its stated
purposes are helping a team establish where it stands and where it wants to go, setting realistic
expectations, and giving people a shared vocabulary. Its support is the author's own experience and his
report of how it was taken up at one conference. In his account level 4 is separated from level 3 by a way of
working rather than by new technology.

## Related Terms

- [[DefinedTerm/ai-maturity-levels]]
- [[DefinedTerm/agentic-autonomy-levels]]
- [[DefinedTerm/se-autonomy-levels]]
- [[DefinedTerm/sandboxing]]
