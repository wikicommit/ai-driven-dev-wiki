---
source:
  type: url
  url: 'https://www.ncsc.gov.uk/blog-post/exercise-caution-building-off-llms'
  hash: sha256:b541d32182b2dc0647d41d9d904fb93653c6c331e794b22d8120713014c203dd
  license:

schema:
status: partial
last_generated_at: "2026-09-20"
extracted_tokens: 4184
generated_pages:
  - .wikicommit/entity/en/BlogPosting/exercise-caution-when-building-off-llms.md
failed_pages: []
---

## Summary

A 2023 NCSC blog post arguing that organisations building services on LLM APIs should treat the technology as still in beta: models can change behind the API a service is built on, a vendor may not survive, and the community does not yet fully understand LLMs' capabilities, weaknesses and vulnerabilities. It presents prompt injection as possibly an inherent issue with the technology -- research suggests an LLM cannot distinguish an instruction from the data supplied to help complete it -- and states that while some strategies make injection more difficult, there are as yet no surefire mitigations. Its central recommendation is architectural: design the system and its data flows so that the organisation is content with the worst case of whatever the LLM-powered application is permitted to do.

## Generation Notes

- "Dave Chismon": excluded, privacy -- the post's named author, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
