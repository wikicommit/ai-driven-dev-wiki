---
title: "Your job is to deliver code you have proven to work"
type: "schema:BlogPosting"
lang: en
tags: [code-review, verification, human-oversight, coding-agents, tdd]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Dec/18/code-proven-to-work/'
    hash: sha256:da102830a9ee0a59c820635f7725af37d08e9758f677e5bc4d7b6c87b5280f39
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A December 2025 post arguing that a software engineer's job is to deliver code they have proven to work, and that submitting large untested LLM-generated pull requests shifts the real work onto reviewers. It sets out manual testing and automated testing as two non-optional steps, argues that coding agents must be made to perform both, and places accountability with the human."
  author: "Simon Willison"
  publisher: "Simon Willison's Weblog"
  datePublished: "2025-12-18"
---

*Your job is to deliver code you have proven to work* opens from an anecdote Willison says he
keeps encountering: a junior engineer, equipped with an LLM tool, deposits a giant untested pull
request on coworkers or open source maintainers and expects code review to absorb the rest. He
calls this rude, a waste of other people's time, and a dereliction of duty as a software
developer. The post's argument is that producing code and establishing that it works are separate
obligations, and that only the second one has become scarce.

From there it states the rule the title names. Engineers do not merely produce code — the post
suggests that is increasingly what LLMs are for — they deliver code that works, together with
proof that it works. Skipping that proof does not remove the work; it transfers it to whoever is
expected to review the change.

The post then sets out what proof consists of, treats coding agents as bound by the same
requirement rather than exempt from it, and closes on accountability: the human in the loop is
what an LLM cannot supply.

## Key Points

- The post's central claim is that a software engineer's job is to deliver code they have proven to work, and that shipping an untested change shifts the actual work onto the reviewer.
- Willison names two steps to proving a change works and states that neither is optional: manual testing, then automated testing.
- On manual testing, his rule is that if you have not seen the code do the right thing yourself, the code does not work — and that if it turns out to work anyway, that is chance. He describes manual testing as a genuine skill: getting the system into an initial state, exercising the change, then checking and demonstrating the effect.
- He recommends reducing a manual test to a sequence of terminal commands that can be pasted, with their output, into a code review comment; where a change resists that, he says to record a screen capture and attach it to the pull request. This is his own working practice rather than a surveyed convention.
- Finding edge cases after the happy path is presented as the next level of the manual-testing skill, and as part of what defines a senior engineer. This is Willison's own characterisation.
- On automated testing, his position is that LLM tooling has removed any excuse for skipping it, and that a contribution should bundle the change with a test that fails if the implementation is reverted.
- He warns against skipping the manual test on the grounds that an automated test covers it, reporting that almost every time he has done so himself he quickly regretted it — backing that is explicitly his own experience.
- The post identifies the explosive growth of coding agents as the most important LLM trend of 2025, describing them as tools that actively execute the code they are working on to check that it works and iterate on problems, and naming [[SoftwareApplication/claude-code]] and Codex CLI as examples.
- Mastering such agents, on his account, means getting them to prove their changes work by the same two steps — and because they are machines, automated and manual tests amount to much the same activity for them.
- He reports that coding agents need little encouragement to write tests, will extend an existing suite unprompted, and reuse patterns from the tests already there — from which he draws the practical recommendation to keep test code well organised and populated with the patterns you want reproduced.
- The closing claim is that almost anyone can prompt an LLM into a thousand-line patch, so that is no longer valuable; what is valuable is contributing code proven to work, and the human supplies the accountability a computer cannot.

## Context

The post sits in Willison's *My open source process* series and is written from his own vantage as
a maintainer receiving contributions, which is the perspective its opening complaint comes from.
Its backing is largely personal practice — the pasted-terminal-output convention, the regret at
skipping manual tests, the observation about agents reusing existing test patterns are all
reported from his own work rather than from measurement or a wider survey — and the post presents
them as such.

Its argument runs closely parallel to
[[BlogPosting/ai-writes-code-faster-your-job-is-still-to-prove-it-works]], which makes the same
core move of treating the burden of proof rather than review itself as what AI changed. Willison
also refers back to an earlier post of his own for the principle that a computer can never be held
accountable, which is the ground for his closing point that accountability is the human's job.

The post's treatment of [[DefinedTerm/ai-coding-agent]] tooling is notable for extending the
requirement rather than relaxing it: the agent's ability to execute code is what makes it an agent
in his framing, and that same ability is what obliges it to demonstrate its work.
