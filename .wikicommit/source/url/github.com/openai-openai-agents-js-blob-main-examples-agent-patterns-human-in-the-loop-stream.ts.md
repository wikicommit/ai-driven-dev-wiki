---
source:
  type: url
  url: 'https://github.com/openai/openai-agents-js/blob/main/examples/agent-patterns/human-in-the-loop-stream.ts'
  hash: sha256:b539be2209796c131f666763bb7f0bc31443222962ec94c0ae76eb1d5d80a43e
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 2977
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/openai-agents-sdk.md
failed_pages: []
---

## Summary

A worked TypeScript example from the `openai-agents-js` repository showing how the OpenAI Agents SDK implements human-in-the-loop tool approval inside a streaming run. A `needsApproval` predicate is attached both to an ordinary tool and to an agent exposed as a tool, and is evaluated against the arguments the model generated, so approval is required per call rather than per tool. When it fires the run completes with a list of interruptions naming the agent, tool and arguments; the host approves or rejects each on the run state and restarts the agent with that same state, repeating until no interruptions remain.
