---
source:
  type: url
  url: 'https://tech.qimao.com/ai-dai-ma-ping-shen-zai-qi-mao-de-shi-jian/'
  hash: sha256:b3c89326b7176bb078a329222696a60fa6aeb732270c6818b325db21588ef5c1
  license:
  lang: zh

schema:
status: generated
last_generated_at: "2026-09-30"
extracted_tokens: 1718
generated_pages:
  - .wikicommit/entity/en/BlogPosting/ai-code-review-practice-at-qimao.md
  - .wikicommit/entity/en/SoftwareApplication/eino.md
failed_pages: []
---

## Summary

Qimao's technology team describes building an AI code review service that automatically reviews merge requests on the Yunxiao platform and posts inline comments without any per-repository setup. The service is written in Go on ByteDance's Eino framework as a chain of data fetching, file grouping, a first-pass review and a second-pass scoring step, and the post reports lessons on input design (line-number drift in LLM output, less context giving better answers) and on choosing among Qwen models by quality, latency and cost.

## Generation Notes

- "李天鸣": exclude_reason privacy — the engineer credited as the post's contributor is a private individual named by the source, which entity-policy.md rules out.
- "郭子龙": exclude_reason privacy — an operations colleague thanked in passing is a private individual, which entity-policy.md rules out.
