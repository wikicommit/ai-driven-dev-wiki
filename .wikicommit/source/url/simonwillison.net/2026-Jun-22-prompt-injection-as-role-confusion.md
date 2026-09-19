---
source:
  type: url
  url: 'https://simonwillison.net/2026/Jun/22/prompt-injection-as-role-confusion/'
  hash: sha256:40d3d22f5c2d4faf24481573bef5187e757c570cd5527e5d7f9c15f5b7595991
  license:

schema:
status: partial
last_generated_at: "2026-09-19"
extracted_tokens: 1002
generated_pages:
  - .wikicommit/entity/en/BlogPosting/prompt-injection-as-role-confusion.md
  - .wikicommit/entity/en/DefinedTerm/role-confusion.md
  - .wikicommit/entity/en/DefinedTerm/prompt-injection.md
failed_pages: []
---

## Summary

A link post reporting on research that frames prompt injection as "role confusion": the finding that models distinguish their own privileged text from untrusted user input largely by its *style* rather than by the role tags wrapping it. It relays the reported result that rewriting an injected passage so it reads less like the expected format — "destyling" — drops average attack success across the researchers' dataset from 61% to 10%, and the researchers' conclusion that injection defence will remain whack-a-mole until models achieve genuine role perception. The post also praises the practice of publishing a readable blog-style writeup alongside a formal paper.

## Generation Notes

- "Simon Willison": excluded, privacy — the post's author, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- "Charles Ye", "Jasmine Cui", "Dylan Hadfield-Menell": excluded, privacy — the researchers, named as authors of the work the post links to, all living individuals. No pages exist for these entities.
- The paper this post links to was not itself registered as a source, so no `ScholarlyArticle` page was created for it and its findings are recorded only as what this post reports.
