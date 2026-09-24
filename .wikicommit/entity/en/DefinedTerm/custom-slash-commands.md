---
title: "Custom slash commands"
type: "schema:DefinedTerm"
lang: en
tags: [agent-config, spec-driven-development, prompt-engineering]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60229/'
    hash: sha256:10d03ac2a5d00b558656acc685e174052e16d06256b8fd88f86df9be1d954d01
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A feature of AI agent tools that saves frequently used prompts as commands and persists and shares them per project, presented in spec-driven development as a way to turn instructions to AI into shared assets."
---

Custom slash commands are a feature of AI agent tools for saving frequently used prompts as named commands and persisting and sharing them at the level of a project. In the context of [[DefinedTerm/spec-driven-development]], [[BlogPosting/spec-driven-development-context-engineering-custom-slash-commands]] describes them as a mechanism for turning instructions to AI into assets and turning the development process itself into a set of functions.

## Usage

That post gives three reasons for using them in spec-driven development. They standardize prompt engineering, so that a command encoding a team's best practice produces the same format and quality whoever runs it, instead of output quality depending on each developer's prompting skill. They automate context injection, because a command can name the specification files to read, so the right specification reaches the agent's context without being selected and pasted by hand each time. And they put prompts under version control as code in the repository ("Prompt as Code"), where a team can review them and improve them over time.

The same post treats the design of commands as the main lever of [[DefinedTerm/context-engineering]] and proposes practices for it: give each command a single responsibility and a single output file, load only the minimum context, define the output's structure and a template before writing the command, test commands against a human-written golden output, keep command logic outside tool-specific directories, and treat long or branching instructions as a sign that a command should be split. These are one tech lead's findings from a proof of concept rather than a general convention.

## Related Terms

- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/context-confusion]]
- [[DefinedTerm/context-poisoning]]
