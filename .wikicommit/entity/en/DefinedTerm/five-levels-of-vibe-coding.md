---
title: "Five Levels of Vibe Coding"
type: "schema:DefinedTerm"
lang: en
tags: [vibe-coding, ai-assisted-programming, maturity-model]
sources:
  - type: url
    url: 'https://sddbook.blob.core.windows.net/downloads/spec-driven-development.pdf'
    hash: sha256:7f897827f00db69ac4a15f3acea3826e5504b1600d0b785cdce210d5414f1eea
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A maturity framework by Dan Shapiro grading AI-assisted development practice from Level 0 to Level 5, which Kevin Ryan records as published in January 2026 and modelled on the NHTSA's five levels of driving automation. Its stated diagnostic value lies less in the levels themselves than in the gap between where teams believe they are and where they actually are."
---

The Five Levels of Vibe Coding is a maturity framework by [[Person/dan-shapiro]] grading a developer's or team's AI-assisted practice on a scale from Level 0 to Level 5. [[Person/kevin-ryan]] records that Shapiro published it in January 2026, modelled on the NHTSA's five levels of driving automation. It describes not how capable the tools are but how much of the work the human still performs directly, and at which point in the loop the human's judgment is applied.

## Usage

| Level | Name | What it looks like |
| --- | --- | --- |
| 0 | Spicy Autocomplete | Not a character hits the disk without your approval. You might use AI as a search engine on steroids, but the code is unmistakably yours. |
| 1 | Coding Intern | You offload discrete tasks — "write a unit test for this," "add a docstring" — but your job is unchanged. You are still moving at the rate you type. |
| 2 | Autopilot on the Highway | You are pairing with the AI and get into a flow state, more productive than you have ever been. Shapiro estimates 90% of self-described "AI-native" developers are here. |
| 3 | The Manager | You are the human in the loop. Your coding agent is always running and you spend your days reviewing code. "Your life is diffs." Almost everyone tops out here. |
| 4 | The PM | You write a spec, argue with the AI about the spec, plan schedules and review plans — then leave for twelve hours and check whether the tests pass. Shapiro puts himself here. |
| 5 | The [[DefinedTerm/dark-factory]] | A black box that turns specs into software. A handful of people on the planet operate here. |

[[Person/kevin-ryan]], who calls the framework more diagnostically useful than anything else in the discourse, argues its value is not in the levels themselves but in the gap between where teams believe they are and where they actually are. He reports that in every engagement he ran in the year before writing, teams self-assessed at least one level higher than their practice: they think Level 3, they are Level 2. On his reading that gap is itself diagnostic — a team that cannot accurately measure its own AI maturity cannot plan where it is going.

Ryan also argues that Level 2 and every level after it "feels like you are done" when you are not, and that the ceiling at Level 3 is psychological rather than technical: the models are capable of more, but reaching Level 4 requires giving up reading the code entirely and trusting the specification and the evaluation instead. To someone who has spent two decades building a career on the ability to read a function and spot the bug, he writes, that shift feels like negligence — and that feeling is where most teams stall.

## Related Terms

The framework's name refers to [[DefinedTerm/vibe-coding]], though its upper levels describe practices that sit closer to [[DefinedTerm/spec-driven-development]] than to the term's original sense. Ryan's [[Book/spec-driven-development-ai-native-software-engineering]] adopts it as the yardstick for the book's own target, arguing that Level 5 requires infrastructure most organisations cannot justify and that the practical goal is Level 3 or 4.
