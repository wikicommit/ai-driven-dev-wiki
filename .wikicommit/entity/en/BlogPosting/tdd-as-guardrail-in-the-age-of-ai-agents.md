---
title: "AIエージェント時代に、テスト駆動開発（TDD）は「ガードレール」になる【t_wada×やっとむ対談】"
type: "schema:BlogPosting"
lang: en
tags: [tdd, ai-assisted-programming, agents]
sources:
  - type: url
    url: 'https://agilejourney.uzabase.com/entry/2025/08/29/103000'
    hash: sha256:3ddb48b38b85526ba30bc0c2f6e032f2041384360d5a6e24c4261f8581fefe0d
    license: all-rights-reserved
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An interview in which Takuto Wada and Tsutomu Yasui argue that generative AI has lowered the cost of writing automated tests, and that test-driven development has become a guardrail against coding agents degrading a codebase — because the phrase itself carries both 'it works' and 'it stays maintainable' to a model."
  author: ["和田卓人 (Takuto Wada)", "安井力 (Tsutomu Yasui)"]
  publisher: "Agile Journey by UZABASE"
  datePublished: "2025-08-29"
---

This interview, recorded in early July 2025 and published that August, pairs Takuto Wada — who has spent some twenty years promoting test-driven development in Japan and translated Kent Beck's book on it — with agile coach Tsutomu Yasui. It is pitched deliberately at teams that have not yet adopted coding agents and are working in codebases with little or no test coverage, rather than at people already running agents at scale.

Its first argument is that generative AI has lowered two long-standing barriers to automated testing at once: the learning cost, because writing a program that verifies another program is a distinct skill many developers never acquire, and the implementation cost. What the model produces is not necessarily high quality, but it is enough to take a first step and start a feedback cycle. The pair single out characterization tests — tests that capture how existing code behaves now rather than how it should behave — as where AI is strongest, because capturing current behaviour is an after-the-fact request that can be given a narrow context.

Its second and titular argument is that TDD has become a guardrail for agent-written code. Wada's account is that agents break working code while searching for a solution, and that an automated test suite is the right instrument for telling an agent to keep what worked working. But passing tests alone does not produce maintainable code, and the phrase "test-driven development" is useful precisely because it carries both halves — working and maintainable — in a single workflow the models already know.

## Key Points

- Wada dates the shift to late 2024 and early 2025, and says the arrival of Claude Code in Japan, with flat-rate access from May, was decisive; he judges enterprise adoption still slow, largely because there were few enterprise plans and companies were handing out individual plans instead.
- He argues teams are often not ready for coding agents: getting good generation out of a model presupposes that development documentation, the repository and CI/CD are already in reasonable shape.
- Generative AI lowered both the learning cost and the implementation cost of automated testing; Wada's claim is that the number of people writing automated tests has clearly increased because of it.
- Yasui notes AI-written tests come with real defects — mocks everywhere so it is unclear what is being tested, overlong fixtures and setup — but that they are enough to let a human take a first step.
- Yasui also warns of the opposite reading: assuming that because AI can write code, tests are unnecessary. Spotting where AI-generated code has drifted requires skill on the human side, and without it problems go unnoticed.
- Wada distinguishes "To-Be" tests (how a system should behave), which TDD needs and which require human skill or software archaeology, from "As-Is" characterization tests, at which he says AI is extremely effective.
- Yasui adds that characterization tests are exactly what is wanted in the maintenance phase, where teams are smaller and less practised at writing test code.
- On test design, Yasui reports that simply asking a model to write tests does not make it reason logically, but naming a technique — boundary value analysis, a decision table, equivalence classes — produces respectable results: giving AI the tools humans use to think logically makes it think logically too.
- Wada puts the point at which careful, test-backed development overtakes ship-and-break development at roughly one month before AI, and roughly a few days as of July 2025 — explicitly an impression gathered from asking conference audiences, not measured data.
- He reports that telling Claude Code "proceed with TDD" tended to produce only "write a lot of tests first", and that using the names of people associated with stricter TDD is reported to convey the classical one-test-fail-then-pass cycle instead.
- Wada connects this to design patterns and pattern languages: giving a problem a name so a short word transmits a whole solution is what that 1990s effort wanted, and he sees it working with models in a way it never quite did between people.
- Yasui argues TDD can hold down the gap between the code and the humans' understanding of it — Ward Cunningham's original sense of technical debt — which AI-written code widens quickly.
- Wada argues delegation to a self-driving agent is if anything more reason to instruct it in TDD, not less, because an unattended agent produces large volumes of code that may work but is unmaintainable.
- On Scrum, Yasui's position is that the roles define who holds which responsibility rather than who does which task, so the structure survives AI, while how each role works changes; he expects a shift toward very small, highly productive teams.
- Both argue the bottleneck in software engineering was never writing code — it was documentation drifting from source, finding what to change, and having to write tests — and that this is where coding agents have their real effect.
- On whether engineers become unnecessary, Wada's honest answer as of July 2025 is that he does not know, and he says he is planning for both futures; he argues the remaining difficulty is sustaining a system rather than producing one, and that turning wants into requirements is the skill non-engineers mostly lack.
- Wada frames the differentiator not as seniority but as negative capability — tolerance for uncertainty, curiosity, flexibility — and suggests junior engineers may be at an advantage for having more disposable time.

## Context

The piece is a conversation rather than a study, and both participants repeatedly mark their claims as impressions: the "a few days" figure is explicitly a feel derived from asking audiences, and the observation about person-names working as prompts is relayed as something reported by others rather than measured. Wada also flags that when vendor engineering guidance says TDD is reinforced by agents, he is not certain the practice being described is TDD in the strict sense he means.

Both participants have a stake in the subject that the interview makes plain. Wada translated Kent Beck's *Test-Driven Development* into Japanese and has spent two decades advocating the practice, and he says frankly that his own knowledge is now inside the models, making him a competitor to them as a consultant. Yasui is an agile coach who designs and sells workshop games. The framing that TDD turns out to matter more in the agent era is, on Wada's own account, a development he did not predict and had not been arguing for.

The interview sits alongside other Japanese-language practitioner writing on the same point: [[BlogPosting/making-ai-do-t-wada-style-tdd]] reports building a tool with an agent instructed to follow Wada's formulation of TDD, and reaches compatible conclusions about which parts stay in human hands.
