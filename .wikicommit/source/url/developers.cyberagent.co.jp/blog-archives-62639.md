---
source:
  type: url
  url: 'https://developers.cyberagent.co.jp/blog/archives/62639/'
  hash: sha256:8fe61a90b7d83235354ba7e66eb8068f7329ab03406aa10fc3725f34ee02cadc
  license:

schema:
status: generated
last_generated_at: "2026-09-21"
extracted_tokens: 6618
generated_pages:
  - .wikicommit/entity/en/BlogPosting/automating-coding-guidelines-with-ai.md
  - .wikicommit/entity/en/DefinedTerm/human-in-the-loop.md
failed_pages: []
---
## Summary

A CyberAgent frontend engineer describes a GitHub Actions workflow that periodically collects pull-request review comments, has an AI distill them into coding-guideline candidates, and opens a pull request where humans decide which to adopt. The workflow runs in two phases — extract, which builds the proposal pull request, and sync, which writes the accepted items back into the guideline document using metadata embedded in the pull request body — and is packaged as a reusable workflow. The author keeps a human in the loop deliberately, on the grounds that guidelines become team norms and that review comments often depend on context an AI cannot weigh.
