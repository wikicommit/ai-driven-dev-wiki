---
source:
  type: url
  url: 'https://docs.claude.com/en/docs/claude-code/sandboxing'
  hash: sha256:57360cd4178c36fd6c21f3d4b7e9a52359e555419c6b9e09d2ba3b7a7f244a3c
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 19956
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/sandboxing.md
failed_pages: []
---

## Summary
Anthropic's documentation for Claude Code's sandboxed Bash tool, in which the operating system enforces user-defined filesystem and network boundaries on shell commands and their child processes so that most commands can run without per-command approval. It covers setup on macOS, Linux and WSL2, the auto-allow and regular permission modes, the unsandboxed retry escape hatch, filesystem and credential protection including credential masking, network isolation through a proxy, organization-wide enforcement, troubleshooting, and the sandbox's security limitations.
