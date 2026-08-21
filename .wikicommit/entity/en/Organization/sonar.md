---
title: "Sonar"
type: "schema:Organization"
lang: en
tags: [code-quality, verification, developer-survey]
sources:
  - type: url
    url: 'https://www.sonarsource.com/state-of-code-developer-survey-report.pdf'
    hash: sha256:3d43f704cf1e52ecf4045d4342479248b68f557da49a051f79fb79b036967a0d
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A code analysis vendor that publishes the State of Code report series, drawing on the more than 750 billion lines of code it states it analyzes each day."
  url: "https://sonar.com/"
---

Sonar is a code analysis vendor whose relevance to this wiki is as a publisher of research on how AI-generated code behaves in practice. It states that it analyzes over 750 billion lines of code each day, and presents that scale as the basis for the understanding of code its published research draws on.

## History

The sources ingested here do not cover Sonar's founding or corporate history.

## Activities & Products

The company publishes a report series it calls State of Code, launched to share its knowledge with developers and technology leaders more broadly. It describes the series as having previously covered code reliability, security, maintainability, and what it calls the specific coding personalities of leading LLMs — reports it characterises as focused on the code itself and the models creating it.

[[Report/state-of-code-developer-survey-2026]] is the entry that changes the vantage point to the developers doing the work. Its stated aim was to read what is changing on the ground as AI shifts the mechanics of coding — the efficiencies, the frustrations and the emerging workflows — and it was deliberately designed to build on findings in other leading developer surveys and answer questions its authors still had after reading them. Its central finding, that a [[DefinedTerm/verification-bottleneck]] has emerged in place of the expected productivity gains, is the company's own.

The report's concluding chapter positions the company's SonarQube product as the verification layer for AI-generated code, and reports that SonarQube users see stronger positive impacts on code quality, technical debt, rework costs, defects and vulnerabilities than non-users — a comparison drawn from within Sonar's own survey, about its own product.
