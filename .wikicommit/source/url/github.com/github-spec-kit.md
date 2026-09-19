---
source:
  type: url
  url: 'https://github.com/github/spec-kit'
  hash: sha256:43e53abd453112137f25876eef80951cf1caabd0b9b88260dc5c527de383c731
  license:

schema:
status: generated
last_generated_at: '2026-09-19'
extracted_tokens: 5540
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/github-spec-kit.md
failed_pages: []
---

## Summary

The GitHub Spec Kit repository, presenting the toolkit as giving AI coding agents structured processes, reusable templates and documented outcomes. It offers three independent entry points rather than mandatory phases: spec-driven development (shipped in core, run as `/speckit-specify`, `-plan`, `-tasks`, `-implement` and `-converge`, with implement and converge repeated until convergence reports "Converged"), bug fixing, and idea assessment, the latter two installed as opt-in extensions. Setup is the `specify` CLI installed with uv; the processes themselves are agent skills invoked in the coding agent's chat rather than terminal commands.
