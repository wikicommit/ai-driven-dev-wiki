---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/claude-code-sandboxing'
  hash: sha256:fb32cb34826801c245ce18f24b54cbb117f8099475c3cf01237f9d74484d7abb
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 3540
generated_pages:
  - .wikicommit/entity/en/BlogPosting/beyond-permission-prompts.md
  - .wikicommit/entity/en/SoftwareApplication/sandbox-runtime.md
failed_pages: []
---

## Summary

An Anthropic engineering post (Oct 2025) introducing two sandboxing features for Claude Code — a sandboxed bash tool built on an open-source sandbox runtime, and Claude Code on the web — which enforce filesystem and network isolation so Claude can run with fewer permission prompts. It argues that effective sandboxing needs both boundaries, reports an 84% reduction in permission prompts in internal usage, and describes how Claude Code on the web keeps git credentials out of the sandbox via a proxy.

## Generation Notes

"David Dworken", "Oliver Weller-Davies": exclude_reason privacy — the post's authors, living individuals; entity-policy.md rules out pages about living individuals.
