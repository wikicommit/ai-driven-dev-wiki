---
title: "Context-Minimization Pattern"
type: "schema:DefinedTerm"
lang: en
tags: [security, prompt-injection, agent-architecture, agent-safety]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Jun/13/prompt-injection-design-patterns/'
    hash: sha256:bd74a0ffe03b1f53850aa0b16d091950d2f2544de525ebb6dade120e2b8ab4c4
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A design pattern in which an agent system removes unnecessary content — including the user's own original prompt — from the context across successive interactions, so that injected instructions cannot persist into a later step where they would take effect."
---

The context-minimization pattern defends against injection by discarding context that is no longer
needed. As quoted in [[BlogPosting/design-patterns-for-securing-llm-agents]], the paper states that
to prevent certain user prompt injections the agent system can remove unnecessary content from the
context over multiple interactions. What distinguishes it from the other five patterns in the same
group is the direction of the threat: the content being removed is the user's own prompt, so the
adversary being guarded against is the person making the request.

## Usage

The example given is a customer service chatbot. A malicious user asks for a quote on a new car and
attempts to inject an instruction granting a large discount. The system first converts the user's
request into a database query — to find the latest offers — and then, before returning the results
to the customer, removes the user's prompt from the context, so that the injected instruction is no
longer present when the response is produced.

The reviewing post records that it is slightly confused by this pattern before offering its own
reading: if a user's prompt is turned into a SQL query that returns raw data, and that data is
returned in a way that cannot include any text from the original prompt, then any chance of an
injection surviving should be eliminated. That reading is the post's own interpretation rather than
a restatement of the paper, and the post presents it as such.

## When It Applies

The pattern applies where the user's request can be reduced to a structured intermediate — a query,
a parameter set — that captures everything later steps need, so that the original wording can be
dropped without losing the request. It assumes such a reduction is possible and that no downstream
step needs the raw prompt. It is misapplied in settings where the user's exact phrasing must survive
into the response, and it addresses only instructions carried in the removed content: material
arriving from retrieved documents or tool results is a different exposure, which the other patterns
in the group address.

It is one of six patterns presented together as trade-offs between utility and resistance to
[[DefinedTerm/prompt-injection]], and the account here is the reviewer's rather than the paper's.

## Related Terms

- [[DefinedTerm/prompt-injection]] — the attack class, in the direct form where the user is the adversary
- [[DefinedTerm/jailbreaking]] — the neighbouring attack that also has the application's own user as
  the adversary
- [[DefinedTerm/context-engineering]] — the general practice of managing what occupies a model's
  context, here applied to a security end
- [[BlogPosting/design-patterns-for-securing-llm-agents]] — the source of this account
