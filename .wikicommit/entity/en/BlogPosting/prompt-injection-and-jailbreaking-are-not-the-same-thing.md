---
title: "Prompt injection and jailbreaking are not the same thing"
type: "schema:BlogPosting"
lang: en
tags: [llm, security, terminology]
sources:
  - type: url
    url: 'https://simonwillison.net/2024/Mar/5/prompt-injection-jailbreaking/'
    hash: sha256:03253e283263bfa4feaf0bb8e37840fdfebd27239d9b8c6a1b186cf5bc19d34a
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Simon Willison's attempt to hold apart two attack classes that are routinely conflated: prompt injection, which depends on concatenating untrusted input with a trusted developer prompt and targets applications, and jailbreaking, which targets the safety filters built into the models themselves."
  author: ["Simon Willison"]
  datePublished: "2024-03-05"
---

This post is a terminological intervention, written by the person who named one of the two terms
it separates. Its occasion is that people keep saying "prompt injection" when they mean
"jailbreaking"; its author concedes at the outset that the mistake may already be beyond
correcting, since the meaning of a recently coined term comes from how it is used, and argues
anyway because he thinks the distinction matters.

What the distinction turns on is concatenation. [[DefinedTerm/prompt-injection]] is defined here
as a class of attacks against applications built on top of LLMs that work by joining untrusted
user input to a trusted prompt the developer wrote; [[DefinedTerm/jailbreaking]] is the class of
attacks that try to subvert the safety filters built into the models themselves. Where there is
no concatenation of trusted and untrusted strings, the post says, it is not prompt injection —
which is presented as following from the name's own origin, chosen as an analogy to SQL injection.

## Key Points

- The two terms name different things, and the test is structural: prompt injection requires the
  concatenation of a trusted developer prompt with untrusted input.
- The stakes differ. The common risk from jailbreaking is described as a "screenshot attack" —
  someone tricks a model into saying something embarrassing and causes a PR incident. Its
  theoretical worst case is the model helping a user commit a crime they could not otherwise have
  committed; the author says he has not heard of a real-world example, since motivated bad actors
  already have other sources of information.
- Prompt injection is treated as the more serious of the two because the target is the
  application rather than the model, and how bad it gets depends entirely on what that
  application can do. With no confidential data and no tools, the risk is limited — his example
  is tricking a translation app into talking like a pirate.
- The danger case is the personal digital assistant: an LLM with access to personal data that
  acts on the user's behalf, reading and sending email. Because it concatenates trusted and
  untrusted input, an email telling it to find the latest sales figures and forward them to an
  attacker is a live risk, and the application has to act on its owner's instructions while
  ignoring instructions arriving in the content it processes.
- A practical consequence: a vendor's "prompt injection" detection system trained on jailbreaking
  attacks may block the grandmother-and-napalm style of prompt while allowing an
  application-specific data-exfiltration instruction, because that second attack is specific to
  the application and not something a jailbreak-trained system has seen.
- The author accepts there is substantial overlap. Some model safety features are baked into the
  models, but many safety features in chat applications are implemented through a concatenated
  system prompt and are therefore vulnerable to prompt injection; sometimes a model can be
  jailbroken by prompt injection, and sometimes a prompt-injection defence — especially one that
  uses AI to detect attacks — can be broken by jailbreaking techniques.
- Conflating the two invites a further misreading he objects to: that prompt-injection protection
  is about model censorship. His position is that prompt injection is a security issue, and that
  however one feels about safety filters, anyone who wants a trustworthy digital assistant should
  care about solving it.

## Context

The post closes on a lesson about terminology rather than about security: that coining a term is
like releasing open source software, in that putting it into the world is not enough and it has
to be maintained. The author judges that he has not done that well enough for prompt injection —
he has written about it a lot, but says that is not the same as getting the information in front
of the people who need it, and draws on a previous role as an engineering director for the point
that an important thing has to be said over and over to different groups rather than written down
once. He concludes it may be too late for this particular term, and that having that
conversation over and over is not what he wants to spend his time on — he has things he wants to
build. The post carries a `semantic-diffusion` tag on his site (see
[[DefinedTerm/semantic-diffusion]]).
