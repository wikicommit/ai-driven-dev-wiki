---
title: "Making frontier cybersecurity capabilities available to defenders"
type: "schema:BlogPosting"
lang: en
tags: [security, claude-code, vulnerability-detection]
sources:
  - type: url
    url: 'https://www.anthropic.com/news/claude-code-security'
    hash: sha256:5c3ca74f735e95124b17f304223a10b3e1f39dfe8d156aba651b1caeba7ab1b1
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "Anthropic's February 2026 announcement of Claude Code Security, a limited research preview in Claude Code on the web that scans codebases for vulnerabilities by reasoning about the code and suggests patches for human approval."
  datePublished: "2026-02-20"
  publisher: "[[Organization/anthropic]]"
---

The post announces [[SoftwareApplication/claude-code-security]], a new capability built into [[SoftwareApplication/claude-code-for-web]] and released as a limited research preview. Its framing is a problem security teams share — too many software vulnerabilities and too few people to address them — and a claim that existing analysis tools help only up to a point, because they usually look for known patterns, while the subtle, context-dependent vulnerabilities attackers often exploit need skilled human researchers whose backlogs keep growing.

[[Organization/anthropic]] presents AI as changing that calculation in both directions: the capabilities that help defenders find and fix vulnerabilities could also help attackers exploit them. The stated purpose of the release is to put those capabilities in defenders' hands and protect code against this new category of AI-enabled attack, and the limited preview is described as a way to refine the capability together with early users and ensure it is deployed responsibly.

## Key Points

- Rule-based static analysis matches code against known vulnerability patterns and catches common issues such as exposed passwords or outdated encryption, but, according to the post, often misses complex vulnerabilities such as business-logic flaws or broken access control.
- Claude Code Security instead reads and reasons about code the way the post says a human security researcher would: understanding how components interact and tracing how data moves through an application.
- Each finding goes through a multi-stage verification in which Claude re-examines the result and tries to prove or disprove it to filter out false positives; findings carry a severity rating and a confidence rating.
- Validated findings appear in a Claude Code Security dashboard where teams review them, inspect suggested patches and approve fixes; nothing is applied without human approval.
- The preview opened to Enterprise and Team customers, with free, expedited access for open-source maintainers who apply.
- Anthropic reports that the product builds on more than a year of its Frontier Red Team's research into Claude's cybersecurity capabilities, and that with Claude Opus 4.6 its team found over 500 vulnerabilities in production open-source codebases that had gone undetected for decades; these are Anthropic's own figures, with triage and responsible disclosure described as still under way.
- Anthropic says it also uses Claude to review its own code and has found it extremely effective at securing its systems.
- The post predicts that a significant share of the world's code will be scanned by AI in the near future, and argues that defenders who move quickly can find and patch the same weaknesses attackers will use AI to find.

## Context

This is a vendor's announcement of its own product, and its claims about effectiveness are the vendor's own. For the broader practice the product automates, see [[DefinedTerm/security-code-review]].
