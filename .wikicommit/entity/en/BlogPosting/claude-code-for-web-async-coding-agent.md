---
title: "Claude Code for web—a new asynchronous coding agent from Anthropic"
type: "schema:BlogPosting"
lang: en
tags: [agents, anthropic, coding-tools, sandboxing, agent-security]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Oct/20/claude-code-for-web/'
    hash: sha256:45fb7060c3561e36111229e2a76520baefc9e1538596494a73f3ba55f27fb826
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A hands-on account of Anthropic's hosted Claude Code, arguing that its real significance is the sandboxing strategy it was announced inside — which the author calls the only approach to agent safety that feels credible to him."
  author: ["Simon Willison"]
  datePublished: "2025-10-20"
---

The post reviews [[SoftwareApplication/claude-code-for-web]] from a weekend of preview access, but
its argument is not really about the product. The author's assessment of the tool itself is
deflationary: it produces pull requests he calls indistinguishable from the local CLI's, the same
prompts would likely produce the same results on a laptop, and the value is convenience rather than
capability.

What the post treats as significant is how the launch was framed. It notes that the product
announcement was buried halfway down an Anthropic engineering post about sandboxing, and reads that
placement as the real news — evidence that Anthropic is treating filesystem and network isolation,
rather than per-action approval, as the way to make capable agents safe to run.

## Key Points

- The author's reading, offered as a guess rather than a documented fact, is that the hosted product is the Claude Code CLI wrapped in a container and configured to skip permission prompts; he reports it appears to behave exactly like the local tool.
- It is positioned as Anthropic's counterpart to OpenAI's Codex Cloud and Google's Jules, with a very similar shape.
- The author's own examples span a task he calls very simple (a query-string-stripper tool), a README correction, and a four-scenario Python templating benchmark with charts — the last prompted from a phone.
- Filesystem sandboxing is characterised as relatively easy and network isolation as the harder problem; the post quotes Anthropic's description of routing internet access through a unix domain socket to an out-of-sandbox proxy that enforces domain restrictions and handles confirmation for newly requested domains.
- Network isolation is presented as crucial against both [[DefinedTerm/prompt-injection]] and [[DefinedTerm/lethal-trifecta]] attacks, on the reasoning that the best defence is cutting off one of the three legs and isolation removes the exfiltration leg.
- The author is uneasy about the middle setting: a "Trusted network access" environment whose default allow-list runs to dozens of entries, which he suspects may leave unintended exfiltration paths open.
- The post frames sandboxing as an acknowledgement that agents run without step-by-step approval are far more valuable and productive than agents requiring it, making convenient safe execution the real problem to solve.
- The author states this kind of sandboxing is the only approach to agent safety that feels credible to him.

## Notes

The post reports that Anthropic released an open source (Apache 2) library carrying its sandboxing
implementation, and that the underlying mechanisms appear to be seatbelt on macOS and Bubblewrap on
Linux — the latter offered as the author's reading rather than as a documented claim, since he notes
he had not yet examined the details.

An update appended to the post declines to estimate what this kind of work costs, on the grounds
that the author was using a plan Anthropic had provided for testing, and reports only a rough daily
figure for his own local CLI usage measured with an unofficial tool.
