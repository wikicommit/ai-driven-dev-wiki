---
title: "Equipping agents for the real world with Agent Skills"
type: "schema:TechArticle"
lang: en
tags: [agentic-coding, configuration, context-engineering, agent-skills]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills'
    hash: sha256:67f4d43862e0cdc95ff69a5da0f2ecb7b3ca20fb9db59e1962077b1c422289d1
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Anthropic's engineering post of 16 October 2025 introducing [[DefinedTerm/agent-skills]] — folders of instructions, scripts, and resources an agent discovers and loads dynamically. It sets out the SKILL.md anatomy, states [[DefinedTerm/progressive-disclosure]] as the design principle behind it, and adds authoring guidelines and a trusted-source security caveat."
  author:
    - "Barry Zhang"
    - "Keith Lazuka"
    - "Mahesh Murag"
  datePublished: "2025-10-16"
  publisher: "[[Organization/anthropic]]"
---

"Equipping agents for the real world with Agent Skills" is the [[Organization/anthropic]] engineering post that introduced [[DefinedTerm/agent-skills]], published 16 October 2025 and written by Barry Zhang, Keith Lazuka, and Mahesh Murag. It carries an update dated 18 December 2025 stating that Agent Skills has since been published as an open standard for cross-platform portability.

The post's stated motivation is a mismatch between capability and context: as models improve, general-purpose agents can interact with full-fledged computing environments — [[SoftwareApplication/claude-code]] is its example, accomplishing complex tasks through local code execution and filesystems — but "real work requires procedural knowledge and organizational context," and equipping agents with domain-specific expertise needs a more composable, scalable, and portable mechanism than building a custom agent per use case. Its analogy for authoring one is putting together an onboarding guide for a new hire.

The mechanism it defines is deliberately plain: a skill is a directory containing a `SKILL.md` file whose YAML frontmatter carries two required fields, `name` and `description`, alongside optional bundled instructions, scripts, and resources. The post closes on that simplicity as the point — "Skills are a simple concept with a correspondingly simple format," which it argues is what makes it easy for organizations, developers, and end users to build customized agents.

## Key Practices

- **Progressive disclosure in three levels.** The post names this "the core design principle that makes Agent Skills flexible and scalable," and its analogy is a well-organized manual with a table of contents, chapters, and a detailed appendix. The **first level** is the `name` and `description` metadata, which the agent pre-loads into its system prompt for every installed skill at startup — enough to know when a skill applies without loading it. The **second level** is the body of `SKILL.md`, read into context only if the agent judges the skill relevant. The **third level and beyond** are additional files bundled in the skill directory and referenced by name from `SKILL.md`, which the agent navigates and discovers only as needed. The post's stated consequence is that an agent with a filesystem and code execution tools never needs the whole skill in context, so "the amount of context that can be bundled into a skill is effectively unbounded."
- **A worked example that shows what the levels buy.** The post walks through the PDF skill behind Claude's document editing abilities: Claude already understands PDFs but is limited in manipulating them, such as filling out a form. That skill's `SKILL.md` references two further files, `reference.md` and `forms.md`; moving the form-filling instructions into `forms.md` keeps the core of the skill lean, on the author's trust that Claude will read it only when actually filling a form. The post traces the resulting context sequence: system prompt plus every skill's metadata plus the user message; Claude invoking Bash to read `pdf/SKILL.md`; Claude choosing to read `forms.md`; then proceeding with the task.
- **Code as a first-class part of a skill.** Skills can bundle code for the agent to execute at its discretion. The post's argument is both economic and about reliability: "sorting a list via token generation is far more expensive than simply running a sorting algorithm," and many applications need the deterministic reliability only code provides. In the PDF example a pre-written Python script extracts all form fields, and the post notes Claude can run it without loading either the script or the PDF into context.
- **Four authoring guidelines.** *Start with evaluation* — find specific capability gaps by running agents on representative tasks and observing where they struggle, then build skills incrementally against those gaps. *Structure for scale* — split an unwieldy `SKILL.md` into referenced files, keep mutually exclusive or rarely co-occurring paths separate to reduce token usage, and make it clear whether Claude should run a script or read it as reference, since code serves as both. *Think from Claude's perspective* — watch how Claude actually uses the skill, looking for unexpected trajectories or overreliance on certain contexts, with special attention to `name` and `description` because those decide whether the skill triggers at all. *Iterate with Claude* — ask Claude to capture its successful approaches and common mistakes into the skill as you work, and to self-reflect when it goes off track, which the post argues surfaces what Claude actually needs rather than what an author anticipated.

## Scope & Caveats

The post states a security position rather than a security mechanism. Because skills supply both instructions and code, it warns that malicious skills may introduce vulnerabilities in the environment where they are used, or direct Claude to exfiltrate data and take unintended actions. Its recommendation is to install skills only from trusted sources, and when a source is less trusted, to audit the skill thoroughly first — reading the bundled files, paying particular attention to code dependencies and bundled resources such as images or scripts, and watching for instructions or code that direct Claude to connect to potentially untrusted external network sources.

On availability, the post states Skills were supported at the time of writing across Claude.ai, Claude Code, the Claude Agent SDK, and the Claude Developer Platform. Its stated near-term plans were features covering the full lifecycle of creating, editing, discovering, sharing, and using Skills, and exploring how Skills can complement [[DefinedTerm/model-context-protocol]] servers by teaching agents more complex workflows involving external tools. Looking further ahead, it states a hope to let agents create, edit, and evaluate Skills on their own, codifying their own patterns of behavior into reusable capabilities.

This is the vendor's own introduction of its own mechanism; the guidelines are Anthropic's design intent rather than independent findings about how skills perform in practice.
