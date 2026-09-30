---
title: "Claude Code Security"
type: "schema:SoftwareApplication"
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
  description: "A capability built into Claude Code on the web that scans codebases for security vulnerabilities by reasoning about the code, verifies its own findings, and suggests targeted patches that are applied only with human approval; announced in February 2026 as a limited research preview."
  applicationCategory: "AI vulnerability scanning and patch suggestion"
  featureList: "Codebase scanning by reasoning about component interactions and data flow; multi-stage self-verification of findings to filter false positives; severity and confidence ratings per finding; dashboard for reviewing findings and suggested patches; fixes applied only after human approval"
  author: "[[Organization/anthropic]]"
---

Claude Code Security is a capability from [[Organization/anthropic]], built into [[SoftwareApplication/claude-code-for-web]], that scans codebases for security vulnerabilities and suggests targeted software patches for human review. It was announced on 20 February 2026 in [[BlogPosting/making-frontier-cybersecurity-capabilities-available-to-defenders]] as a limited research preview.

Anthropic positions it against rule-based static analysis, which matches code against known vulnerability patterns: that catches common issues such as exposed passwords or outdated encryption but, on Anthropic's account, often misses complex vulnerabilities such as flaws in business logic or broken access control. The stated aim is to let security teams find and fix issues that traditional methods often miss, and to put AI's vulnerability-finding capabilities in the hands of defenders.

## Capabilities

Rather than scanning for known patterns, it is described as reading and reasoning about code the way a human security researcher would — understanding how components interact and tracing how data moves through an application.

Every finding goes through a multi-stage verification process before it reaches an analyst: Claude re-examines each result, attempting to prove or disprove its own finding and filter out false positives. Findings are assigned a severity rating so teams can prioritize, and a confidence rating, because such issues often involve nuances that are hard to assess from source code alone.

Validated findings appear in the Claude Code Security dashboard, where teams review them, inspect the suggested patches and approve fixes. Nothing is applied without human approval: the tool identifies problems and suggests solutions, and developers make the decision. Because it is built on [[SoftwareApplication/claude-code]], teams can review findings and iterate on fixes within tools they already use.

## Adoption & Ecosystem

At announcement the research preview was opened to Enterprise and Team customers, who get early access and work directly with Anthropic to refine the tool, and open-source maintainers were invited to apply for free, expedited access. Anthropic says it builds on more than a year of research by its Frontier Red Team into Claude's cybersecurity capabilities, and that Anthropic also uses Claude to review its own code.
