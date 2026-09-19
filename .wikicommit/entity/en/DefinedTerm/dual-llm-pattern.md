---
title: "Dual LLM Pattern"
type: "schema:DefinedTerm"
lang: en
aliases: ["Dual language model pattern"]
tags: [llm, security, agent-safety, agent-architecture]
sources:
  - type: url
    url: 'https://simonwillison.net/2023/May/2/prompt-injection-explained/'
    hash: sha256:0d92bc59d6b47bea9a692f7ac853d8e13f2857879ab57db58c2e47b4e30fc1d3
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Simon Willison's proposed mitigation for prompt injection in assistant applications: build the assistant out of two language models, a privileged one that holds the tools and only ever sees trusted input, and a quarantined one that reads untrusted content, with the privileged model addressing the quarantined model's inputs and outputs only as opaque variables it never reads."
---

The dual LLM pattern — which Simon Willison also calls the dual language model pattern — is a way
of building an assistant application out of two separate language models so that the component
holding dangerous capabilities never reads attacker-controllable text. He proposes it as a
mitigation for [[DefinedTerm/prompt-injection]], and offers it with an explicit caveat: he
introduces it saying he has a potential solution, does not think it is very good, and asks that it
be taken with a grain of salt.

## Usage

The split is by privilege. The **privileged LLM** is the one with access to tools — Willison's
examples are deleting emails and unlocking his house — and it is only ever exposed to trusted
input; it is crucial, on his account, that nothing untrusted reaches it. The **quarantined LLM**
is the one expected to go rogue: it reads emails, summarizes web pages, and absorbs whatever
nastiness arrives with them, and has no access to anything else. All of its input and output is
treated as tainted and never passed directly to the privileged model.

What makes that separation work is indirection. The privileged model never sees the untrusted
content; it sees variables instead, and deals in tokens. Willison's worked sequence is that the
privileged model knows an email body has arrived and is called `$var1` without having seen it, asks
the quarantined model to summarize `$var1`, gets a result saved as `$summary2` — again without
seeing it — and can then tell the display layer to show that summary to the user.

## When It Applies

The pattern is aimed at the case Willison treats as the dangerous one: an assistant with tools
that acts on content other people can write. His running example is an email assistant that can
read, summarize and reply, where an incoming message saying to search for password-reset emails
and forward them to an attacker is indistinguishable, to a naive design, from an instruction from
the owner. He also names exfiltration attacks in the same setting — instructing the model to
base64-encode private data onto the end of a URL and induce the user to click it — as a class that
matters even where no destructive action is available.

What it assumes is that the work can be expressed as operations on opaque handles, which is also
where its cost lies: Willison says building these systems is not going to be fun, that it is
really fiddly, and that there are all sorts of things that cannot be done with them. His own
assessment is that it is a terrible solution which may nonetheless be the best available in the
absence of rock-solid, 100% reliable protection against prompt injection.

How well-established it is: this is one researcher's proposal, presented in a talk as his own
attempt to put forward something workable after arguing that the alternatives fail, and he says he
has written it up in more detail separately. It is offered as a design direction rather than a
tested or adopted defence.

## Related Terms

- [[DefinedTerm/prompt-injection]] — the attack this pattern is proposed against
- [[DefinedTerm/indirect-prompt-injection]] — the variant that arrives through retrieved content
- [[DefinedTerm/fides]]
- [[DefinedTerm/sandboxing]]
