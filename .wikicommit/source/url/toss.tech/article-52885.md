---
source:
  type: url
  url: 'https://toss.tech/article/52885'
  hash: sha256:e856fa940d5aebd5b630258f50c137d6ab0362f88e157ef8793d464a0625b252
  license:

schema:
status: generated
last_generated_at: '2026-09-22'
extracted_tokens: 4633
generated_pages:
  - .wikicommit/entity/en/BlogPosting/from-ai-generated-code-to-admin.md
  - .wikicommit/entity/en/SoftwareApplication/toi.md
failed_pages: []
---

## Summary

An engineering account of TOI, an internal Toss platform on which teams build admin tools by registering the APIs they need and describing the screens they want in natural language, with a model generating React against the registered request and response schemas. The post's subject is the environment that runs the generated code: a shared server-side dev server leaked one user's compile errors onto other users' screens, a third-party browser sandbox isolated users but took 47 seconds to show a first preview, and the team replaced both with an in-browser build over a layered virtual file system, with packages prebuilt per dependency combination and supplied through an import map, reaching 1.3 seconds. Its closing argument is that as generating code gets cheaper, the engineering work moves to guaranteeing the policies an admin tool must observe and designing a structure in which generated code can be run safely.

## Generation Notes

- "이현재": excluded, privacy -- the post's author, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. Not a relevance judgment. No page exists for this entity.
- "Sandpack": excluded, theme_mismatch -- CodeSandbox's browser sandbox, discussed here as a rejected approach. It is a general-purpose browser bundling and preview tool rather than AI-driven development tooling, so it falls outside this wiki's theme; it is named in the body of the pages built from this source instead. No page exists for this entity.
