---
title: "Stop Hand-Holding Your Coding Agent: Engineering the Loops that Replace Step-by-Step Prompting"
type: "schema:ScholarlyArticle"
lang: en
tags: [loop-engineering, coding-agents, position-paper]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.00038'
    hash: sha256:2f17c51102988847128a0fb57824555d6ac3a32183f9ed61e269f1a63d48d4c0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A position paper anchored in a descriptive corpus study that defines the loop specification as the object of loop engineering, gives it an anatomy and taxonomy, hand-codes the fifty loops of the public Loop Library, and grounds design principles and anti-patterns in research on self-correction, reward hacking and model-as-judge fragility."
  author: ["Sandeco Macedo"]
  abstract: "In mid-2026 a slogan reorganized how practitioners talk about coding agents: stop prompting your agent, start designing the loop that prompts it. The paper calls the object of the new practice the loop specification — a bounded, reusable artifact made of a trigger, a goal, a verification step, a stopping rule and a memory, handed to an agent harness such as Claude Code or Codex so the agent pursues a goal on its own. It distinguishes this from an ordinary programming loop and from the harness's internal perceive-act-observe cycle, positions loop engineering as a new layer after prompt, context and harness, and argues that it does not retire prompt engineering. Its contributions are a definition and scope, an anatomy and taxonomy including a five-level verification ladder and named terminal states, a descriptive analysis of the fifty-loop Loop Library, and design principles and anti-patterns. Seventy percent of the loops verify in the autonomous zone of the ladder and seventy-four percent name their terminal states, while automated triggering and durable memory remain underdeveloped."
  keywords: ["loop engineering", "loop specification", "coding agents", "verification", "agent harness"]
---

This single-author position paper from the Instituto Federal de Goiás in Brazil sets out to give
the mid-2026 practitioner slogan behind [[DefinedTerm/loop-engineering]] — stop prompting the
coding agent at every step and design the loop that prompts it — a reviewable account. It notes that
the concept arrived through threads, talks and blog posts rather than through any reviewable
account, and asks what exactly is being built, how it relates to the loops that already exist inside
an agent, what a corpus of real loops looks like, and which practitioner claims survive contact with
the scientific literature.

Its central move is to fix the object of study as the [[DefinedTerm/loop-specification]]: an
external, bounded, reusable artifact — trigger, goal, verification, stopping rule and memory — that a
human designs and hands to an agent harness such as [[SoftwareApplication/claude-code]] or Codex.
This is kept separate from an ordinary programming loop and from the internal cycle in which the
model runs tools over a stop condition, which the paper treats as plumbing of the
[[DefinedTerm/agent-harness]]: "the harness supplies the engine; loop engineering writes the pilot."
It places loop engineering as a fourth layer after [[DefinedTerm/prompt-engineering]],
[[DefinedTerm/context-engineering]] and [[DefinedTerm/harness-engineering]], each subsuming the
previous one, and argues against the strongest headlines that loops do not make prompt engineering
obsolete.

The paper then gives an anatomy and taxonomy of loop specifications, codes the fifty loops of the
public Loop Library catalogue by hand, distils design principles and anti-patterns, and releases an
authoring skill, [[SoftwareApplication/sandeco-loop]], as an accompanying deliverable. It explicitly
runs no loops under a measured budget and claims no benchmark result.

## Key Points

- The paper defines a loop specification as a bounded, reusable artifact of five parts — a trigger
  (a person, a schedule or an event), a preferably verifiable goal, an execution phase ideally
  calling proven named skills, a real verification, and a stopping rule driving the loop to a named
  terminal state — plus a memory of progress and decisions kept on disk rather than in the
  conversation.
- It holds that the central skill of the practice is designing the check that decides when the
  work is done, not writing a better prompt, and that a loop is justified over a bare scheduled
  prompt only when the result of one turn changes the next action.
- Its taxonomy classifies loops by trigger, goal type (verifiable, judged by a model against a
  rubric, or mixed), a five-level [[DefinedTerm/verification-ladder]], architecture (solo,
  maker–checker, or manager orchestrating helpers) and named terminal states (success, no-op,
  blocked, stalled, exhausted), with an error or exhausted budget never counting as success.
- In its hand-coding of the fifty Loop Library loops, half verify deterministically and seventy
  percent verify in the ladder's autonomous zone; seventy-four percent name their terminal states
  and sixty-six percent set a verifiable goal.
- The same corpus is least developed where loops would run without a person: the trigger is manual
  in seventy-eight percent of loops, seventy-eight percent run a single agent, only twenty percent
  call named reusable skills, and only thirty-two percent develop persistent memory — which the
  paper calls a maturity mismatch.
- Of the eleven loops whose dominant check is a model judge, most pair it with a maker–checker
  architecture or a separate critic.
- It organizes design principles into four families — define "done" before anything else, act
  without breaking what works, earn trust in the result, and sustain the loop over time — and names
  five anti-patterns: the while-true around a stranger, the self-approving loop (reward hacking),
  specification gaming, pretending level 4 is level 1, and the unattended runaway.
- It proposes cost per accepted change — tokens or money spent divided by the number of changes that
  survived verification — as the headline metric for the empirical study it does not itself run.
- Its limits for the practice include the verification burden, [[DefinedTerm/comprehension-debt]]
  and [[DefinedTerm/cognitive-surrender]]; it argues that the loop automates the typing, not the
  judgment, and lists cases where a loop is the wrong tool.

## Notes

The author describes the fifty-loop coding as a qualitative reading of a single public catalogue
that another coder might code differently, not a random sample of loops in the wild, and states that
the transfer of lessons from research on the internal agent cycle to the external loop is an argued
analogy rather than a measured result. No usage data is reported for the released skill. Among its
illustrations, it presents the [[DefinedTerm/ralph-loop]] as the purest case of keeping all state in
files while replaying the same prompt with a fresh context each turn. The paper draws its operational
anatomy of a loop system from a practitioner post, [[BlogPosting/loop-engineering]], and cites
[[BlogPosting/designing-agentic-loops]] among its practitioner sources.
