---
source:
  type: url
  url: 'https://techblog.zozo.com/entry/verify-ai-agent-coding-rules-with-archunit'
  hash: sha256:24dfa5099ece90e3a7f95765c99bee45ad8dc9ddd142924e79cb91050675908c
  license:

schema:
status: partial
last_generated_at: "2026-09-22"
extracted_tokens: 11380
generated_pages:
  - .wikicommit/entity/en/BlogPosting/verify-ai-agent-coding-rules-with-archunit.md
  - .wikicommit/entity/en/DefinedTerm/ai-ide-rules.md
failed_pages: []
---


## Summary

A ZOZO team describes moving the coding rules it gives to AI agents from natural-language documents checked by reviewers to ArchUnit tests enforced as a required CI gate. Two premises drive the shift: that the reader of these rules is the agent rather than a person, so each rule should be self-contained rather than cross-referenced across files, and that a rule which cannot be mechanically checked is only as reliable as whichever review happens to catch a violation — with each rule document additionally stating which of its own constraints are already machine-checked and which still depend on the eye. The post also reports what did not work: a plan to distribute shared rules across repositories was abandoned when almost no team took up another team's rules, which the authors attribute to there being fewer genuinely portable rules than expected and to the standing cost of keeping an imported rule consistent with its test and the code.

## Generation Notes

- "藤本" (schema:Person): excluded, `privacy` — the post's named author, a living individual, which `.wikicommit/entity-policy.md` rules out; named in the body text and as a plain-text `author` value instead.
- "ArchUnit" (schema:SoftwareApplication): excluded, `theme_mismatch` — a general-purpose Java architecture-testing library that predates and is independent of AI-driven development; it appears in this source as the mechanism the rules are compiled into rather than as a subject of the wiki's own field. Described in body text on the generated pages instead.
