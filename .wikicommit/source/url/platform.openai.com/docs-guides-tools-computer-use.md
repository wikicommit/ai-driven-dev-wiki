---
source:
  type: url
  url: 'https://platform.openai.com/docs/guides/tools-computer-use'
  hash: sha256:b981146b951cbe05f5084f9bf92ce301183dfed2c810a242adaab76293df9394
  license:

schema:
status: generated
last_generated_at: '2026-09-19'
extracted_tokens: 13463
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/computer-use.md
failed_pages: []
---

## Summary

OpenAI's API guide for the computer use capability, which lets a model operate browser and desktop interfaces on a user's behalf while the caller supplies and runs the environment. It documents two integration styles — code execution, in which the model writes a script driven by a library such as PyAutoGUI or Playwright and which OpenAI recommends for GPT-6 Astra, and the `computer` tool, in which the model returns structured mouse and keyboard actions — and closes with four safety controls: restrict the environment, treat screen content as untrusted, confirm consequential actions, and bound and verify the run.
