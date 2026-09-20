---
title: "Exercise caution when building off LLMs"
type: "schema:BlogPosting"
lang: en
tags: [llm, security, prompt-injection, governance]
sources:
  - type: url
    url: 'https://www.ncsc.gov.uk/blog-post/exercise-caution-building-off-llms'
    hash: sha256:b541d32182b2dc0647d41d9d904fb93653c6c331e794b22d8120713014c203dd
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An NCSC post arguing that organisations building services on LLM APIs should treat the technology as still in beta, that prompt injection may be inherent to it with no surefire mitigations, and that the main defence available is architecting for the worst case of whatever the application is permitted to do."
  author: "Dave Chismon"
  publisher: "NCSC"
  datePublished: "2023-08-30"
---

This post's argument is summarised in its own standfirst: Large Language Models are an exciting
technology, but our understanding of them is still "in beta". Written as organisations across all
sectors began reporting that they were investigating LLM integrations for internal and customer
use, it sets out two categories of caution — one about the market and one about the technology —
and lands on an architectural recommendation rather than a technical fix.

The market caution is that even paid-for commercial access to LLMs changes rapidly. An organisation
building services on LLM APIs has to account for models changing behind the API it is using, which
breaks existing prompts, and for the possibility that a key part of its integrations ceases to
exist because the startup offering it does not survive.

The technology caution is that the global tech community does not yet fully understand LLMs'
capabilities, weaknesses and, crucially, vulnerabilities. The post frames this as a blind spot in
how the field thinks: machine learning was understood as being good at things like classifying
whether an image had a cat in it, artificial general intelligence as something we would know when
we saw it, and LLMs fit neither picture — the author notes the observation that it is more accurate
to say we "grew" LLMs than that we created them, and suggests treating them as a third kind of
entity rather than forcing them into the ML or AGI frame.

## Key Points

- Research is suggesting that an LLM inherently cannot distinguish between an instruction and data
  provided to help complete the instruction. The post states this as what research suggests rather
  than as settled fact.
- [[DefinedTerm/prompt-injection]] may simply be an inherent issue with LLM technology. Research
  into possible mitigations is ongoing and some strategies can make injection more difficult, but
  the post states there are as yet no surefire mitigations.
- The reputational version of the risk had already been observed: the prompt behind an
  organisation's LLM-powered chatbot was, with appropriate coaxing from a hostile user, subverted
  into making the chatbot state upsetting or embarrassing things, which then appeared on social
  media.
- The dangerous version is a hypothetical the post works through. A bank deploys an LLM assistant
  for account holders to ask questions or give instructions about their finances; an attacker sends
  the user a transaction request whose reference field hides a prompt injection; when the user asks
  the assistant whether they are spending more this month, it analyses transactions, encounters the
  malicious one, and is reprogrammed by it into sending the user's money to the attacker's account.
  The post notes that early developers of LLM-integrated products have already observed attempted
  prompt injection attacks.
- Testing LLM-based applications may need different techniques from those the community already has
  for classical attacks — the post's examples are social-engineering-like approaches that convince
  models to disregard their instructions, or that find gaps in the instructions. It sets this
  against SQL injection, which it describes as well known and far less commonly seen these days.
- The central recommendation is architectural: ensure the organisation is architecting the system
  and data flows so that it is happy with the worst-case scenario of whatever the LLM-powered
  application is permitted to do. The post adds that more vulnerabilities and weaknesses will be
  discovered in these technologies that have not yet been foreseen.

## Context

The post's closing analogy is to a product or code library that is in beta: an organisation would
not let such a thing be involved in making transactions on a customer's behalf, and would not fully
trust it yet, and the author argues similar caution should apply to LLMs. The caution is presented
as compatible with enthusiasm rather than opposed to it — the post is explicit that the emergence
of LLMs is an exciting time, and that the NCSC is among the organisations that want to explore and
benefit from it.
