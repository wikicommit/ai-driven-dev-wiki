---
title: "Jailbreaking"
type: "schema:DefinedTerm"
lang: en
tags: [llm, security, agent-safety]
sources:
  - type: url
    url: 'https://docs.anthropic.com/en/docs/test-and-evaluate/strengthen-guardrails/mitigate-jailbreaks'
    hash: sha256:cccb2171881ac7e3fdad07195764b42fff863153b2b262af3fd66a5ff5c7779c
  - type: url
    url: 'https://simonwillison.net/2024/Mar/5/prompt-injection-jailbreaking/'
    hash: sha256:03253e283263bfa4feaf0bb8e37840fdfebd27239d9b8c6a1b186cf5bc19d34a
  - type: url
    url: 'https://www.ibm.com/topics/prompt-injection'
    hash: sha256:a266835677476a694038cea4bd96f4ae88e318fe878bc7adcc4a28c90d8f3144
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An attempt to make a language model ignore its own guidelines or the instructions an application gave it. Simon Willison defines it narrowly as the class of attacks that try to subvert the safety filters built into the models themselves, as against prompt injection, which targets applications; Anthropic's documentation instead groups it with direct prompt injection under one threat model, in which the application's own user is the adversary. An IBM explainer separates the two on a third basis — disguise versus disregard."
---

Jailbreaking is an attempt to make a language model ignore its guidelines or the instructions the
application built on it gave it. Anthropic's platform documentation, which states this of Claude
specifically, treats jailbreaking and prompt injection together as attempts at the same thing, and
says Claude is inherently resilient to such attacks while still recommending additional
application-level measures — particularly against uses that would violate Anthropic's Terms of
Service or Usage Policy.

## Usage

What that documentation organises the two around is not the technique but the threat model, and it
puts jailbreaking on the same side as *direct* [[DefinedTerm/prompt-injection]]: the user of the
application is the adversary, deliberately crafting inputs intended to bypass the application's
guardrails. It sets this against [[DefinedTerm/indirect-prompt-injection]], where the user is
trusted and the adversarial instructions instead arrive inside third-party content the model
processes on that user's behalf — a fetched web page, an inbound email, a document, a tool result.

Because the adversary in this model is the person typing, the four mitigations Anthropic lists
under this heading operate on the application's own input path and on its relationship with that
person:

- **Harmlessness screens** — pre-screen user input with a lightweight model such as Claude Haiku
  4.5 before it reaches the main conversation, using structured outputs to constrain the answer to
  a simple classification such as a single `is_harmful` boolean.
- **Input validation** — filter input for known injection patterns before it reaches the model,
  optionally using an LLM to generalise a validation screen from examples of known jailbreaking
  language.
- **Prompt engineering** — write system prompts that state ethical and legal boundaries explicitly
  and tell the model how to refuse, the documentation's example being a values block followed by a
  fixed refusal sentence.
- **Responding to repeat offenders** — adjust responses and consider throttling or banning users
  who repeatedly attempt to circumvent the application's guardrails, telling the user their actions
  violate the relevant usage policies.

That last one has no counterpart on the indirect side, and it is the clearest sign of what the
threat model is doing: it is a measure against a person, not against a payload.

A second account draws the line differently, and does so on purpose. Writing in
[[BlogPosting/prompt-injection-and-jailbreaking-are-not-the-same-thing]], Simon Willison defines
jailbreaking as the class of attacks that attempt to subvert safety filters built into the LLMs
themselves, and prompt injection as a class of attacks against applications built on top of LLMs
that work by concatenating untrusted user input with a trusted prompt the developer wrote. On that
reading the two are separated by *what they target* rather than by who the adversary is: where
there is no concatenation of trusted and untrusted strings, he says, it is not prompt injection.
That puts jailbreaking on the other side of the line from where Anthropic's documentation puts
it — the two framings disagree about the grouping, not about what either attack does.

He argues the distinction matters because the stakes are not the same. The common risk he
attributes to jailbreaking is a "screenshot attack" — someone gets a model to say something
embarrassing and causes a PR incident — with a theoretical worst case of the model helping someone
commit a crime they could not otherwise have committed, of which he says he has not heard a
real-world example. Prompt injection he treats as far more serious, because its severity is set by
what the application can reach.

The practical consequence he draws is about buying defences: a vendor's prompt-injection detection
system trained on jailbreaking attacks may block a jailbreak-shaped prompt while letting through an
instruction telling an assistant to forward a user's data to an attacker, because that second
attack is specific to the application and not something a jailbreak-trained system has seen.

He also accepts a large overlap. Some safety features are baked into the models, but many of those
in chat applications are implemented through a concatenated system prompt and are therefore
vulnerable to prompt injection; sometimes a model can be jailbroken *by* prompt injection, and
sometimes a prompt-injection defence — especially one that relies on AI to detect attacks — can be
broken by jailbreaking techniques.

A third account, an IBM explainer, separates the two on a different basis again: prompt injections
disguise malicious instructions as benign inputs, while jailbreaking makes an LLM ignore its
safeguards. On that reading the distinction is between concealment and refusal rather than between
targets or adversaries. It describes system prompts as carrying not only instructions but
safeguards — its illustration being a translation chatbot told not to translate statements
containing profanity — so that jailbreaking means writing a prompt that convinces the model to
disregard them, often by asking it to adopt a persona or play a game. It names "Do Anything Now", or
DAN, as a common technique of that kind, in which the user asks the model to assume the role of an AI
with no rules.

That account also describes the dynamic around the technique as an arms race: safeguards make
jailbreaking harder, hackers and hobbyists work on prompts to beat the latest rulesets, working
prompts are shared online, and developers update their safeguards in response. Like the second
account, it holds that injection and jailbreaking are ultimately two distinct techniques while
accepting that each can enable the other — prompt injections can be used to jailbreak a model, and
jailbreaking tactics can clear the way for a successful prompt injection.

## Related Terms

- [[DefinedTerm/prompt-injection]] — named alongside jailbreaking in the same documentation as the other way a model's guidelines are attacked, and grouped with it under one threat model in its direct form
- [[DefinedTerm/indirect-prompt-injection]] — the other threat model in the same documentation
- [[DefinedTerm/guardrails]] — what a jailbreak attempts to get past
- [[BlogPosting/prompt-injection-and-jailbreaking-are-not-the-same-thing]] — the source of the second account
- [[DefinedTerm/semantic-diffusion]] — the concern that post raises about its own coined term
