---
source:
  type: url
  url: 'https://mathspp.com/blog/write-a-coding-agent-from-first-principles-better-tools'
  hash: sha256:a1984116f7e1602a9a51a47561da2c3f8d48ea9ec9fd990feb94e38f995739c4
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-09-30"
extracted_tokens: 11827
generated_pages:
  - .wikicommit/entity/en/BlogPosting/write-a-coding-agent-from-first-principles-better-tools.md
failed_pages: []
---


## Summary

A tutorial on mathspp that extends a minimal Python coding agent by replacing its hand-written file-editing and shell tools with Anthropic's text editor tool and bash tool, whose schemas the Claude models are trained on. It walks through implementing the text editor's create, str_replace, view and insert commands, a persistent bash session with timeouts and output truncation, and guardrails such as restricting edits to the working directory, backing files up before edits and asking the user to approve each shell command.
