---
title: "A Fireside Chat with Cat and Thariq from the Claude Code team"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agents, prompt-engineering, code-review, evaluation, agent-safety]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Jul/21/cat-and-thariq/'
    hash: sha256:a27deba3b2ae555c7354fa9733173cb7efc80237fc406cc7f265170dc8a99b5b
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An edited transcript of a conference fireside chat with two members of Anthropic's Claude Code team, covering their move from human to automated code review, the evals that make it tolerable, a large reduction in the product's system prompt, tool design, and the permission mode they treat as the security foundation for a Slack-resident agent."
  author: ["Simon Willison"]
  datePublished: "2026-07-21"
---

The post is an edited transcript, with added links and the author's own highlights, of a fireside
chat he hosted with two members of [[Organization/anthropic]]'s [[SoftwareApplication/claude-code]]
team. It opens with a set of top-level notes for readers who do not want the whole transcript, and
those notes are a fair guide to where its weight lies: how the team's own work has changed, what
they have stopped doing to their system prompt, and how far they have moved code review off humans.

Two threads run through it. The first is organisational. The team report that
[[SoftwareApplication/claude-tag]], their Slack-resident agent, now lands 65% of their product
engineering pull requests; that a feature must clear an internal bar for active users and retention
inside the company before it is shipped externally; and that over a process they describe as more
than six months long they have moved from human review of everything to fully automated review of
the product's outer layers, retaining code owners for its core. The mechanism they credit is
iterative: when an incident happens they look at the pull requests that caused it, ask how to update
code review to catch that, and add those pull requests to an eval set so the metric cannot regress.

The second is about prompting, and is the densest part of the post. They report reducing the Claude
Code system prompt by 80% for their most capable models, and describe two specific reversals:
removing examples was extremely helpful, because the model was more creative than the examples given
to it, and long lists of "do not do X" instructions can reduce output quality, especially where they
conflict with a user's later instructions. The generalisation they offer is to look for the edge
cases in any instruction — to find the statement that is 90% true — and to soften it, on the grounds
that you are giving the prompt to the model 100% of the time. The author notes that this amounts to
relying on the model's judgment, which is only available at frontier-model level; the team confirm
they now run a different system prompt per model.

## Key Points

- The team report that their internal version of Claude Tag lands 65% of their product engineering
  pull requests, which they characterise as an evolution of Claude Code and a
  large shift in how they work internally.
- The reported division of labour is that Claude Code remains the best place for the most complex
  tasks where a human iterates interactively, while Claude Tag is for having an agent work
  proactively without being kicked off each time.
- A feature must clear an internal bar for number of active users and for retention, measured inside
  the company, before it is shared with the world; they state that having the bar be very clear means
  every engineer knows what they are aiming at.
- Their stated reasoning for that bar includes polish: if a feature is not polished people churn, and
  in that case they conclude the feature should not ship.
- For the most critical changes to the core of their products there is always a code owner who
  manually reviews every change, and the system prompt is given as an example of an area with one.
- For changes at the outer layers they report having Claude's code review fully review them, with no
  human in the loop, reached over a process they describe as six-plus months of building trust in
  steps.
- The trust-building method they describe is file-scoped: identifying code changes where automated
  review was catching 100% of the issues and then removing the human reviewer for those files.
- Their incident loop feeds review quality directly: they examine the pull requests that caused an
  incident, ask how code review should be updated to catch it, and add those pull requests to an eval
  set so future changes cannot regress the metric.
- They state the purpose of building up an eval base over time is so that a new model can be a
  drop-in replacement: the whole eval set is run and the new model must come out strictly better
  before it is adopted.
- They report not having complete confidence that a given system prompt tweak improves the product,
  and describe optimising primarily for capability while building a separate set of behavioural evals
  for things users dislike.
- The Claude Code system prompt was reduced in size by 80% for their frontier models, attributed to
  those models rather than to any single release, with older models keeping the full prompt.
- Removing examples from the system prompt is reported as extremely helpful, on the stated grounds
  that the model was more creative than the examples provided — offered as a reversal of what was
  previously best practice.
- Lists of "do not do X" instructions are described as a very strong impulse for the model and as
  confusing when they conflict with a user's later instructions, so the team moved toward fewer hard
  constraints, more context, and fewer instructions overall.
- The prompting heuristic they generalise from that is to look for edge cases where an instruction is
  only 90% true, imagine how a well-intentioned human could misread it, and soften the wording so it
  is accurate 100% of the time.
- Their worked example is verification: an instruction to always verify front-end changes was
  replaced with a softer statement about running the app locally for larger changes to the user
  experience — and they observe that even that is imperfect, since what counts as a large change is
  undefined.
- They report running a different system prompt per model, which the author connects to the fact
  that softening an instruction relies on the model having the judgment to apply it.
- On tool design the stated direction is fewer tools, with each new tool required to have a function
  distinct from every other so the model can tell easily when to call which.
- They report having removed their own grep and glob search tools in favour of native bash, while
  keeping a dedicated file-editing tool for a presentational reason: it lets them know
  deterministically that a file change is happening, so they can render an approval UI for it.
- One of them states that for users on auto mode the file-edit tool probably no longer matters and
  could likely be removed.
- The team's stated security position rests on auto mode, the permission mode that delegates
  approval decisions to a model: they report thousands of evals,
  multiple commissioned red teams building adversarial environments, and having mitigated every issue
  found — while explicitly declining the stronger claim that it catches 100% of attacks.
- Their stated comparison is that for the main risk categories they worry about, notably
  [[DefinedTerm/prompt-injection]] and data exfiltration, the risk is far lower than that of the
  average human reviewer.
- They advise against building one's own AI Slack bot, on the grounds that a feedback channel users
  can post into becomes an input the bot reads — given as the reason their own permission work is
  what makes Claude Tag viable.
- Two further isolation mechanisms are described: provisioning Claude its own credentials in Claude
  Tag so it acts as its own identity and can be audited, and credential injection, where a proxy
  inserts credentials into the agent's requests so they are usable by the agent without being
  accessible to it.
- On the human side, one of them reports a real sense of loss among developers whose previous work is
  now a prompt, and offers being more ambitious as the way to offset it rather than disputing the
  feeling.
- The other describes the product role converging on a mix of engineer, designer and product manager
  whose job is plugging whatever gap stands between an idea and a shipped change.
- Asked what the models still cannot do, they name design and interaction taste — one noting that
  frontier AI products need interaction experiences that have yet to be designed — and interaction
  with the physical world.
- Two cultural practices are offered for other companies to copy: keeping most Slack channels public,
  because the agent can only search what it has access to, and a stated principle of not negotiating
  against oneself — making trade-offs prove themselves rather than talking oneself out of ambitious
  work.
- Internal dogfooding at the company is reported to be called "ant fooding".
- They report that memory in Claude Tag is currently a markdown file per channel, shared by every
  instance in that channel, with sessions able to contribute back to the main memory.
- On eval tooling, they report having considered building it but judging the limiting factor to be the
  skill of writing a good eval rather than the tools available.

## Context

The post is a transcript the author edited, linked and highlighted himself, so its framing is his
while its claims are the speakers'. Almost everything substantive in it is a vendor's account of its
own product and its own internal practice, and the author marks the points where that matters: he
calls the security claim "a big claim" to the speaker's face, records the reply that the evals will
be published so others can assess them, and says he is looking forward to seeing them. Several
figures — the 65% of pull requests, the 80% prompt reduction, the thousands of evals — are reported
numbers with no external verification offered. The author also uses the post to register a standing
request that the team publish their prompts, on the argument that the prompts are the documentation.
Where the post reaches outside the conversation it does so to corroborate rather than to measure:
the author appends a rival vendor's own published prompting guidance as convergent advice, which is
that vendor's claim rather than the team's and is not established here. The automated-review theme
is treated as its own subject under [[DefinedTerm/agentic-code-review]] and the review capacity it
trades against under [[DefinedTerm/review-bottleneck]]; auto mode, which the security discussion
turns on, is covered under [[DefinedTerm/permission-modes]].
