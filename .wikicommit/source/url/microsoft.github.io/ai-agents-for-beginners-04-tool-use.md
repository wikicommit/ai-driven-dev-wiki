---
source:
  type: url
  url: 'https://microsoft.github.io/ai-agents-for-beginners/04-tool-use/'
  hash: sha256:71a0416f774296d3c63b62963e0d749c00171e54c528c1541b44d90949d22ab2
  license:

schema:
status: generated
last_generated_at: "2026-09-18"
extracted_tokens: 4852
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/tool-use-design-pattern.md
  - .wikicommit/entity/en/SoftwareApplication/microsoft-agent-framework.md
  - .wikicommit/entity/en/SoftwareApplication/microsoft-foundry-agent-service.md
failed_pages: []
---

## Summary

Lesson 4 of Microsoft's open-source "AI Agents for Beginners" course, covering the Tool Use Design Pattern: supplying a model with schemas for callable functions so that it can select one, return a structured call, and have the result fed back into its reasoning. It names six implementation building blocks, walks through function calling end to end with a worked example, and then demonstrates the pattern through the Microsoft Agent Framework and the Microsoft Foundry Agent Service. It also notes that the risk from model-generated SQL is addressed by configuring read-only database permissions rather than by trusting the model.
