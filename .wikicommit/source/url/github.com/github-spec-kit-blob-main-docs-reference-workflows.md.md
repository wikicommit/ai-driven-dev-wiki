---
source:
  type: url
  url: 'https://github.com/github/spec-kit/blob/main/docs/reference/workflows.md'
  hash: sha256:9edc007a729f332382682e209b40662bb963919d8d88fe0d101594ce7adad161

schema:
status: generated
last_generated_at: "2026-08-19"
extracted_tokens: 7923
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/spec-kit.md
failed_pages: []
---

## Summary

Spec Kit's reference documentation for workflows: YAML-defined, resumable sequences that chain commands, agent prompts, shell steps and human approval gates into repeatable multi-step spec-driven development processes. It documents the eleven step types, the CLI surface for running and managing workflows, the overlay mechanism for customising an installed workflow without editing it, catalog resolution order, and the built-in "Full SDD Cycle" workflow. It is unusually explicit about what the engine does not guarantee — there is no sandbox around a shell step and expression interpolation is plain string substitution — which was recorded on the Spec Kit page as a stated security posture.
