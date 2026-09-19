---
title: "Role Confusion"
type: "schema:DefinedTerm"
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
  description: "A proposed name for the mechanism underlying prompt injection: a model's failure to reliably tell its own privileged text from untrusted input, because it judges a passage's role largely by writing style rather than by the role tags delimiting it."
---

Role confusion is the name researchers give to a language model's failure to reliably perceive which
role a passage of text belongs to — whether it is the model's own privileged content, wrapped in tags
such as `<system>`, `<think>` or `<assistant>`, or untrusted input wrapped in `<user>`. The finding
the term rests on is not merely that models make this distinction imperfectly, but that they appear
to weigh a passage's *style* more heavily than the role tag actually delimiting it, so that text
written to look like a model's internal reasoning is treated with something closer to the authority
of internal reasoning.

## Usage

The term is used to reframe [[DefinedTerm/prompt-injection]] as a perceptual problem rather than a
parsing one. Role tags are a delimiting mechanism, and the research the term comes from treats their
failure as evidence that delimiting is not what the model is actually keying on. The practical
demonstration reported is a jailbreak: a request the model would ordinarily refuse, followed by text
in the register of a thinking block asserting a permissive policy conditional on some incidental
detail of the request, can override the model's initial training — reported as effective against
models such as `gpt-oss-20b`.

The counterpart technique is **destyling**: rewriting a passage so that it reads less like the format
expected inside its role tag, while leaving its meaning intact. The researchers are quoted as
measuring average attack success across their dataset falling from 61% to 10% under destyling, and as
characterising that change as nearly invisible to a human reader yet decisive for the model's role
perception. Those figures reach this wiki at one remove: they are quoted by
[[BlogPosting/prompt-injection-as-role-confusion]] from the researchers' own blog-style writeup of
their work, which is not itself held as a source here.

Two consequences are drawn by the researchers as quoted. The first is that injection defence will
remain a perpetual whack-a-mole game unless models achieve genuine role perception; they describe
role confusion as a key challenge in addressing prompt injection in today's models. The second is
that the continuity of role boundaries opens a further threat: injections designed to shift a model's
state subtly through text that looks innocuous, which the researchers describe as deployable legally
and at scale.

## Related Terms

[[DefinedTerm/prompt-injection]], [[DefinedTerm/jailbreaking]],
[[DefinedTerm/indirect-prompt-injection]], [[DefinedTerm/control-data-plane-confusion]],
[[DefinedTerm/two-channel-prompt-injection]], [[BlogPosting/prompt-injection-as-role-confusion]]
