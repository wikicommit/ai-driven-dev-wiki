---
title: "Lethal Trifecta"
type: "schema:DefinedTerm"
lang: en
tags: [agent-security, prompt-injection, tool-use, exfiltration]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/'
    hash: sha256:0af6dbc8f6a6fb02d0257c9c4aa852d009e4afdd442ba84dd828c21a84d987dd
  - type: url
    url: 'https://simonwillison.net/2025/Oct/20/claude-code-for-web/'
    hash: sha256:45fb7060c3561e36111229e2a76520baefc9e1538596494a73f3ba55f27fb826
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Simon Willison's name for the combination of three capabilities that, held together by one LLM agent, lets an attacker steal a user's data: access to private data, exposure to untrusted content, and the ability to communicate externally."
---

The lethal trifecta is the name Simon Willison gives to a combination of three capabilities which,
when a single tool-using LLM system holds all of them at once, allows an attacker to trick it into
taking a user's private data and sending it to the attacker. The three are **access to private
data**, which is usually the whole reason the tools were connected; **exposure to untrusted
content**, meaning any path by which text or images controlled by an attacker can reach the model;
and **the ability to communicate externally** in a way that can carry data out. The argument is that
the danger is a property of the combination rather than of any one capability — each is ordinary and
useful on its own.

## Usage

The underlying mechanism is [[DefinedTerm/prompt-injection]]. LLMs follow instructions found in
content, and the source argues they cannot reliably distinguish instructions by origin, because
everything is ultimately concatenated into one token sequence handed to the model. So a page a model
is asked to summarise, an email it is asked to read, or an image it is asked to look at can carry
instructions that the model acts on; the source's illustration is a web page that says the user
wants their private data retrieved and emailed to an attacker. It notes these systems are
non-deterministic, so the risk is probabilistic rather than certain, and argues that telling the
model not to comply is not a defence given the unbounded ways malicious instructions can be phrased.

The source treats [[DefinedTerm/model-context-protocol]] as the reason exposure has become easy to
acquire by accident: MCP encourages mixing and matching tools from different sources, many of which
reach private data, many of which reach places that may host malicious instructions, and almost any
of which can communicate outward — the source notes that a tool able to make an HTTP request at all,
even to load an image or offer a link for the user to click, can carry stolen information back. It
gives email as the sharpest case of an untrusted-content source, since an attacker can simply write
to the assistant. It cites a reported exploit against GitHub's official MCP server as an example of
one tool supplying all three legs at once: reading attacker-filed public issues, reaching private
repositories, and creating pull requests that carry the private data out.

## When It Applies

The framing applies to anyone assembling tools for an agent, and the source is directed at end users
as much as developers, on the grounds that vendors cannot help here. Reported exploits against
individual products have generally been fixed by the vendor closing the exfiltration path — the
source lists a long run of such cases against major assistant products between 2023 and 2025 — but
once a user combines tools themselves, no vendor is in a position to close anything.

The source is explicit that mitigation is unsolved. It says we still do not know how to prevent this
reliably, and is openly sceptical of vendor "guardrail" products that claim to detect a high
percentage of attacks, on the grounds that in web application security a 95% catch rate is a failing
grade. It points to research directions — design patterns that constrain an agent once it has
ingested untrusted input, and the CaMeL approach — while noting these help application developers
rather than end users mixing tools. For the end user, its stated remedy is avoidance: do not let the
three capabilities coexist.

That avoidance has a practical form, and [[BlogPosting/claude-code-for-web-async-coding-agent]]
describes it as the reason sandboxed network isolation matters. Its argument is that the best way to
prevent these attacks is to cut off one of the three legs, and that restricting which domains an
agent's process can reach removes the exfiltration leg specifically — an agent run with no network
access has nothing to worry about on this axis, whatever it reads. The same post notes the limit of
a partial cut: an environment that allows a long default list of dependency-installation domains
leaves the author uneasy about unintended exfiltration paths surviving inside the allow-list.

The source is also careful about the term's relationship to its parent concept. It notes that
"prompt injection" — which the same author coined, naming it after SQL injection — has drifted in
popular use toward meaning [[DefinedTerm/jailbreaking]], and argues that developers who conflate the
two dismiss the issue as a vendor-embarrassment problem rather than their own. See
[[DefinedTerm/semantic-diffusion]].

## Related Terms

[[DefinedTerm/prompt-injection]], [[DefinedTerm/indirect-prompt-injection]], [[DefinedTerm/jailbreaking]], [[DefinedTerm/model-context-protocol]], [[DefinedTerm/sandboxing]], [[DefinedTerm/guardrails]], [[BlogPosting/the-lethal-trifecta]]
