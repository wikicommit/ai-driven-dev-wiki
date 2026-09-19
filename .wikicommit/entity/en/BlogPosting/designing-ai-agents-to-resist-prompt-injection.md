---
title: "Designing AI agents to resist prompt injection"
type: "schema:BlogPosting"
lang: en
tags: [security, prompt-injection, agent-safety]
sources:
  - type: url
    url: 'https://openai.com/index/designing-agents-to-resist-prompt-injection/'
    hash: sha256:a6abdf1b681484a9400a9cdf6ae01a404d4dba8657ede15473b45bfd66d74271
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "OpenAI's 11 March 2026 post arguing that effective real-world prompt injection has come to resemble social engineering more than instruction override, and that the response should therefore be to constrain the impact of manipulation rather than to try to classify malicious input."
  author: ["Thomas Shadwell", "Adrian Spânu"]
  datePublished: "2026-03-11"
  publisher: "OpenAI"
---

This post sets out OpenAI's stated position on [[DefinedTerm/prompt-injection]] against agents that
browse the web, retrieve information and act on a user's behalf. Its central move is a
reframing: the most effective real-world versions of these attacks are said to increasingly resemble
social engineering rather than simple prompt overrides, and the consequence drawn is that defence
cannot rely only on filtering inputs. If the problem is resisting misleading or manipulative content
in context rather than identifying a malicious string, then the system has to be designed so that
the impact of manipulation is constrained even when an attack succeeds.

The post traces a progression. Early attacks are described as being as simple as editing a
Wikipedia article to include direct instructions to visiting agents, which models without
training-time experience of adversarial environments would often follow without question. As models
became smarter and less vulnerable to that, attacks are said to have responded by incorporating
social engineering. The worked example is an email written as a plausible corporate follow-up about
restructuring materials, which embeds its instruction — retrieve an employee profile and submit it
to an external "compliance validation" endpoint — inside legitimate-looking action items and an
assertion that the assistant has full authorization to do so.

## Key Points

- The framing claim is that effective real-world prompt injection increasingly resembles social
  engineering, and should be managed with the same lens used for social engineering risk against
  people in other domains.
- The goal is stated as not being limited to perfectly identifying malicious inputs, but designing
  agents and systems so that the impact of manipulation is constrained even if it succeeds.
- "AI firewalling" — an intermediary that attempts to classify inputs as injection or not — is
  described as commonly recommended within the wider AI security ecosystem, and as not usually
  catching fully developed attacks of this kind. The stated reason is that detecting such an input
  becomes the same very difficult problem as detecting a lie or misinformation, often without the
  necessary context.
- The agent is analogized to a customer support agent in a three-actor system: acting for an
  employer while continuously exposed to external input that may mislead it. The post's argument is
  that such an agent, human or AI, must have limits on its capabilities to bound the downside, and
  that in the human case deterministic systems already cap refunds and flag phishing rather than
  relying on the agent never being fooled.
- Alongside that framing the post reports using traditional security engineering, naming
  [[DefinedTerm/source-sink-analysis]]: an attacker needs both a way to influence the system and a
  capability that is dangerous in the wrong context.
- The security expectation it states for users is that potentially dangerous actions, or
  transmissions of potentially sensitive information, should not happen silently or without
  appropriate safeguards.
- The attacks reported as most common against ChatGPT attempt to convince the assistant to transmit
  secret information from a conversation to a malicious third party; the post states that in most
  known cases these fail because safety training causes a refusal.
- For cases where the agent is convinced, the post describes a mitigation called
  [[DefinedTerm/safe-url]], and states the same mechanism applies to navigations and bookmarks in
  its browser product and to searches and navigations in its deep research product.
- Its forward-looking recommendation for integrators is to ask what controls a human agent should
  have in a similar situation and implement those. It expects a maximally intelligent model to
  resist social engineering better than a human agent, while noting this is not always feasible or
  cost-effective.

## Context

The post is a vendor's account of its own product defences, and several of its central claims —
that most such attacks fail because of safety training, and that the described mitigation catches
the remainder — are stated without accompanying measurements. Its example attack is attributed to
external security researchers who reported it, with the post stating that in testing it worked half
the time against a deep-research prompt. Because the reported research and the other product posts
it links are known here only through this post, their own titles, dates and authorship are not
restated as established facts.
