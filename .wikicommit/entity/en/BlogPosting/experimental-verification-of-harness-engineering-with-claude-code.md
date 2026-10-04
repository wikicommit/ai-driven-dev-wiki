---
title: "Claude Codeで試すHarness Engineeringの実験的検証"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, hooks, quality-gates, claude-code]
sources:
  - type: url
    url: 'https://techblog.sakurug.co.jp/article/jdqkqgjavou/'
    hash: sha256:97ebf1fecfb6856f0d67a0b0c6c1466afc4956a0f246c1c7452db796e4a00c3e
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A small controlled experiment in which Claude Code built the same customer-management app under five cumulative harness conditions, from prompt only up to a Red/Green/Refactor stop gate, concluding that a harness fixes the intermediate checks and the definition of done rather than raising the best-case output."
  author: "Akiyoshi"
  datePublished: "2026-03-30"
  publisher: "SAKURUG TECHBLOG"
---

This post on SAKURUG's engineering blog sets out to answer the practical question behind [[DefinedTerm/harness-engineering]]: what does adding a given element change, and where does it act? The author had [[SoftwareApplication/claude-code]] build the same small customer-management screen — list, search, filter, create, edit, delete, validation and persistence on Nuxt 4, Hono, Drizzle ORM and SQLite — from one fixed prompt under five cumulative conditions, orchestrated only through [[DefinedTerm/claude-md]] and [[DefinedTerm/agent-hooks]], without Skills or subagents. The author acted only as the operator running commands; the write-up of the experiment's results was itself produced by an AI agent.

The five conditions were: A, prompt only; B, adding a `CLAUDE.md`; C, adding a PostToolUse hook that runs lint, typecheck and test after every file edit and returns failures to the agent; D, adding a UI checklist and a Stop completion gate that refuses to let the agent finish while checklist items remain or the e2e suite fails; and E, which the post calls "Gate TDD", splitting the stop gate into Red (automated checks and the checklist), Green (a critical UI review that must report no remaining issues) and Refactor (an internal-structure checklist followed by re-running the checks).

Every condition's final build passed lint, typecheck, unit tests and e2e tests, so on final checks alone the five were indistinguishable. The post's argument is that the difference lies elsewhere: in how often the harness pushed back during the run, and in what the agent was permitted to count as finished.

## Key Points

- On a first run, the prompt-only condition produced what looked like the most polished result. A rerun of the same condition produced an English-leaning UI instead of a Japanese one, a mix of Japanese and English seed data, different file locations and a different major version of the framework dependency, yet still passed every check. The author's reading is that prompt only reliably reaches *a* passing solution but not *the same* solution.
- Adding `CLAUDE.md` stabilized the directory layout but did not control data quality: condition B's seed data consisted of auto-generated test strings. The post judges `CLAUDE.md` not decisive for completing a task of this size, but the foundation every later condition built on, since it is where the hooks and gates are described to the agent.
- The PostToolUse hook blocked 31 of its 37 firings in condition C. Its history showed checks passing progressively but with repeated regressions, where fixing one place broke another; the post values the hook as much for recording when and what broke as for catching it. C nevertheless finished with 60 lint warnings and a nearly empty screen, because the hook returns failures but leaves the decision that the work is complete to the agent.
- In condition D the Stop gate fired five times and blocked four: three times for an incomplete checklist, and once for two failing e2e tests after the checklist had been fully ticked. The author argues that without the gate that regression would probably have shipped. D ended with no lint warnings, but still produced an English UI and seed data named like test fixtures — aspects the gate did not measure.
- Condition E's stop gate fired nine times and blocked eight (once at Red, twice at Green, five times at Refactor). Its final build had a Japanese UI, realistic seed data without placeholder words, and passed a critical UI review and refactoring checklist, extending the completion criteria from tests and checklists to review and restructuring.
- The post summarizes the four elements as acting on different targets: `CLAUDE.md` fixes the premises, the PostToolUse hook guards intermediate quality, the checklist and stop gate decide functional completion, and the critical review and refactor checklist decide whether critical review and restructuring have been done. It treats them as independent layers — intervening during the run and fixing the end condition are separate concerns.
- Its overall conclusion is that a harness replaces "happens to go well" with "reliably keeps a minimum standard", widening what counts as done; it does not guarantee the best output, and layout density and visual quality still depend on how the review document is designed and how critical the agent is.
- For individual developers the author proposes an adoption order: write structure and minimum completion criteria in `CLAUDE.md`; return static checks through a PostToolUse hook; add a checklist and stop gate for UI-heavy work; and move to a Red/Green/Refactor gate where UI quality or language handling still slips through.

## Context

The author is explicit about the limits of the evidence: conditions B to E were each run once and A twice, too few to say anything about the variance of the block rates or firing counts, and token consumption and elapsed time added by the hooks were not measured. What the post holds to despite that is a structural observation — only the conditions with hooks and gates left a record of how many times, and why, the agent was sent back.
