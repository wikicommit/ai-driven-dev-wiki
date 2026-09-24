---
title: "ast-grep"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, coding-tools]
sources:
  - type: url
    url: 'https://aise.phodal.com/aise-code-review.html'
    hash: sha256:c66c9a026df66e7f4feae11ee51fd39f0d6479793176e5269c0d01403e7f9453
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An AST-based tool for matching code patterns at scale, written in Rust on tree-sitter parsers, that uses a simple regular-expression-like query language; CodeRabbit uses it for AST-pattern-based review instructions."
  applicationCategory: "AST-based code pattern matching and linting tool"
---

ast-grep is presented in Phodal's chapter on AI-assisted code review, next to a link to its rule-configuration documentation, as "a new AST based tool for managing your code, at massive scale". It is written in Rust and uses tree-sitter parsers to generate abstract syntax trees for many popular programming languages, and it lets developers match code patterns using a simple query language modelled on regular expressions.

## Capabilities

Its rule configuration combines three kinds of condition. Atomic rules match on a pattern, a tree-sitter node kind or a regular expression; relational rules constrain a match by its position relative to other code (inside, has, follows, precedes); and composite rules combine others with all, any and not. The example also shows a matches key.

Beyond enforcing coding standards, the chapter describes ast-grep as able to surface the intent of code — detecting network calls, error-handling patterns, resource management and concurrency patterns.

## Adoption & Ecosystem

[[SoftwareApplication/coderabbit]] uses ast-grep under the hood to support review instructions based on AST patterns — the chapter's example configuration enables essential security rules and names custom rule directories and rule packages. The chapter, summarising a CodeRabbit article, presents the combination as an AI-native universal linter: patterns and context extracted by ast-grep are passed to an LLM to produce more accurate fix suggestions, while the deterministic matching reduces the noise and variability that generative AI alone produces.
