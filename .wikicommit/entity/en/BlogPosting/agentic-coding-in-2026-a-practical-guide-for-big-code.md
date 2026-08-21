---
title: "Agentic Coding in 2026: A Practical Guide for Big Code"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, ai-assisted-programming, context-engineering, code-quality]
sources:
  - type: url
    url: 'https://sourcegraph.com/blog/agentic-coding'
    hash: sha256:0555e00c666984a838cc1b7db05eafdeedd950e02544b3d77491c6bc5a918d1c
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A Sourcegraph guide of 21 May 2026 by Matt Tanner, aimed at senior engineers and platform leaders running coding agents on large codebases. It defines agentic coding against vibe coding, sets out the agent loop, and names [[DefinedTerm/eighty-percent-problem]] as the characteristic failure at scale."
  author:
    - "Matt Tanner"
  datePublished: "2026-05-21"
  publisher: "[[Organization/sourcegraph]]"
---

"Agentic Coding in 2026: A Practical Guide for Big Code" is a guide published on the [[Organization/sourcegraph]] blog on 21 May 2026 by Matt Tanner. Its stated audience is senior engineers and platform leaders making agentic coding work at real scale, and its organising observation is that "techniques that work on a side project fall over the moment you aim them at a 2,000-repository monorepo with twelve years of accumulated decisions."

The guide's substantive contribution is [[DefinedTerm/eighty-percent-problem]] — its name for the pattern in which an agent completes the visible portion of a task and silently misses what lies outside its context window — together with the argument that this is a context-infrastructure problem rather than a model limitation. That argument leads to the publisher's own products, and the post is a vendor guide: its closing sections are a catalogue of Sourcegraph surfaces and a demo request.

It is nonetheless careful about the boundary of its own claim. Its "honesty caveat" states that on a small single-repo project this codebase-wide context is not needed, and that the value it argues for "shows up the moment your repo count crosses 1 and accelerates towards 100."

## Key Points

- **A definition drawn around autonomous tool use.** The guide defines agentic coding as software development where an autonomous agent plans, writes, tests, and iterates on code with limited human intervention, using a shell, a test runner, code search, and version control. Its illustration of the boundary is what each category of tool does when told "fix the failing build": autocomplete does nothing because it needs you to start typing; chat reads a pasted error and suggests a fix you apply manually; an agent opens a terminal, runs the failing test, reads the stack trace, greps for the broken function, edits the file, re-runs the test, and reports back when green. The behavioural leap it identifies is that "the agent decides what to do next based on what it just observed."
- **Vibe coding as posture, agentic coding as architecture.** The post attributes the coining of "vibe coding" to Andrej Karpathy in a February 2025 tweet describing "a new kind of coding" where you "fully give in to the vibes, embrace exponentials, and forget that the code even exists," and notes Karpathy was explicit that he was describing throwaway weekend projects. Its own distinction is that "vibe coding is a posture: trust the model, don't read the diff, keep prompting until it works," while "agentic coding is an architecture: the model is wired into tools, runs in a loop, and produces code that a human reviews against a definition of done." It reduces this to a single question — "The difference is who owns correctness" — and to a rule: "Vibe coding works when the cost of being wrong is zero. Agentic coding has to work when the cost of being wrong is a customer outage."
- **A seven-step loop.** Prompt, context gathering, plan, execute, test, refine, output. Its claim about what differentiates agents is that "what makes one agent better than another is rarely the model," since many tools draw on the same frontier model families — the differentiator being the system around the model: retrieval, tool use, planning, sandboxing, and review, and above all the quality of step two.
- **The 80% problem.** Agents reliably do the visible 80% of a task and miss the invisible 20% outside their context window, in predictable categories: auth middleware, API DTOs at another layer, audit logging, integration tests in sibling repositories, frontend guards mirroring backend permissions, and migration scripts. The post frames the fix as retrieval rather than reasoning — "The agent didn't get smarter. It got more eyes" — and distinguishes approximate retrieval (embeddings, vector similarity) from deterministic search (exact symbol references, every callsite, every implementer).
- **A six-step team workflow.** Scope the task, with a senior engineer writing the prompt and deciding whether the change is local or cross-cutting; equip the agent with context; run the loop, watching for a clean exit or a stuck state; review the diff like a human pull request, including running it locally; gate on CI, so no agent commit lands without the checks human commits face; and audit afterward, tracking activity by agent, prompt, and code change — its framing being to "treat the agent like a contractor with commit rights." It adds a cheap check: when an agent says it is done, search for other usage of the symbols it touched, and if something turns up the agent never opened, the task is not done.
- **A three-layer stack.** Coding agents that run the loop; IDE integrations and chat assistants, useful for short-horizon tasks but not autonomous in the loop sense; and context and infrastructure layers — indexing, code search, code intelligence, repository-wide knowledge. Its mental model for the three is that "agents are the engine, MCP is the wiring, codebase context is the fuel. A great engine on bad fuel still stalls."

- **A cost model for running agents.** The guide decomposes cost into three lines — model inference, retrieval and indexing infrastructure, and human review time — and names inference as the most volatile, "because agents make many calls per task during the refine loop." Its stated driver of the variance teams report is context quality: "with the right context, agents retry less and finish faster," which makes context work a cost lever rather than only a quality one.

## Context

The post cites its own publisher's data for the claim that agent output compounds rather than settles: it reports that 84% of large enterprise accounts saw a steady increase in lines of code after AI rollout, and that developers responded by searching more, not less. That figure is Sourcegraph's own, drawn from its own accounts.

Two attributions it makes to others are worth keeping separate from its own argument. It reads [[Person/simon-willison]]'s writing on agentic engineering as framing the practice as "professional engineers using coding agents to amplify existing expertise, not replace human judgment with vibes" — compare the primary account on [[DefinedTerm/vibe-engineering]]. And it cites Steve Yegge's "brute squad" framing for the changed developer role: less typing code, more steering and verifying many concurrent runs. It also quotes Stripe's Alistair Gray, from the Sourcegraph homepage, describing Stripe's internal "Minions" agent workforce as connected to MCP for gathering internal docs, ticket details, build statuses, and code intelligence.
