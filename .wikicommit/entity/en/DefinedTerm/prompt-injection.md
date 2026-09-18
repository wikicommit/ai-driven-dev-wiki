---
title: "Prompt injection"
type: "schema:DefinedTerm"
lang: en
tags: [agents, llm, security, agent-safety]
sources:
  - type: url
    url: 'https://www.preamble.com/prompt-injection-a-critical-vulnerability-in-the-gpt-3-transformer-and-how-we-can-begin-to-solve-it'
    hash: sha256:d50c6e50f004ff07f866bd42358fe7440c72f3ec8a51cebfdd37d08b4e5a2ad8
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A vulnerability of large language models in which natural-language input supplied through the prompt overrides the model's built-in guardrails, letting a user issue commands the system was meant to refuse. First reported against GPT-3 in May 2022 under the name command injection, and renamed prompt injection several months later."
---

Prompt injection is a vulnerability of large language models in which an attacker uses ordinary
natural-language input to override the guardrails the model operates under, so that the model
carries out instructions its operator intended to prevent. Preamble, which reported the
vulnerability to OpenAI in 2022, originally referred to it as **command injection**, citing the
similarities to traditional SQL injection and command injection attacks: a user could issue
commands through a natural-language based prompt and so override the guardrails inherent to GPT-3.
The name *prompt injection* was applied to it only later.

## Usage

Preamble's account places the discovery in May 2022. The company made a private responsible
disclosure to OpenAI on 3 May 2022; OpenAI confirmed receipt the same afternoon, and Preamble
supplied further examples the following day. The disclosure remained private until Preamble declassified it on
22 September 2022, publishing the correspondence in order — in the company's own words — to
establish an accurate historical record of the vulnerability and to promote AI security research.

The name the field settled on came from outside that disclosure. Preamble records that the term
*prompt injection* was coined several months after its report by the AI security researcher Simon
Willison. The two facts are worth keeping apart: on Preamble's account the company discovered and
disclosed the vulnerability, while the name by which it is now known was supplied later by someone
else.

Preamble describes the vulnerability as unresolved rather than historical. It reports that prompt
injections continue to affect generative AI and LLM products through both **direct** and
**indirect** attack methods, and that AI agents raise the likelihood of exploitation specifically
because their additional API integrations give an attacker a larger attack surface to work
against.

## Related Terms

- [[DefinedTerm/indirect-prompt-injection]] — the variant in which the adversarial instructions are
  planted in data the application retrieves, rather than typed in by the attacker directly
- [[DefinedTerm/tool-poisoning]] — an injection attack that hides its instructions in a tool's own
  description or metadata
- [[DefinedTerm/two-channel-prompt-injection]] — a tool-invocation hijack that splits its payload
  across a tool's description and its return value
- [[DefinedTerm/guardrails]] — the policy and control frameworks placed around AI agents, a broader
  sense of the word than the model-inherent guardrails this source describes
