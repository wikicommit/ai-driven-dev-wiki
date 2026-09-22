---
title: "Claude Tag"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-agents, coding-tools, agent-safety, human-ai-collaboration]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Jul/21/cat-and-thariq/'
    hash: sha256:a27deba3b2ae555c7354fa9733173cb7efc80237fc406cc7f265170dc8a99b5b
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "Anthropic's Claude for team collaboration tools, launched in Slack: multiplayer by default, able to act proactively for the lifetime of a channel rather than only when addressed, and carrying a shared per-channel memory. Its makers describe it as the evolution of Claude Code and report it landing 65% of their own product engineering pull requests."
  applicationCategory: "Collaborative coding agent"
  author: "[[Organization/anthropic]]"
---

Claude Tag is [[Organization/anthropic]]'s Claude for a team's collaboration tools, launched first
within Slack. Its makers describe it, in [[BlogPosting/a-fireside-chat-with-cat-and-thariq-from-the-claude-code-team]],
as internally the evolution of [[SoftwareApplication/claude-code]] and as a large shift in how they
work — reporting that their internal version lands 65% of their product engineering pull requests,
which they note is more than half.

Three differences from a conventional coding agent are given as the substance of the product. It is
**multiplayer by default**: once added to a channel, the person who invoked it and their teammates
can all chime in and collaborate on the same pull request. It is **proactive rather than reactive**:
it can be told to monitor every bug report in a channel, open a pull request to fix each one and tag
the engineer who last touched that part of the codebase, and will do so for the lifetime of the
channel without being addressed again. And it has **team memory**: preferences stated in the channel
in natural language are remembered for future posts, for everyone on the team rather than just the
person who said them.

The division of labour its makers describe is that Claude Code remains the best place for the most
complex tasks, where a person iterates interactively with the agent, while Claude Tag is for having
work done proactively on one's behalf — so that a coding agent no longer has to be started by hand
for every incoming bug report.

## Capabilities
- Multiplayer sessions in a channel: several people steering one session and collaborating on the
  resulting pull request. Its makers report a large share of their sessions being multiplayer, and
  say they are still working out the social dynamics of several people steering the same session.
- Standing, proactive instructions scoped to a channel — monitoring reports, opening pull requests
  and tagging the relevant engineer — persisting for the channel's lifetime.
- Team memory, currently implemented as a markdown file per channel, shared by every instance in that
  channel, with individual sessions able to contribute back to the main memory.
- Search across a company's public Slack channels, described as valuable as a search engine for the
  company: who has been saying what, and product context for questions about metrics when connected
  to an event store.
- Work for non-programmers: cloning a codebase to explain a feature, and producing a recording of the
  feature being used, are given as things a marketing team has had it do.
- Sharing a recording of an implementation into the channel, so that design and engineering can
  review and take a change forward in turn.
- Provisioning Claude its own credentials, so it acts as its own identity rather than on a person's
  behalf, which its makers say also makes its actions easier to audit and inspect.

## Adoption & Ecosystem
The adoption reported is the makers' own, and heavily so: 65% of their product engineering pull
requests, with sessions frequently involving several people. They describe a workflow in which a
feature is proposed in a channel, Claude Tag makes a first pass, a recording is shared with design,
and engineering takes it to production — and note that people picked up the norms by watching
others use it. One of them adds that using it in public levels up how everyone uses Claude and
reduces slop.

Its dependence on [[DefinedTerm/permission-modes]] is stated directly: Claude Tag uses the mode that
delegates approval decisions to a model, and its makers give that as what makes the product work at
all. Their reasoning is that a bot reading a channel anyone can post into is exposed to
[[DefinedTerm/prompt-injection]] by construction — they name a user feedback channel as the example
— and they advise against building one's own AI Slack bot for that reason. They also state that
Claude Tag works best when most of a company's channels are public, since it can only search what it
has access to; that is a claim about answer quality, made by the vendor, alongside the exposure just
described.
