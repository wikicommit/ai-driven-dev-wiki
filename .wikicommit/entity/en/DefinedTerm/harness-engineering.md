---
title: "Harness Engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, evaluation, agent-tooling]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agent-harness-engineering/'
    hash: sha256:7fc8b9bc3a19589c08e3c6ab46607839f3c435799f128886bea9bca6cd634760
  - type: url
    url: 'https://developers.googleblog.com/the-anatomy-of-harness-engineering-how-to-evaluate-iterate-and-guard-ai-coding-agents/'
    hash: sha256:b7703e83eb963ad1264b1927a931ffc37279d57efe136cc6d02e664b3df6aa63
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/how-coding-agents-work/'
    hash: sha256:a8be3f0926e2b75d77e83036446bf575cf49b7dff42641018af0909da9d387eb
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
    hash: sha256:26ce4c203cbb030f31253f1eb174b46b2c0203c9b44576aa4654b89b4d7be777
  - type: url
    url: 'https://www.anthropic.com/engineering/harness-design-long-running-apps'
    hash: sha256:47a08ad7125c953a6a359d169a11e61245c1d5329e47cb7057f496aaaef42b2a
  - type: url
    url: 'https://www.anthropic.com/research/building-effective-agents'
    hash: sha256:611504eb30423330be060ed8f00e432a0adcb417f992b2cfb5cbf9ccd8d511bf
  - type: url
    url: 'https://www.anthropic.com/research/trustworthy-agents'
    hash: sha256:7b2800e6840e79dc817c3f2b89dba0aad5a79482b920ffc7c6ff72b1b9f967c9
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The discipline of treating the scaffolding built around an AI model — prompts, tools, context policies, hooks, sandboxes, feedback loops — as a real engineering artifact, rather than treating model choice as the main lever on agent behavior."
---

Harness engineering is the discipline of designing and maintaining the "harness" around an AI model — the prompts, tools, context policies, hooks, sandboxes, subagents, feedback loops, and recovery paths that turn a raw model into a working agent. It is summarized, in a formulation Addy Osmani's post attributes to Viv Trivedy, as "agent = model + harness": the model is one input, and the harness is everything else that gives it state, tool execution, feedback loops, and enforceable constraints.

An Anthropic post on agent governance, [[BlogPosting/trustworthy-agents-in-practice]] (April 9, 2026),
splits the same territory four ways rather than two, and names the harness as one of the four. On that account an agent is built from
**the model** (the intelligence that makes tasks possible, shaped by training), **a harness** (the
instructions and the guardrails the model operates under — its examples are telling the agent to flag
anything over a set amount, or never to submit expenses without user confirmation), **tools** (the services and
applications the model can use), and **an environment** (where the agent runs and which files, websites
and systems it can reach, so that the same agent on a corporate laptop inside a company network has
different data access and different stakes than on a personal phone). Each is described as both a source
of capability and a potential point of oversight.

That four-way split is not a rival to "agent = model + harness" so much as a decomposition of its second
term, and the argument attached to it is about where attention goes. The post observes that most AI
policy conversation centres on the model, understandably, since that is where core capabilities come
from — but that a well-trained model can still be exploited through a poorly configured harness, an
overly permissive tool, or an exposed environment. Read alongside the formulation above, it is the case
for harness engineering stated from the security side rather than the behaviour side.

## Usage

The term is applied to coding agents such as Claude Code, Cursor, Codex, Aider, and Cline. Addy Osmani's post argues that the behaviour a user experiences from these agents is dominated by what the harness does even where the model underneath is the same, and observes that set side by side they look more like each other than their underlying models do — the models differ while the harness patterns converge. The practice covers concrete components including the filesystem and Git for durable state, bash and code execution as the general-purpose action mechanism, sandboxes for safe execution, memory files (e.g. `AGENTS.md`) for continual learning across sessions, techniques for mitigating context rot (compaction, tool-call offloading, progressive disclosure of skills), long-horizon execution patterns (the Ralph Loop, planning, planner/evaluator splits), and hooks that enforce rules deterministically rather than relying on a model to remember them.

## Evaluating a Harness

A Google engineering team writing on the same discipline argues that how a harness is evaluated is
part of engineering it. They treat end-to-end benchmarks as the de facto way to evaluate model
performance and to decide what needs deeper investigation, but argue they are a poor instrument for
iteration: on their account, running suites such as Terminal-Bench and DeepSWE moves a composite
score by a few percentage points without typically saying directly why it changed. Their proposed complement is
[[DefinedTerm/behavioral-evaluation]] — fast, deterministic, unit-style assertions on discrete
observable actions the agent takes, such as which tool it called or which file it modified — which
they describe as integration tests for harness operation and as an iteration partner that shows
whether a prompt tweak, tool schema change or model upgrade made the agent holistically worse.

They also place evaluation in time: a team bootstrapping an agent starts with developer instinct
and dogfooding, and until the agent can dogfood its own codebase they argue it does not make sense
to run evaluations at all. Their closing position is that the two kinds are complementary rather
than substitutes, with macro benchmarks verifying the final destination and micro behavioural evals
enabling safe, rapid iteration. This is one team's recommended practice published on their
employer's developer blog, not a measured comparison.

A chapter of [[CreativeWorkSeries/agentic-engineering-patterns]] supplies the plainest statement of
what the word "harness" denotes: a coding
agent *is* a harness for a language model — software that extends the model with additional
capabilities powered by prompts the user never sees and implemented as callable tools. Read that way,
the harness is not a layer wrapped around the product; it is what makes the product something other
than a text completion endpoint. That chapter's inventory of the pieces is correspondingly minimal —
the chat-templated prompt the harness assembles and replays, the tool definitions it offers, the
system prompt it hides, and the loop it runs — and its deflationary conclusion is that a simple tool
loop takes a few dozen lines while a *good* one is a great deal more work. See
[[DefinedTerm/ai-coding-agent]].

[[BlogPosting/effective-harnesses-for-long-running-agents]] is a worked example of harness engineering
at the horizon where the context window stops being sufficient, and its lesson is about where state
belongs. Anthropic reports that a frontier model on a general-purpose harness, with compaction
available, still fails to build a production-quality application from a high-level prompt — so the
harness work it describes is not in the model loop at all but in the artifacts around it: a startup
script, a progress log, a git history, and a structured feature list written once by an
[[DefinedTerm/initializer-agent]]. It also reports a prompting-level fix for premature completion — instructing the agent to verify
features end-to-end through browser automation, as a user would, rather than marking them passing on its
own say-so — which it describes as mostly working once explicitly prompted.

A later post from the same engineering team,
[[BlogPosting/harness-design-for-long-running-application-development]], makes the separation between
the agent doing the work and the agent judging it a harness lever in its own right. Its stated reason
is that agents asked to evaluate their own output tend to praise it confidently even when the quality
is visibly mediocre — most sharply on subjective tasks such as design, where no binary check equivalent
to a software test exists, but also on tasks that do have verifiable outcomes. Separation is not
presented as eliminating that leniency, since the evaluator is still an LLM inclined to be generous
toward LLM-generated output; the argument is that tuning a standalone evaluator to be skeptical is far
more tractable than making a generator critical of its own work, and that once that external feedback
exists the generator has something concrete to iterate against. The same post reports the tuning as
real work rather than a configuration step: out of the box it describes Claude as a poor QA agent,
which it watched identify legitimate issues and then talk itself into approving the work anyway, and
which tested superficially rather than probing edge cases.

That account also treats an evaluator's value as conditional rather than settled. As the underlying
model improved, tasks that had previously needed the evaluator's check came within what the generator
handled reliably on its own, and for those the evaluator became unnecessary overhead; the rule the post
draws is that an evaluator is worth its cost when the task sits beyond what the current model does
reliably solo.

## When It Applies

The practice treats an agent's mistakes as permanent signals rather than isolated incidents: a specific observed failure is encoded as a rule, a hook, or a check, and a rule is only removed once a more capable model has made it redundant — so a harness is described as shaped by its own failure history rather than something that can be downloaded ready-made. It applies where an agent is expected to work with some autonomy over multiple steps. Osmani's post also describes a way of over-applying the mindset, in a point it credits to Anthropic's own write-up: treating harness components as permanent rather than revisiting them as models improve, since a component that once compensated for a model limitation can become dead weight once that limitation is gone.

Anthropic states that position firsthand in
[[BlogPosting/harness-design-for-long-running-application-development]], and as a general principle
rather than a caution: every component in a harness encodes an assumption about what the model cannot do on
its own, and those assumptions are worth stress testing, both because they may be incorrect and because
they can quickly go stale as models improve. That post's two reported drops arrived by different routes.
[[DefinedTerm/context-reset]] was simply left out of the new harness from the start, because Opus 4.5
largely removed the [[DefinedTerm/context-anxiety]] behaviour the technique had been compensating for.
The sprint-based decomposition of the build went later and deliberately: after a first attempt at
cutting the harness back radically failed to replicate the original's performance and left it difficult
to tell which pieces had been load-bearing, the author moved to removing one component at a time and
reviewing the impact of each, and the sprint construct was the first thing removed that way. That post
quotes Anthropic's own [[BlogPosting/building-effective-agents]] for the underlying idea — "find the
simplest solution possible, and only increase complexity when needed" — and closes on the position that
the space of interesting harness combinations does not shrink as models improve but moves.

The term and its "agent = model + harness" formulation are attributed by Osmani's post to Viv Trivedy, whose own write-up it credits as the clearest derivation of what a harness is and why each piece exists; that post also draws on Dex Horthy, HumanLayer, Anthropic's own engineering team and Birgitta Böckeler, describing itself as an attempt to pull those threads together.

## Related Terms

[[DefinedTerm/ralph-loop]], [[DefinedTerm/harness-as-a-service]], [[DefinedTerm/context-rot]], [[DefinedTerm/compaction]], [[DefinedTerm/agents-md]], [[DefinedTerm/behavioral-evaluation]], [[DefinedTerm/initializer-agent]], [[DefinedTerm/ai-coding-agent]], [[DefinedTerm/context-reset]], [[DefinedTerm/context-anxiety]], [[DefinedTerm/guardrails]]
