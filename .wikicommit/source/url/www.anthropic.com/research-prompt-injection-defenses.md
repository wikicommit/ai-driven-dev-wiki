---
source:
  type: url
  url: 'https://www.anthropic.com/research/prompt-injection-defenses'
  hash: sha256:a0696c23a0c6a65b1581eb7fa746dbecd592b1177f016f52481cf3d09d18ab4f
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 3120
generated_pages:
  - .wikicommit/entity/en/BlogPosting/mitigating-prompt-injections-in-browser-use.md
  - .wikicommit/entity/en/DefinedTerm/indirect-prompt-injection.md
failed_pages: []
---

## Summary

Anthropic's account of prompt injection risk in browser use and the defences built against it. It argues browser agents amplify the risk two ways — a vast attack surface across every page, document, advertisement and dynamically loaded script, and a wide action space of navigating, form-filling, clicking and downloading — and describes three layers of response: reinforcement learning against injections embedded in simulated web content, classifiers scanning all untrusted content entering the context window for hidden text, manipulated images and deceptive UI elements, and continuous internal plus external red teaming. It reports a 1% attack success rate against an internal adaptive Best-of-N attacker given 100 attempts per environment, and states plainly that this still represents meaningful risk and that no browser agent is immune.
