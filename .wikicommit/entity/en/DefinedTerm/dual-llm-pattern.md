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
  - type: url
    url: 'https://simonwillison.net/2025/Jun/13/prompt-injection-design-patterns/'
    hash: sha256:bd74a0ffe03b1f53850aa0b16d091950d2f2544de525ebb6dade120e2b8ab4c4
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Simon Willison's proposed mitigation for prompt injection in assistant applications: build the assistant out of two language models, a privileged one that holds the tools and only ever sees trusted input, and a quarantined one that reads untrusted content, with the privileged model addressing the quarantined model's inputs and outputs only as opaque variables it never reads. It was later taken up as one of six design patterns in a multi-institution paper."
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

A later account by the same author, in
[[BlogPosting/design-patterns-for-securing-llm-agents]], restates the same mechanism in the
vocabulary of the paper reviewed there: a privileged LLM co-ordinates a quarantined LLM while
avoiding any exposure to untrusted content, and the quarantined LLM returns symbolic variables —
the example given is a variable standing for a summarized web page — which the privileged LLM can
ask to have shown to the user without being exposed to the tainted content itself. He reports that
the paper describes his exact pattern and illustrates it with a diagram.

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

How well-established it is: it began as one researcher's proposal, presented in a talk as his own
attempt to put forward something workable after arguing that the alternatives fail. It has since
been taken up beyond its author — the second source reports that a paper by authors from several
organizations includes it among six recommended design patterns, and that an earlier paper
proposing what became the [[DefinedTerm/code-then-execute-pattern]] was itself influenced by it.
That is uptake in the literature rather than evidence of deployment or measured effectiveness, and
the author's own reservations above are not withdrawn in the later account.

## Related Terms

- [[DefinedTerm/prompt-injection]] — the attack this pattern is proposed against
- [[DefinedTerm/indirect-prompt-injection]] — the variant that arrives through retrieved content
- [[DefinedTerm/code-then-execute-pattern]] — described as an improved version of this pattern
- [[DefinedTerm/llm-map-reduce-pattern]] — a neighbouring pattern in the same group, containing
  untrusted content in sub-agents rather than behind opaque variables
- [[DefinedTerm/fides]]
- [[DefinedTerm/sandboxing]]
- [[BlogPosting/design-patterns-for-securing-llm-agents]] — the source of the later account
