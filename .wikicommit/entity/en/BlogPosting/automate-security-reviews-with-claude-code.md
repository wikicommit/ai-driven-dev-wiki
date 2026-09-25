---
title: "Automate security reviews with Claude Code"
type: "schema:BlogPosting"
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
  description: "Anthropic's August 2025 product announcement of automated security reviews in Claude Code: a /security-review command for ad-hoc analysis from the terminal and a GitHub Action that reviews every new pull request for vulnerabilities."
  datePublished: "2025-08-06"
  publisher: "[[Organization/anthropic]]"
---

The post announces automated security reviews in [[SoftwareApplication/claude-code]], delivered as two features — a new `/security-review` command and a GitHub Action for pull requests — whose documentation the post links under the name `claude-code-security-review` (see [[SoftwareApplication/claude-code-security-review]]). Its argument is that as developers rely on AI to ship faster and build more complex systems, code security becomes more critical, and that building security review into existing workflows catches vulnerabilities before they reach production.

It places the two features at different points in development. The command keeps [[DefinedTerm/security-code-review]] "in your inner development loop," run from the terminal before committing; the action applies a consistent review to every pull request across a team. Both were announced as available to all Claude Code users.

## Key Points

- `/security-review` runs an ad-hoc security analysis from the terminal: Claude searches the codebase for potential vulnerabilities and explains any issues found.
- The command uses a specialized security-focused prompt that checks for common vulnerability patterns, including SQL injection risks, cross-site scripting, authentication and authorization flaws, insecure data handling and dependency vulnerabilities.
- After issues are identified, Claude Code can be asked to implement fixes for each of them.
- The GitHub Action triggers automatically on new pull requests, reviews the code changes for security vulnerabilities, applies customizable rules to filter out false positives and known issues, and posts inline comments on the pull request with its concerns and recommended fixes.
- The action is described as integrating with an existing CI/CD pipeline and being customizable to a team's security policies, so that no code reaches production without a baseline security review.
- Anthropic reports using the action on its own code, including Claude Code itself. Its two examples: the action identified a remote code execution vulnerability exploitable through DNS rebinding in an internal tool that started a local HTTP server, and flagged that a proxy built to manage internal credentials was vulnerable to SSRF attacks; both were fixed before shipping.
- The command is used by updating Claude Code and running `/security-review` in a project directory, and can be customized; the action has its own installation and configuration documentation.

## Context

This is a vendor's announcement of its own features, and the evidence it offers for their effectiveness is two examples from Anthropic's internal use rather than a measurement. The post does not claim the reviews replace other security practices; it frames them as a baseline check at two points in the workflow.
