---
title: "How StrongDM's AI team build serious software without even looking at the code"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agents, code-review, verification, evaluation]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Feb/7/software-factory/'
    hash: sha256:f037b61ef74329e98d22e3f5e86498585708d651d71581e420890095020b0ad3
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An account of StrongDM's AI team's first public description of their software factory, focused on the question the arrangement raises: how you gain confidence that code works when neither the implementation nor the tests were written or read by a human."
  author: ["Simon Willison"]
  datePublished: "2026-02-07"
---

The post relays and reacts to the first public description by [[Organization/strongdm]]'s AI team of
how they work, having seen a demo of it some months earlier. Their arrangement — which they call a
[[DefinedTerm/software-factory]] — is summarised through their own quoted rules, and the author
singles out one of them as by far the most interesting: that code **must not be reviewed by humans**.
His framing question is how that could possibly be a sensible strategy given how prone LLMs are to
mistakes a human would not make.

Most of the post is the answer to that question, and the author treats it as the consequential one
for software development generally: how can you prove software works when both the implementation
and the tests are written for you by coding agents? Having the agents write tests only helps if they
do not cheat. The answer, which the source describes as inspired by
scenario testing, is the team's own repurposing of "scenario" to mean an end-to-end user story they say is often held **outside** the codebase — the author
draws the analogy the team does, to a holdout set in model training — and to replace a boolean
notion of success with a probabilistic one they call satisfaction. The author calls the
scenarios-as-holdout idea fascinating and reads it as imitating aggressive testing by an external QA
team.

The part that impressed him most is the [[DefinedTerm/digital-twin-universe]]: agent-built
behavioural clones of the third-party services the software depends on, which let the team run
thousands of scenarios per hour without rate limits or API costs. He notes that the software being
built this way manages user permissions across connected services — security software, which he says
is the last thing you would expect to be built from unreviewed LLM code. The post closes on the
figure it initially skated over: the team's stated benchmark of at least $1,000 of tokens per
engineer per day. The author treats that as the term that decides whether any of this generalises,
observing that at roughly $20,000 per engineer per month the patterns become a business-model
question rather than an engineering one, and saying he hopes they can be put into play for much less.

## Key Points
- The team's stated rules are quoted in three forms — a question ("Why am I doing this?", implying
  the model should be doing it instead), two prohibitions (code must not be written by humans; code
  must not be reviewed by humans), and a spend benchmark of at least $1,000 of tokens per human
  engineer per day.
- Of those, the author identifies "code must not be reviewed by humans" as the most interesting and
  the hardest to accept, given how prone LLMs are to mistakes a human would not make.
- The question the post treats as the most consequential in software development right now is how to
  prove that software works when both implementation and tests are agent-written — because agent-authored
  tests only help if the agent does not cheat.
- The team dates its founding catalyst to a transition observed in late 2024, stating that with the
  second revision of Claude 3.5 long-horizon agentic coding workflows began to compound correctness
  rather than error; this is their own account of their history, quoted by the post.
- The team was founded in July 2025 on the rule of no hand-coded software, which the author calls
  radical for that date while reporting that significant numbers of experienced developers began
  adopting it around January 2026.
- The author separately notes a widely acknowledged inflection point in November 2025, when
  Claude Opus 4.5 and GPT 5.2 appeared to turn the corner on how reliably a coding agent could follow
  instructions and take on complex tasks — his own framing, distinct from the team's 2024 catalyst.
- A "scenario" in their usage is an end-to-end user story, often stored outside the codebase, which
  an LLM can understand intuitively and validate flexibly; that keeping it out of the codebase puts it
  where the coding agents cannot see it is the relaying author's gloss rather than the team's stated
  rationale.
- "Satisfaction" is their term for a probabilistic measure of validation: of all observed
  trajectories through all the scenarios, what fraction likely satisfy the user — adopted because
  much of the software they grow has an agentic component, so boolean success is the wrong shape.
- Keeping scenarios where the agents cannot read them is presented by the author as imitating
  aggressive testing by an external QA team, an expensive but highly effective quality mechanism in
  conventional software.
- The Digital Twin Universe is described by the team as behavioural clones of their third-party
  dependencies, replicating APIs, edge cases and observable behaviours, with twins built for Okta,
  Jira, Slack, Google Docs, Google Drive and Google Sheets.
- The team's stated reasons for the twins are validation at volumes and rates far exceeding
  production limits, testing failure modes that would be dangerous or impossible against live
  services, and thousands of scenarios per hour without rate limits, abuse detection or API costs.
- As the author understood the technique, a twin is built by feeding a service's full public API
  documentation into their agent harness and having it produce an imitation as a self-contained Go
  binary, with a simplified UI generated over the top.
- An update appended to the post relays the twins' creator stating a repeatable fidelity
  strategy, which is to treat the widely used public reference SDK client
  libraries for a service as the compatibility target a twin is built against, aiming always at full
  compatibility.
- The team argues that a high-fidelity clone of a significant SaaS application was always possible
  but never economically feasible, and that engineers who wanted one historically self-censored the
  proposal to build it.
- The software being built under this arrangement manages user permissions across a suite of
  connected services, which the author flags as notable because security software is the last thing
  one would expect to be built from unreviewed LLM code.
- Two releases accompanied the write-up: [[SoftwareApplication/attractor]], whose repository contains
  no code at all, and [[SoftwareApplication/cxdb]], a conventional release of roughly 16,000 lines of
  Rust, 9,500 of Go and 6,700 of TypeScript.
- Three further named techniques are introduced from the team's own techniques page — gene transfusion
  for having agents extract patterns from existing systems and reuse them elsewhere, semports for
  porting code directly between languages, and pyramid summaries for layered summaries an agent can
  scan cheaply and then zoom into; the details of those pages are theirs and are not established here.
- The author's judgment on cost is explicit: if these patterns add roughly $20,000 per engineer per
  month they are far less interesting to him, becoming a question of whether the product line can
  carry the overhead.
- He notes a second consequence of the same capability — that sustainable software businesses look
  different when any competitor can clone a new feature with a few hours of coding agent work.
- He reports that a $200/month subscription gives him room to experiment with agent patterns, while
  noting he is not running a swarm of simulated QA testers continuously.

## Context
The post is a firsthand reaction to a demo the author attended some months before publication,
combined with the team's own first public write-up, and it is candid about that dual footing: the
mechanics of the digital twins are given as "as I understood it", and the team's quoted claims about
their catalyst and their results are relayed rather than verified. The author's stance is interested
rather than convinced — he calls the arrangement a glimpse of one potential future, in which
engineers move from building the code to building and semi-monitoring the systems that build it, and
he twice returns to what he says he is most invested in: what it takes to have agents prove their
code works without a human reading every line. He also records revising the post to give the token
spend serious attention after initially glossing over it. The broader framing of a development
organisation as a factory is treated elsewhere as its own subject — see
[[DefinedTerm/factory-model]] — and the review question the post turns on is the subject of
[[DefinedTerm/review-bottleneck]] and [[DefinedTerm/agentic-code-review]].
