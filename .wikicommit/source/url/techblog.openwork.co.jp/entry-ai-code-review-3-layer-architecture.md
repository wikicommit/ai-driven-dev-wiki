---
source:
  type: url
  url: 'https://techblog.openwork.co.jp/entry/ai-code-review-3-layer-architecture'
  hash: sha256:b4d6c939c7b4971dd50b6e2277243cbceb4d415eaf799742f1d75acf18a48570
  license:

schema:
status: generated
last_generated_at: "2026-09-22"
extracted_tokens: 7042
generated_pages:
  - .wikicommit/entity/en/BlogPosting/three-layer-agent-orchestration-ai-code-review.md
  - .wikicommit/entity/en/DefinedTerm/three-layer-agent-orchestration.md
failed_pages: []
---

## Summary

An OpenWork engineer describes a three-layer agent orchestration built on GitHub Copilot CLI custom agents to raise AI code-review precision. A parent agent decides which technical domains a branch touches and fans out per-perspective review agents; each perspective is reviewed by four agents split across two model families, and only findings two or more agents raise independently are kept, which is the post's stated defence against hallucinated and trivial comments. Results post as PR inline comments, and a context-collection agent feeds prior review threads back in so engineers' "won't fix" replies are not re-raised.

## Generation Notes

- "Yamamoto (k_yamamoto_ow)": excluded (privacy) -- the post's author, named as a web application engineer at the company; entity-policy.md rules out a page about a real individual who is not a public figure. No existing page.
- "OpenWork": not extracted -- appears as the publishing employer, with no independent facts about the organization itself stated; Organization.md's granularity treats that as an incidental mention.
