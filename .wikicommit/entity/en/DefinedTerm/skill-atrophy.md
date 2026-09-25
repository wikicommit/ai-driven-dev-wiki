---
title: "Skill Atrophy"
type: "schema:DefinedTerm"
lang: en
tags: [human-oversight, ai-assisted-programming, agentic-engineering]
sources:
  - type: url
    url: 'https://addyosmani.com/agentic-engineering/skill-atrophy/'
    hash: sha256:093e78f49a3b3b5adf304d52c21d5f996df2d142d90137b42629a4ffc505058a
  - type: url
    url: 'https://www.anthropic.com/research/how-ai-is-transforming-work-at-anthropic'
    hash: sha256:768151bc1fd55f4171a86c1cf74c112f09821eebf20b00b6dcd176e957394536
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The gradual loss of an engineering skill through disuse when AI agents consistently take over the work that used to exercise it - a risk framed not as a reason to avoid AI tools but as a reason to keep practising the skills that a reviewing role depends on."
---

Skill atrophy is what happens when a skill stops being practised and the ability to perform it
gradually degrades. Addy Osmani's agentic engineering glossary applies the term to software
development: if an AI agent handles a developer's error handling, debugging, architecture decisions
and algorithm implementation, that developer may find themselves slower and less confident when the
AI is unavailable — not because the capability was never there, but because skills need regular
exercise to stay sharp. The glossary draws the analogy to pilots whose manual flying degrades under
heavy autopilot use and to surgeons who lose precision when they do not operate regularly.

The entry is explicit that this is not an argument against using AI tools. It presents skill atrophy
as a reason to use them thoughtfully — keeping the skills that matter while letting AI take the work
where human effort adds the least value.

## Usage

Within [[DefinedTerm/agentic-engineering]] the concern is framed as a dependency rather than a side
effect: the glossary argues that agentic engineering explicitly requires strong engineering
fundamentals, because AI-generated code cannot be reviewed effectively by someone who does not
deeply understand the code, good specifications cannot be written without understanding the
technical constraints, and a flawed architectural decision by an agent cannot be recognised by
someone who has never designed a system. Osmani states this as a paradox: the better AI gets at
writing code, the more important it becomes for engineers to understand code deeply, because the
human role shifts from writing to evaluation and evaluation demands even stronger skills than
writing does.

The entry lists six counter-practices. Intentional practice means periodically writing code by hand
for important or educational tasks even where AI would be faster. Deep review means reading AI output
closely — understanding why each decision was made and considering alternatives — rather than
scanning it. Debugging skills are kept by resisting the urge to hand a breakage straight back to the
AI and debugging it first, which is where the entry locates the development of deep understanding.
Teaching and explaining is offered as a test: being unable to explain AI-generated code to a
colleague indicates it is not understood well enough. Balanced delegation means using AI for routine
work such as boilerplate, tests and documentation while keeping architectural and complex logic work
in human hands. Learning new things frames AI as a learning accelerator rather than a learning
replacement — it should expand what a developer can build, not narrow what they understand.

The concern also appears in practitioners' own accounts. In
[[Report/how-ai-is-transforming-work-at-anthropic]], Anthropic's study of its own engineers and
researchers, some interviewees worried about "skills atrophying as [they] delegate more" and about losing
the incidental learning that comes from working through a problem by hand — reading docs and code that
builds a model of how a system works even when it does not directly solve the problem at hand. The study
ties this to what it calls the [[DefinedTerm/paradox-of-supervision]]: using Claude effectively requires
supervising it, and supervising it requires the coding skills that may atrophy. It also records that
engineers were divided on how much this matters. Some deliberately practise without AI to stay sharp;
others were unworried, saying AI helped them learn faster, that they had only lost less important skills,
or that lost skills could come back if needed; and one questioned the premise, arguing that coding will
not return to the way it was before these tools.

## Related Terms

[[DefinedTerm/automation-bias]], [[DefinedTerm/the-70-percent-problem]],
[[DefinedTerm/cognitive-debt]], [[DefinedTerm/human-in-the-loop]],
[[DefinedTerm/paradox-of-supervision]]
