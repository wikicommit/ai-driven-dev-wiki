---
title: "Prompt-injection defense patterns compared"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-26"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/BlogPosting/design-patterns-for-securing-llm-agents.md
    source_commit: a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a
  - path: .wikicommit/entity/en/DefinedTerm/dual-llm-pattern.md
    source_commit: a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a
  - path: .wikicommit/entity/en/DefinedTerm/action-selector-pattern.md
    source_commit: a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a
  - path: .wikicommit/entity/en/DefinedTerm/plan-then-execute-pattern.md
    source_commit: a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a
  - path: .wikicommit/entity/en/DefinedTerm/llm-map-reduce-pattern.md
    source_commit: a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a
  - path: .wikicommit/entity/en/DefinedTerm/code-then-execute-pattern.md
    source_commit: a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a
  - path: .wikicommit/entity/en/DefinedTerm/context-minimization-pattern.md
    source_commit: a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a
  - path: .wikicommit/entity/en/DefinedTerm/structured-query.md
    source_commit: 6b5a8ac7a493c71300dccb7564cd1bdadb65f53c
  - path: .wikicommit/entity/en/DefinedTerm/fides.md
    source_commit: 7b07912e0ef7183c203dba9eea44e8052dcec715
  - path: .wikicommit/entity/en/DefinedTerm/safe-url.md
    source_commit: ac679fb0b8398751f97b635791af1ae0e67cb150
---

Several pages in this wiki describe designs meant to stop [[DefinedTerm/prompt-injection]] from
turning into harmful agent behaviour. Six of them come from a single paper, known here only through
Simon Willison's review of it in [[BlogPosting/design-patterns-for-securing-llm-agents]]. Three more
come from separate sources: a USENIX Security paper, an architecture decision record in Microsoft's
agent framework, and an OpenAI post. This page sets them side by side and draws out where they
differ. It does not rank them — the six are presented in their source as trade-offs between an
agent's utility and its resistance to injection rather than as a ranked list, and the other three
come from different settings.

## The premise the six share

The review highlights the paper's organising principle: once an agent has ingested untrusted input,
it must be constrained so that it is impossible for that input to trigger consequential actions. It
quotes the paper's view that, as long as both agents and their defences rely on the current class of
language models, general-purpose agents are unlikely to provide meaningful and reliable safety
guarantees. The review calls the willingness to limit agents' ability to perform arbitrary tasks an
unpopular trade-off. Each of the six patterns accepts a narrower agent in exchange for a specific
protection, and they differ in what they give up.

## The six patterns side by side

| Pattern | What untrusted content can reach | What stays protected | What it gives up or assumes |
|---|---|---|---|
| [[DefinedTerm/action-selector-pattern]] | Nothing: no feedback from an action is allowed back into the agent | The agent's choice of action, completely | Actions whose purpose is retrieval (reading an email, fetching a page) are unavailable; assumes a set of self-contained actions can be enumerated in advance |
| [[DefinedTerm/plan-then-execute-pattern]] | Tool output returns to the agent, but only after its sequence of tool calls has been fixed | Which tools run, and parameters fixed at planning time — in the example, the email's recipient | The content of later steps stays exposed — in the example, the email's body; assumes the plan can be formed from the request alone |
| [[DefinedTerm/llm-map-reduce-pattern]] | Sub-agents read the untrusted items; the coordinator receives only their constrained results (a boolean per file in the example) | The coordinator never sees the untrusted text | Assumes the task reduces to independent per-item judgements; a sub-agent can still be wrong about its own item |
| [[DefinedTerm/dual-llm-pattern]] | A quarantined LLM reads it; the privileged LLM handles it only as opaque variables | The privileged LLM, which holds the tools, never reads tainted text | Assumes the work can be expressed as operations on opaque handles; its author calls building such systems really fiddly |
| [[DefinedTerm/code-then-execute-pattern]] | Tool outputs flow through a program the privileged model wrote in a sandboxed domain-specific language | Where tainted data travels, tracked through data flow analysis before anything runs | Assumes a custom language and a sandbox to run it in; guarantees are bounded by what the analysis models |
| [[DefinedTerm/context-minimization-pattern]] | The user's own prompt, until it has been converted into a structured intermediate such as a database query | An instruction injected in the user's prompt is no longer in context when the response is produced | Addresses only the content removed, not retrieved documents or tool results; unsuitable where the user's exact phrasing must survive into the response |

## How the six relate to each other

The pages describe the patterns as neighbours, each answering something another leaves open.
Action-selector is the stricter neighbour of plan-then-execute: one admits no tool output at all,
the other admits it but only after the choice of actions is settled. LLM map-reduce addresses the
exposure plan-then-execute leaves — malicious instructions affecting the content passed to a later
step — by keeping untrusted text inside sub-agents whose output shape is constrained. The dual LLM
pattern also quarantines untrusted reading behind another model, but returns symbolic variables
rather than aggregated judgements. Code-then-execute is described as an improved version of the dual
LLM pattern: where the dual LLM pattern keeps untrusted content in opaque variables, a program in a
purpose-built language additionally lets the system reason about which tool consumes a tainted value.

Context-minimization differs in the direction of the threat. In the other five, the untrusted text
arrives from outside — a web page, an email, a file. Here the content removed is the user's own
prompt, so the adversary is the person making the request; the example is a customer asking a
service chatbot for a car quote while trying to inject a discount. The review says it is slightly
confused by this pattern, and its own reading of it is presented as an interpretation rather than as
the paper's statement.

## Designs from outside the six

**[[DefinedTerm/structured-query]]** changes the interface to the model rather than the agent built
around it. An input is sent as two separate parts, a prompt and data, and the model is trained to
follow instructions found only in the prompt part. Its source, [[ScholarlyArticle/struq]], reaches
the idea by analogy with classic injection attacks and names SQL prepared statements as the model
fix. It is stated to apply to programmatic LLM-integrated applications and not to web chatbots with
open-ended multi-turn conversation, and it is not designed to defend against jailbreaks or data
extraction.

**[[DefinedTerm/fides]]** enforces labels in framework middleware. Content carries an integrity label
and a confidentiality label, combined under a most-restrictive-wins policy; middleware propagates the
labels and checks policy before a tool call executes. Two of its components correspond to mechanisms
the dual LLM pattern's page describes: variable indirection, which keeps untrusted content out of the
model's context behind references, and a quarantined path in which untrusted data is processed. Its
decision record weighs it against prompt-engineering defences, content sanitization, separate agent
instances and runtime monitoring alone, and rejects each.

**[[DefinedTerm/safe-url]]** acts at the point where information would leave. It detects when
information the assistant learned in a conversation would be transmitted to a third party, and
either shows the user what would be sent and asks for confirmation, or blocks the transmission and
tells the agent to find another way. It is aimed at exfiltration specifically, and its source places
it behind safety training: it handles the rare cases where the agent has already been convinced.

## Where each one intervenes

The nine designs act at different places:

- **In the agent's structure** — the six patterns, which decide which component may read untrusted
  content and what may flow from it to the component that acts.
- **In the model's input interface and training** — structured query, which separates prompt from
  data and fine-tunes an existing model to respect the separation.
- **In framework middleware** — FIDES, which propagates labels and checks policy on each tool call,
  opt-in and per agent or tool.
- **At the outgoing transmission** — Safe Url, which asks the user or blocks when data would go to a
  third party, making it a [[DefinedTerm/human-in-the-loop]] control in the case where it asks.

## What stands behind each

The kind of evidence differs as much as the designs do:

- **The six patterns** are known here through a review rather than the paper itself. The review
  reports that the paper closes with ten case studies, each with threat models and mitigations. For
  the dual LLM pattern, its page notes that it began as one researcher's proposal and that its uptake
  in the literature is not evidence of deployment or measured effectiveness.
- **Structured query** has one implementation, evaluated by its own authors on two 7B open-source
  models; the paper's own conclusion is that it is a promising direction rather than a settled one.
- **FIDES** is recorded in a decision document carrying the status *proposed*. Performance
  benchmarks and user acceptance testing are left unchecked in it, and it says nothing either way
  about whether the design has shipped.
- **Safe Url** is one vendor's description of its own deployed defence. No effectiveness figures and
  no independent evaluation appear in its source.
