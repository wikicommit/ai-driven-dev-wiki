---
title: "the 80% problem"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, context-engineering, code-quality, terminology]
sources:
  - type: url
    url: 'https://sourcegraph.com/blog/agentic-coding'
    hash: sha256:0555e00c666984a838cc1b7db05eafdeedd950e02544b3d77491c6bc5a918d1c
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A term used in a 2026 Sourcegraph guide for the pattern in which a coding agent reliably completes the visible 80% of a task and silently misses the 20% that lies outside its context window — cross-cutting changes, sibling repositories, and layers it never opened. Framed as a context-infrastructure problem rather than a model limitation."
  termCode: ""
  inDefinedTermSet: ""
---

The 80% problem, as [[BlogPosting/agentic-coding-in-2026-a-practical-guide-for-big-code]] names it, is the pattern where "AI coding agents reliably do the visible 80% of a task and miss the invisible 20% that lives outside their context window." Its characteristic shape is that nothing looks wrong at the time: the agent finishes quickly, the diff looks clean, the tests pass, and the change merges — and then days later an unrelated team's CI fails because a downstream service still expects the old shape, and the agent never knew that service existed. This is one vendor's framing of the failure, offered in a guide that goes on to argue for its own product as the remedy.

## Usage

The post's central claim about the term is a claim about *where* the fault lies: "The 80% problem isn't a model limitation. It's a context infrastructure problem." Its argument is that an agent plans on what it can see — if it searches the local working directory and finds three relevant files, it plans on three files, and if the real change affects seventeen files across nine repositories it "doesn't know and won't ask," producing confident, locally correct code that misses two-thirds of the work.

What the missing 20% consists of is, on that account, predictable rather than random. The post lists the same categories recurring every time: auth middleware wrapping the changed function, API DTOs serialized at a different layer, audit logs recording state transitions, integration tests in a sibling repository, frontend guards mirroring backend permissions, and migration scripts needing regeneration. It groups the conditions that produce them into three: cross-cutting changes touching more than one service, repository, or layer; hidden technical debt in the form of subtle overrides, custom decorators, and sibling microservices the agent never opens; and monorepo blind spots, where a search limited to the working directory misses the rest of the tree.

The retrieval distinction the post draws underneath this is between **approximate retrieval** — embeddings, vector similarity, "files that look related" — and **deterministic search** — exact symbol references, every callsite, every interface implementer. Its position is that approximate retrieval is adequate on a small repository but on a large estate "returns plausible-looking results that miss cross-cutting impact, and the agent ships plausible-looking code with latent bugs."

Two practical consequences follow in the same post. Parallelism does not help: "Sub-agents amplify whatever context layer the parent has. Bad context yields parallel wrong answers faster." And the workaround it offers costs nothing to try — when an agent says it is done, search the codebase for any other usage of the symbols it touched, and if something turns up that the agent never opened, the task is not done.

## Related Terms

The 80% problem is a failure mode of [[DefinedTerm/agentic-coding]] specifically at scale, and the argument that it is a retrieval problem places it inside [[DefinedTerm/context-engineering]] — the same guide's companion post treats retrieval as one of four pillars of that discipline, and [[Dataset/codescalebench]] is the benchmark its publisher built to measure the effect. It is distinct from [[DefinedTerm/context-rot]], which concerns degradation of what is *in* the window rather than what never entered it, and it is one of the conditions [[DefinedTerm/verification-debt]] and human review are left to catch.
