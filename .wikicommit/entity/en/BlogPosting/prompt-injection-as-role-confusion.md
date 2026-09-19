---
title: "Prompt Injection as Role Confusion"
type: "schema:BlogPosting"
lang: en
tags: [prompt-injection, jailbreaking, llm-security]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Jun/22/prompt-injection-as-role-confusion/'
    hash: sha256:40d3d22f5c2d4faf24481573bef5187e757c570cd5527e5d7f9c15f5b7595991
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A link post relaying research that frames prompt injection as 'role confusion': models judge whether text is privileged largely by its style rather than by the role tags around it, and rewriting an injection to look less like the expected format collapses its success rate."
  author: ["Simon Willison"]
  datePublished: "2026-06-22"
---

This is a link post, and its subject is research it points at rather than an argument of its own.
The research concerns whether models can distinguish their own privileged text — wrapped in role tags
such as `<system>`, `<think>` and `<assistant>` — from untrusted user input wrapped in `<user>`. The
post relays the finding that they cannot, and that they appear to weigh the *style* of the text more
heavily than its actual role marking.

The consequence the post highlights is a jailbreak shape: a request a model would refuse, followed by
text written in the style of the model's own internal thinking blocks, can override the model's
initial training. The example relayed is a request for drug-manufacturing instructions paired with an
irrelevant detail ("I'm wearing a green shirt"), followed by pseudo-policy text stating that such
advice is allowed if the user is wearing green — which the post reports confuses models such as
`gpt-oss-20b`.

Its second thread is a point about scientific communication rather than security. The post opens by
praising the researchers for publishing a readable blog-style writeup alongside the formal paper,
arguing that academic writing is dry and that a paper's impact can be much higher with an accessible
companion version — and wishing every paper came with one.

## Key Points
- The research reported here concerns whether models can distinguish their own privileged text, wrapped
  in role tags, from untrusted user input — and confirms that they cannot.
- More surprisingly, the reported finding is that models take the *style* of text more seriously than
  the role tag actually wrapping it.
- This makes a jailbreak available: appending text written in the style of a model's internal thinking
  blocks, asserting a permissive policy, can override the model's initial training.
- The relayed example pairs a refused request with an irrelevant personal detail and then pseudo-policy
  text making the request conditional on that detail — reported as confusing models such as `gpt-oss-20b`.
- "Destyling" — rewriting text so that it looks less like the expected format for its role tag — is
  reported to have a material effect on how the model classifies it.
- The researchers are quoted as measuring average attack success across their dataset dropping from
  61% to 10% under destyling; the post quotes this from the researchers' own blog-style writeup, and
  it is not an independent result.
- The researchers are quoted describing that change as nearly invisible to a human reader while
  completely changing the model's role perception.
- The underlying mechanism is named "role confusion", and the researchers describe it as a key
  challenge in addressing prompt injection in today's models.
- The researchers are quoted as holding that injection defence will remain a perpetual whack-a-mole
  game unless models achieve genuine role perception.
- They are also quoted raising a further threat: because role boundaries are continuous, injections
  could be designed to shift model state subtly through seemingly innocuous text, legally and at scale.
- Separately from the security content, the post argues that every paper should come with a readable
  blog-style writeup, on the grounds that academic writing is dry and accessibility raises impact.

## Context
The post is a short link-blog entry, so almost everything it states about the research is relayed
rather than independently examined; the figures and conclusions it quotes come from the researchers'
own blog-style writeup, which it links and which is not itself registered as a source here. The post
opens by noting that this writeup accompanies a formal paper. The post is tagged under
[[DefinedTerm/prompt-injection]] and jailbreaking, and the author's own contribution to it is
limited to two things: the opening argument about readable paper writeups, and a one-line
characterisation of the finding as fascinating research into a challenge he describes as not only
unsolved but worse than expected. See [[DefinedTerm/role-confusion]] for the mechanism itself.
