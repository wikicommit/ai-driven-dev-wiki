---
source:
  type: url
  url: 'https://github.com/All-Hands-AI/OpenHands'
  hash: ""
  license:

schema:
status: failed
last_generated_at:
extracted_tokens:
generated_pages: []
failed_pages: []
---

## Failure Reason

Text extraction failed: `add_source.py --fetch-url` (markitdown via requests) got `HTTPError: 403 Client Error: Forbidden` for https://github.com/All-Hands-AI/OpenHands. The 403 body came from this session's GitHub access gate ("GitHub access to this repository is not enabled for this session"), not from the source itself, so this is an execution-environment restriction rather than a property of the page; re-run `/wikicommit-generate https://github.com/All-Hands-AI/OpenHands` from an environment that can fetch github.com. No content was extracted, so Passes 2-4 were not run for this source.
