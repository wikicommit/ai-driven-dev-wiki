---
source:
  type: url
  url: 'https://tech.kakao.com/posts/696'
  hash: sha256:f0f6b624af35db20919086a553302d61aaee2924607847748e7c6f8166ff51da
  license:

schema:
status: failed
last_generated_at:
extracted_tokens:
generated_pages: []
failed_pages: []
---

## Failure Reason

Text extraction returned a content shell, not the article: the fetch succeeded (2,073 bytes) but contained only the site header, the article title and author byline, previous/next links, the sitemap footer and the search widget -- no article body. tech.kakao.com appears to render post bodies client-side. Guard A passed it (natural-language character ratio 0.62) because the Korean navigation and footer chrome reads as prose, so the low-density heuristic could not distinguish this from a real page; operator confirmed it as an extraction failure. Passes 2-4 were not run for this source.
