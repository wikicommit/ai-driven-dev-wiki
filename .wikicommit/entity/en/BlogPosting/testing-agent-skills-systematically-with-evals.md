---
title: "Testing Agent Skills Systematically with Evals"
type: "schema:BlogPosting"
lang: en
tags: [agent-skills, evaluation, coding-agents]
sources:
  - type: url
    url: 'https://developers.openai.com/blog/eval-skills/'
    hash: sha256:51ec56a57b97282cac1e2ff8d92b29b354928a62291f581e9daa7e0697a3597d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A January 2026 post on OpenAI's developer blog that sets out a pattern for evaluating Codex agent skills: define measurable success first, run a small prompt set including negative controls, score the recorded event trace with deterministic checks, and add a rubric-based model-graded style check with a structured output schema."
  author: ["Dominik Kundel", "Gabriel Chua"]
  publisher: "[[Organization/openai]]"
  datePublished: "2026-01-22"
---

*Testing Agent Skills Systematically with Evals*, published on OpenAI's developer blog on 22 January
2026, is a practical guide to treating a skill for [[SoftwareApplication/openai-codex]] — in
the sense of [[DefinedTerm/agent-skills]] — as something that can be tested, scored and improved over time.
Its starting problem is that when iterating on a skill it is hard to tell whether a change improved it
or merely changed its behaviour, and that regressions slip in: the skill does not trigger, skips a
required step, or leaves extra files behind.

The post's premise is that a skill is an organized collection of prompts and instructions for an LLM,
so the most reliable way to improve one is to evaluate it the way one would any other prompt. It
defines an eval as a prompt, a captured run (trace and artifacts), a small set of checks, and a score
that can be compared over time — in practice, it says, something close to a lightweight end-to-end
test. The walkthrough uses a deliberately minimal example skill, `setup-demo-app`, which scaffolds a
small React demo app with a fixed file structure and an explicit definition of done.

## Key Points

- Success should be written down in measurable terms before the skill is written, split into outcome
  goals (did the task complete), process goals (did Codex invoke the skill and follow the intended
  tools and steps), style goals (does the output follow the requested conventions) and efficiency goals
  (did it get there without thrashing). The post recommends keeping this list small and limited to
  must-pass checks.
- A Codex skill is a directory with a `SKILL.md` file whose YAML front matter carries a `name` and
  `description`; the post singles these out as the primary signals Codex uses to decide whether to
  invoke the skill and when to load the rest of the file, so vague or overloaded values make triggering
  unreliable.
- The first pass should be manual: explicitly invoke the skill in a real or scratch repository and look
  for hidden assumptions about triggering, environment and execution order. The post treats every
  manual fix made at this stage as a candidate for a future eval.
- A small prompt set of 10–20 cases is presented as enough for a single skill. The example set mixes
  explicit invocation, implicit invocation, contextual invocation with extra domain detail, and at least
  one negative control that should not trigger the skill, to catch false positives where the skill fires
  too eagerly.
- Deterministic checks run over the structured event trace that `codex exec --json` writes as JSONL —
  for example whether `npm install` was run or `package.json` was created — so that a failing check can
  be explained by reading the trace.
- Qualitative requirements such as component structure and styling conventions are graded by a second,
  read-only `codex exec` run whose final answer is constrained by `--output-schema` to a rubric JSON
  object with an overall pass, a score and per-check results.
- The post suggests extending the suite as the skill matures — counting commands to catch looping,
  tracking token usage, running a build or a runtime smoke check, checking that the repository is left
  clean, and checking that the skill works without escalated permissions — adding slower checks only
  where they reduce risk.
- Its closing advice is to let real failures drive coverage: every miss found in development or use
  becomes a new row in the prompt set, which the post describes as a living record of what the skill
  must keep getting right.

## Context

This is OpenAI's own guidance for its own agent and CLI, and every command in it is a Codex command;
the post reports no measured results from applying the method. Its central move is to evaluate a skill
on what the agent did — which commands it ran, in what order, with which files resulting — rather than
only on how the final output looks, and it explicitly contrasts that with asking whether a change "feels
better" or relying on vibes. Its pattern pairs deterministic checks on the agent's recorded actions
with a model-graded rubric for what rules cannot capture, starting with the fast checks and adding
slower, heavier ones only where they add confidence.
