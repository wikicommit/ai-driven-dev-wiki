---
title: "Dark Factory"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, ai-assisted-programming, spec-driven-development]
sources:
  - type: url
    url: 'https://sddbook.blob.core.windows.net/downloads/spec-driven-development.pdf'
    hash: sha256:7f897827f00db69ac4a15f3acea3826e5504b1600d0b785cdce210d5414f1eea
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Level 5 of Dan Shapiro's Five Levels of Vibe Coding: a black box that turns specifications into software, named after the Fanuc robot factory and dark because humans are neither needed nor welcome. Kevin Ryan reports that a handful of people on the planet operate there."
---

A Dark Factory is a software operation that functions as a black box turning specifications into software, with humans neither writing nor reviewing code. It is Level 5 — the top level — of [[Person/dan-shapiro]]'s [[DefinedTerm/five-levels-of-vibe-coding]], named after the Fanuc robot factory: dark because humans are neither needed nor welcome. [[Person/kevin-ryan]] reports that a handful of people on the planet operate at this level.

## Usage

[[Organization/strongdm]] is the worked example Ryan gives. Its Dark Factory has been running since July 2024 with three engineers: no standups, no sprints, no Jira, no humans writing code and no humans reviewing code. Agents build the software, test it and ship it; the engineers specify what needs to exist and evaluate whether the output meets the specification. Ryan reports the operation's AI compute bill at a thousand dollars per engineer per day, which the company considered a bargain.

Ryan argues the transferable content is not the automation itself but the two architectural innovations that make autonomous execution safe — [[DefinedTerm/external-scenarios]], which put the success criteria outside the codebase where the agent cannot game them, and [[DefinedTerm/digital-twin]] environments, which let agents develop against behavioural clones of external services rather than production APIs.

He is also direct that the Dark Factory is not the target for most readers. Level 5, he writes, requires infrastructure, investment and architectural commitment that most organisations cannot and should not attempt today; the practical goal is Level 3 or 4, "where the leverage is real and the path is practical." His argument for paying attention to it anyway is that the companies operating there are the bellwether of a disruption that reshapes the economics of the entire industry.

## Related Terms

The Dark Factory sits at the far end of [[DefinedTerm/five-levels-of-vibe-coding]] and is the operational endpoint of [[DefinedTerm/spec-driven-development]] — the point at which the specification is the only artifact humans work on. The techniques that make it viable are covered under [[DefinedTerm/external-scenarios]] and [[DefinedTerm/digital-twin]].
