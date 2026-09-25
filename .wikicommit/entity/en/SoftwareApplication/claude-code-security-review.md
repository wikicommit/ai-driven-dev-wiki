---
title: "Claude Code Security Review"
type: "schema:SoftwareApplication"
lang: en
tags: [security, code-review, claude-code]
sources:
  - type: url
    url: 'https://www.anthropic.com/news/automate-security-reviews-with-claude-code'
    hash: sha256:98a0426960b7284026f86bb9083e584f1c6b55aec4f769321bbfe4b123035dd8
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Anthropic's automated security review for Claude Code, available as a /security-review command for ad-hoc analysis from the terminal and as a GitHub Action that reviews each new pull request and comments inline on vulnerabilities it finds."
  applicationCategory: "Automated security code review"
  featureList: "/security-review command in Claude Code; GitHub Action triggered on new pull requests; security-focused prompt covering SQL injection, XSS, authentication and authorization flaws, insecure data handling and dependency vulnerabilities; customizable rules to filter false positives and known issues; inline PR comments with recommended fixes"
  author: "[[Organization/anthropic]]"
---

Claude Code Security Review is [[Organization/anthropic]]'s automated security review for [[SoftwareApplication/claude-code]], announced in August 2025 in [[BlogPosting/automate-security-reviews-with-claude-code]]. The name is the one under which the announcement links the features' documentation; the post itself speaks of automated security reviews in two forms: a `/security-review` command that a developer runs in Claude Code from the terminal, and a GitHub Action that runs on pull requests. In both, Claude is asked to identify security concerns in code and can then be asked to fix them.

It addresses the concern that as developers rely on AI to ship faster and build more complex systems, code security becomes more critical. Anthropic positions it as a way to integrate [[DefinedTerm/security-code-review]] into existing workflows so that vulnerabilities are caught before they reach production.

## Capabilities

The `/security-review` command runs an ad-hoc analysis before code is committed: Claude searches the codebase for potential vulnerabilities and gives detailed explanations of what it finds. It uses a specialized security-focused prompt that checks for common vulnerability patterns, including SQL injection risks, cross-site scripting, authentication and authorization flaws, insecure data handling and dependency vulnerabilities. Claude Code can then be asked to implement a fix for each issue. The command is available by updating Claude Code to its latest version, and it can be customized.

The GitHub Action triggers automatically when a pull request is opened, reviews the changes for security vulnerabilities, applies customizable rules to filter out false positives and known issues, and posts inline comments on the pull request describing each concern with recommended fixes.

## Adoption & Ecosystem

Anthropic announced both features as available to all Claude Code users, and describes the action as integrating with an existing CI/CD pipeline and being customizable to a team's security policies. It reports using the action on its own code, including Claude Code itself, and gives two examples in which it caught a vulnerability before the pull request was merged or the code shipped: a remote code execution vulnerability exploitable through DNS rebinding in an internal tool that started a local HTTP server, and an SSRF vulnerability in a proxy built to manage internal credentials.
