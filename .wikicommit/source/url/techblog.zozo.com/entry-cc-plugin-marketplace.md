---
source:
  type: url
  url: 'https://techblog.zozo.com/entry/cc-plugin-marketplace'
  hash: sha256:3ea931e475eb0d34cf89d80370d5fb142dc0684ce20d67ed208b882d87f015b1
  license:

schema:
status: generated
last_generated_at: "2026-09-22"
extracted_tokens: 12581
generated_pages:
  - .wikicommit/entity/en/BlogPosting/shared-claude-code-plugin-marketplace.md
  - .wikicommit/entity/en/DefinedTerm/claude-code-plugin-marketplace.md
  - .wikicommit/entity/en/Organization/zozo.md
failed_pages: []
---


## Summary

Two ZOZO engineers describe operating a single Claude Code plugin marketplace shared across several teams, and the five problems that shared operation produced: unclear grouping and unclear maintenance ownership, conflicts and missed registrations in the one shared `marketplace.json`, structural errors slipping past review and breaking the catalog for every team at once, skills that could not be found by search and were therefore reinvented, and fixes to existing plugins deferred because their blast radius was invisible. Each is met with a different mechanism — team-owned directories, `marketplace.json` regenerated in CI from each plugin's own `plugin.json`, static validation delegated almost entirely to `claude plugin validate`, a browsable skill index searched by intent phrases rather than by developer-written descriptions, and an on-demand `@claude` check for breaking changes and marketplace conventions. After roughly ten months of operation the authors report no major incident, and say improvements to existing plugins account for close to 60% of merged pull requests.

## Generation Notes

- "木村" (schema:Person): excluded, `privacy` — one of the post's two named authors, a living individual, which `.wikicommit/entity-policy.md` rules out; named in the body text instead.
- "上國料" (schema:Person): excluded, `privacy` — the post's other named author, a living individual, which `.wikicommit/entity-policy.md` rules out; named in the body text instead.
