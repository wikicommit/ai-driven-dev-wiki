---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/redesigning-source-control'
  hash: sha256:6eef9526169f77948a21587667cdda2583e166d062e81b5b2f46bdc53c2be1ed
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-10-16"
extracted_tokens: 7567
generated_pages:
  - .wikicommit/entity/en/BlogPosting/redesigning-source-control-at-anthropic.md
  - .wikicommit/entity/en/SoftwareApplication/scion.md
failed_pages: []
---


## Summary

Anthropic describes how a more than tenfold rise in merged code changes, driven by Claude writing most of its code, made git-based source control its biggest development bottleneck, and how a seven-person team built Scion — an in-house, server-centric version control system designed on the assumption that clients (mostly agents and CI jobs) are always online — and migrated its monorepo to it in five months. The post sets out Scion's design principles and architecture and the lessons the team drew, including that engineers' role shifted toward design judgment and telling Claude "no", and argues that some of these ideas could be applied to git servers without abandoning git's model.
