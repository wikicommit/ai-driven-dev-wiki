---
title: "진짜 '딸깍'으로 다 되나요? — 보수적 개발자가 AI 에이전트로 프로덕트를 릴리즈하며 깨달은 것들"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, coding-tools, testing, developer-productivity]
sources:
  - type: url
    url: 'https://jonghoonpark.com/2026/03/29/agentic-engineering'
    hash: sha256:92fea29c2779ce511435e3c79aeb42f9b33855c8f3a1f24849a1c6993534b024
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A Korean write-up of a talk in which a self-described conservative developer recounts rebuilding a community site with a coding agent, arguing that the real work is engineering rather than vibes, that economising on tokens costs more than it saves, and that test code is what makes agent-written code trustworthy."
  author: "박종훈"
  datePublished: "2026-03-29"
---

A write-up of a talk, published on the author's own Korean technical blog, recounting the
rebuild and release of the K-DEVCON community site with a coding agent. Its framing device is the
author's self-description as a conservative developer — someone who watches new technology from a
distance and does not pay for subscriptions readily — who ended up on a $100-a-month plan. The post
notes at the top that its prose was organised from the talk by AI, so some of it may differ from what
was said and much may be omitted.

## Argument

Its opening move is the one the title argues against: that a product does not come out of a single
click. The post places its own account under [[DefinedTerm/agentic-engineering]] rather than
[[DefinedTerm/vibe-coding]], glossing the two halves of the name — agentic, meaning the developer
supervises agents that write the code instead of writing it themselves, and engineering, meaning the
process demands expertise that must be learned and developed — and then confirming the choice from
experience: the author reports that working with AI felt closer to a fight than to vibes, and recalls
asking the agent more than once why it was doing the thing it had been told not to. Technology delivers value, on this
account, only once the agent's output can be controlled and verified.

The post's most developed argument is against economising on tokens. The author describes starting on
a free tier, getting a skeleton out of it, and then stalling: additions produced the wrong shape,
runs did not finish, quotas blocked. On a paid tier the pattern became what the post calls a
token-based life — develop while tokens last, then do the laundry and wait for the reset. The
conclusion drawn is that the loss of a developer's cognitive flow costs more than the tokens saved.

That leads to the shift the post treats as decisive, which it attributes to a question put to the
author by an acquaintance: why are you fixing that yourself, instead of throwing it at the agent? The
author had been giving the model three to five attempts at an error and then opening the code
directly, to avoid burning tokens in a loop. The reframing is to treat the agent not as a code
generator but as an entity that reasons about and solves problems itself — handing over the error
logs and failing tests whole, and taking the developer's role to be a director who supplies the right
context and makes the final call.

On trusting what the agent writes, the post's answer is test code as compulsory verification. Passing
tests are what demonstrate that new code has not disturbed what was there, and the post extends what
tests should defend beyond logic to architecture (structural rules enforced by architecture tests),
coverage (a minimum threshold), and code quality (static analysis in the test pipeline). It adds a
second reason for them: test results are one of the best ways to tell an AI the direction a team
wants, clearer than documentation and acting as a guardrail without narrowing the agent's options
too far.

## Reported practice

The post calls its SEO work the most interesting part of the site revamp, on the grounds that the
author is a backend developer who nonetheless improved the site's SEO score dramatically.

- **Two-track routing** to get crawler-visible metadata without server-side rendering: the backend
  generates static Open Graph HTML when content is created, edited or deleted and stores it on a
  shared volume, and Nginx branches on User-Agent, sending ordinary users to the React SPA and
  crawler bots to the pre-generated HTML. The post links to its own earlier article for the detail.
- **A third-party SEO skill** run against the site to produce a list of improvement points, which is
  then handed back to the agent to apply against the source; the post reports repeating this loop
  about once a week. Its stated observation is that [[DefinedTerm/agent-skills]] help most in a
  domain that is not one's own.
- **Lighthouse output as JSON** fed to the agent with a request to check the source and fix what the
  report flags.
- **Templating repeated prompts as Skills** — the example given is a standing request to analyse
  uncommitted changes and write tests for them. The stated motive is that retyping the same prompt
  had become tedious; what the post says the result is, is not a mere prompt but an engineer's
  know-how transplanted into coding conventions.

## Reception and limits

The post closes on what it calls the last 20%. AI is said to handle 80% of the work while filling in
the remaining detail, and answering for the result, stays with people. Against accounts of enormous
token spend and tens of thousands of lines added, the author reports that such cases tend to involve
one person owning a whole area or working outside a live service, and advises against anxiety about
them.

Its final position is about direction rather than answers: AI can supply many answers, but choosing
the one that fits a service's context is something only a developer who has been through it can do;
knowledge alone leaves you accepting what you are given, while detail filled in by direct experience
becomes a capability. The post asks readers not to accept an AI's answer unexamined but to ask why it
judged as it did — and states plainly that AI takes no responsibility, and only people can carry it
and decide the direction.

This is one developer's account of one project, presented as a talk write-up; it reports no
measurement and no comparison, and the productivity claims in it are the author's own.
