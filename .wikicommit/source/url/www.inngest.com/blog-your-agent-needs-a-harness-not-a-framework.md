---
source:
  type: url
  url: 'https://www.inngest.com/blog/your-agent-needs-a-harness-not-a-framework'
  hash: sha256:7123c66145498ab1e1f577792f9a542f2ac18ddf3ab8acc8c2c0c4af7748b4e4
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 5439
generated_pages:
  - .wikicommit/entity/en/BlogPosting/your-agent-needs-a-harness-not-a-framework.md
  - .wikicommit/entity/en/SoftwareApplication/utah.md
failed_pages: []
---

## Summary

An Inngest blog post by Dan Farrelly (3 March 2026) arguing that an agent runtime needs a harness — the layer that connects, protects and orchestrates the LLM, its tools and its memory without doing the work itself — and that durable, event-driven infrastructure already provides one. It presents Utah (Universally Triggered Agent Harness), a reference implementation in which every LLM call and tool call is an independently retryable Inngest step, the agent is split into six event-connected functions, sub-agents run via step.invoke(), one run per conversation is enforced with singleton concurrency, and context is kept in check with two-tier pruning, compaction and overflow recovery; it names steering and streaming as open problems.

## Generation Notes

- "Utah": the source states the reference implementation's code repository URL, but SoftwareApplication.md's properties block has no field for it, so it is recorded only in the body.
- "Dan Farrelly": exclude_reason privacy — the post's author, a living individual; entity-policy.md rules out pages about living individuals.
