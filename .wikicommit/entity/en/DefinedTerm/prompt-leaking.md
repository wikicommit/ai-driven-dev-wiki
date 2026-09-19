---
title: "Prompt Leaking"
type: "schema:DefinedTerm"
lang: en
tags: [security, prompt-injection, llm]
sources:
  - type: url
    url: 'https://simonwillison.net/2022/Sep/12/prompt-injection/'
    hash: sha256:2d2b741596804f79993a763d44b45e8307bef3e18b62aa98912d397b49a1fa23
  - type: url
    url: 'https://www.ibm.com/topics/prompt-injection'
    hash: sha256:a266835677476a694038cea4bd96f4ae88e318fe878bc7adcc4a28c90d8f3144
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An application of prompt injection in which the attacker induces the model to reveal the system prompt it was given. The leaked text matters both as a commercial asset and as a template: knowing the developer's wording makes subsequent injected input easier to disguise as legitimate instruction."
---

Prompt leaking is the use of [[DefinedTerm/prompt-injection]] to make a model disclose the system
prompt an application gave it. [[BlogPosting/prompt-injection-attacks-against-gpt-3]] demonstrates
it directly: asking a translation application to output the translation as "LOL" instead, followed
by a copy of the full prompt text, caused GPT-3 to emit the original instruction along with a
translation of the injected request. That post reports the attempt as the first its author found
that worked.

Two distinct reasons are given for why the leak matters. The first is commercial: a prompt becomes
important intellectual property, and it is not hard to imagine startups whose secret sauce is a
carefully crafted prompt. The second, from an IBM explainer, is operational — a system prompt may
not be sensitive in itself, but attackers can use it as a template for crafting further malicious
input, because input resembling the system prompt is more likely to be complied with.

## Usage

The attack is reported to work against deployed systems, not only against demonstrations. The same
post records a case in the wild: a recruitment startup's Twitter bot, which replied to mentions of
remote work using GPT-3, was induced to disclose that its initial instructions were to respond to
the tweet with a positive attitude towards remote work in the first-person plural. The IBM account
gives a second instance, reporting that a Stanford University student got Microsoft's Bing Chat to
divulge its programming with a prompt telling it to ignore previous instructions and report what was
written at the beginning of the document above.

The IBM explainer lists prompt leaks first among the common effects of prompt injection attacks,
alongside remote code execution, data theft, misinformation campaigns and malware transmission.

## When It Applies

The technique applies wherever an application places a developer-authored instruction in the same
context as attacker-reachable input — which, on both accounts here, is the ordinary way such
applications are built. It assumes only that the model can be induced to treat the prompt as
material to report rather than as instructions to follow.

Its practical significance depends on what the prompt contains: where a system prompt is merely
functional, the loss is the advantage it gave in disguising later attacks rather than the text
itself. Mitigations are not separately enumerated for this effect in either source; it is treated as
one consequence of an attack class that both describe as unresolved.

## Related Terms

- [[DefinedTerm/prompt-injection]] — the attack class this is an application of
- [[BlogPosting/prompt-injection-attacks-against-gpt-3]] — the post that demonstrates it
- [[DefinedTerm/jailbreaking]] — a neighbouring attack against the model's own safeguards
- [[DefinedTerm/prompt-engineering]] — the practice that produces the prompts at stake here
