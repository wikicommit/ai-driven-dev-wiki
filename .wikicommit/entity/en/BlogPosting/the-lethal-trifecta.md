---
title: "The lethal trifecta for AI agents: private data, untrusted content, and external communication"
type: "schema:BlogPosting"
lang: en
tags: [agent-security, prompt-injection, exfiltration, tool-use]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/'
    hash: sha256:0af6dbc8f6a6fb02d0257c9c4aa852d009e4afdd442ba84dd828c21a84d987dd
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The post that named the lethal trifecta, arguing that the danger in tool-using LLM systems lies in one particular combination of three capabilities rather than in any single one, and that end users mixing their own tools cannot rely on vendors to protect them."
  author: ["Simon Willison"]
  datePublished: "2025-06-16"
---

This post names a pattern rather than reporting a new vulnerability. Its contribution is to isolate
the specific combination under which prompt injection becomes data theft — private data access,
untrusted content exposure, and outward communication held by the same system — and to give it a
label short enough to use as a checklist. The term it introduces is developed as its own subject under
[[DefinedTerm/lethal-trifecta]].

The post is addressed to users as much as to developers, and that choice carries its argument. It
observes that almost all of the reported exfiltration attacks against major assistant products were
promptly fixed by the vendors, usually by locking down the exfiltration vector, then points out that
this remedy
stops being available the moment a user assembles tools themselves. Its conclusion is correspondingly
blunt: the vendors are not going to save us, and avoiding the combination is the only reliable move
available to an end user.

## Key Points

- The three capabilities are individually ordinary and useful; the risk is a property of holding all three at once, which is why the post treats the combination rather than any single capability as the thing to name.
- LLMs follow instructions found in content and cannot reliably weight instructions by origin, because everything is concatenated into one token sequence — so summarising a page, reading an email, or looking at an image is a potential injection vector.
- Because these systems are non-deterministic, the post frames the risk as a "very good chance" rather than a certainty; it lists instructing the model not to comply among the ways to reduce the likelihood, then asks how confident anyone can be that such a protection works every time, given the unbounded space of possible phrasings.
- [[DefinedTerm/model-context-protocol]] makes the combination easy to assemble by accident, since it encourages mixing tools from different sources; the post argues almost any tool that can make an HTTP request — even to load an image or render a clickable link — can serve as the exfiltration leg.
- Email is called a perfect source of untrusted content, because an attacker can address the assistant directly; the post gives a sample message asking the assistant to forward password reset emails.
- The reported GitHub MCP exploit is cited as a case where a single tool supplied all three legs: reading attacker-filed public issues, reaching private repositories, and creating pull requests that carried the data out.
- The post is explicitly sceptical of commercial guardrail products, arguing that a claimed 95% detection rate is a failing grade by web application security standards.
- It points to approaches it has recently written up that application developers can take to mitigate this class of attack, and concludes that none of them help end users who are mixing and matching tools, whose only safe move is to avoid the combination.
- The post argues the term [[DefinedTerm/prompt-injection]] has drifted toward meaning [[DefinedTerm/jailbreaking]], and that developers who conflate the two wrongly treat the issue as a vendor's embarrassment rather than their own problem.

## Notes

The author states that he coined the term "prompt injection" some years earlier, naming it after SQL
injection for the shared underlying problem of mixing trusted and untrusted content in one context,
and that he considers jailbreaking a separate issue. The post also says he has collected dozens of
examples of this class of attack under an exfiltration-attacks tag on his blog.
