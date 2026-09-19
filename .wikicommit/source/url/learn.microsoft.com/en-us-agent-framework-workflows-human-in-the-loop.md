---
source:
  type: url
  url: 'https://learn.microsoft.com/en-us/agent-framework/workflows/human-in-the-loop'
  hash: sha256:c8d4c0ec859c61f78664fbc60f846dfd583f0efa4b93d0d0c42cffa2dcdce9f8
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 3802
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/microsoft-agent-framework.md
failed_pages: []
---

## Summary

Microsoft's documentation page for human-in-the-loop interactions in the Agent Framework's workflow system. It presents HITL as a case of a more general request-and-response mechanism: an executor sends a request out of the workflow through a typed request port, the workflow pauses and emits an event carrying the request, an external system responds, and the framework routes the response back to the executor that asked. It shows the mechanism in C#, Python and Go, explains that tool approval under the prebuilt agent orchestrations reuses the same event with an approval payload, notes that sequential, concurrent and group-chat orchestrations do not pause for free-form user input while the handoff orchestration is interactive by default, and describes how pending requests are preserved in checkpoints and re-emitted on restore.
