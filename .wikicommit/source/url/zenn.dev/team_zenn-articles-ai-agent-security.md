---
source:
  type: url
  url: 'https://zenn.dev/team_zenn/articles/ai-agent-security'
  hash: sha256:2be721cd73612dfe7c91c26ac50fcee96d54da09dcbaa9bd625325d049417502
  license:

schema:
status: partial
last_generated_at: "2026-09-22"
extracted_tokens: 4681
generated_pages:
  - .wikicommit/entity/en/BlogPosting/ai-coding-agent-speed-and-safety-2026.md
  - .wikicommit/entity/en/DefinedTerm/sandboxing.md
  - .wikicommit/entity/en/DefinedTerm/permission-modes.md
  - .wikicommit/entity/en/DefinedTerm/approval-fatigue.md
failed_pages: []
---

## Summary

Based on a January 2026 conference talk, this post surveys the security risks of working with AI coding agents — credential exposure, vulnerable or malicious dependencies, prompt injection, and insecure generated code — and argues from a combinatorial estimate that exhaustive output checking by model vendors is not technically possible, so verification falls to the user. It then sets out guardrails against each risk: keeping secrets out of plaintext local storage, cooldown settings and scanners for dependencies, curating `permissions.allow`/`deny` so that automatic approval can be used without habituating reviewers, and three sandboxing options — Dev Containers, Claude Code's built-in sandbox, and cloud IDEs — compared on effort, stability, IDE choice and external-tool integration. The author concludes that no guardrail set removes the need for human supervision, and that review intensity should be scaled to how mission-critical the code is.

## Generation Notes

- "dyoshikawa": excluded (privacy) — the post's bylined author, a named living individual; entity-policy.md rules out a page about a living individual, and the switch is on. No existing page.
