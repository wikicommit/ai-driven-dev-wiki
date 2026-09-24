---
source:
  type: url
  url: 'https://developers.cyberagent.co.jp/blog/archives/62404/'
  hash: sha256:d49efd9233d456d1b205c748e19560ccabe3dc107352ab0e2e2f6f98094dd5ca
  license:

schema:
status: partial
last_generated_at: "2026-09-24"
extracted_tokens: 8630
generated_pages:
  - .wikicommit/entity/en/BlogPosting/sdd-in-unity-client-antipatterns-and-improvements.md
  - .wikicommit/entity/en/DefinedTerm/context-bloat-loop.md
  - .wikicommit/entity/en/DefinedTerm/deterministic-quality-gate.md
  - .wikicommit/entity/en/DefinedTerm/multi-model-orchestration.md
failed_pages: []
---

## Summary

A CyberAgent Developers Blog post by a Unity engineer at GOODROID comparing two attempts to move the development of internal Unity client infrastructure to spec-driven development with AI agents, so that humans wrote no code. In the first, a single giant spec that took about 73% of the context window led to frequent compaction, skipped workflow steps, and a loop in which fixing the flow with more rules made it worse. The second split the work into 21 specs, minimized always-loaded context, orchestrated Claude Code with Codex across providers, enforced tests through deterministic gates in hooks and GitHub Actions, and ran agents without permission prompts in an isolated Docker environment, after which the volume of pull requests became the new bottleneck.

## Generation Notes

- "Shinji Oikawa": exclude_reason privacy — the post's author, a living individual; entity-policy.md rules out pages about living individuals.
