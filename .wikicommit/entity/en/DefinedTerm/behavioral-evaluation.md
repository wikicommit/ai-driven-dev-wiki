---
title: "Behavioral Evaluation"
type: "schema:DefinedTerm"
lang: en
sources:
  - type: url
    url: 'https://developers.googleblog.com/the-anatomy-of-harness-engineering-how-to-evaluate-iterate-and-guard-ai-coding-agents/'
    hash: sha256:b7703e83eb963ad1264b1927a931ffc37279d57efe136cc6d02e664b3df6aa63
  - type: url
    url: 'https://developers.openai.com/blog/eval-skills/'
    hash: sha256:51ec56a57b97282cac1e2ff8d92b29b354928a62291f581e9daa7e0697a3597d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"
tags: [evaluation, harness-engineering, agent-architecture]

properties:
  description: "Evaluating an agent by asserting on discrete, observable intermediate actions — which tool it called, which file it modified — rather than on whether it completed an end-to-end task."
---

Behavioral evaluation is the practice of measuring an AI agent by asserting on discrete,
observable actions it takes during execution — whether it asked a clarifying question
when given an underspecified prompt, whether it ran the local validator before declaring
a build-file change complete, whether it consulted live search rather than answering from
memory — instead of scoring whether it solved an entire task end to end. Google engineers
describe such evaluations as functioning like integration tests for improving agent
harness operation, asserting on intermediate execution steps such as specific tool calls
or file modifications rather than on final string equality.

## Usage

The contrast the practice is defined against is the end-to-end benchmark. Google's
engineers characterize the common approach as evaluating an agent the way one would
evaluate a student taking an exam — hand it a large codebase, impose a time limit, and
score it on how many tests pass — and argue that when the resulting composite score moves
by a few percentage points, such benchmarks do not typically answer directly why. Their
examples of what goes unanswered are whether the model became overconfident on an ambiguous prompt, whether it forgot to
verify the test suite before submitting, or whether it hallucinated a CLI flag.

A behavioral evaluation architecture, on their account, separates behavioral assertions
into fast, deterministic, unit-style checks that run locally — their illustration runs a
local behavioural suite in under five seconds. With a rich enough set of them, they argue,
a team has a baseline for the behaviour it is targeting and can iterate on system prompts
or switch models while knowing immediately if a core behaviour has broken. They further
suggest the suite can automate prompt engineering: an LLM tweaks its own system prompt
until a failing test passes, while the rest of the suite acts as a CI/CD-style guardrail
against breaking existing features.

A second vendor describes the same shape of check for a narrower subject, without using the term.
OpenAI's [[BlogPosting/testing-agent-skills-systematically-with-evals]] applies it to agent skills
for [[SoftwareApplication/openai-codex]]: each eval runs the agent on a prompt, records what it did as
a structured JSONL event trace, and scores that trace with deterministic checks — whether the agent
ran `npm install`, whether a `package.json` was created, whether the expected commands ran in the
expected order. The post names "process goals" — did the agent invoke the skill and follow the
intended tools and steps — as one of four kinds of success to define up front, alongside outcome,
style and efficiency goals, and values these checks because a failure can be explained by opening the
trace and reading every command execution in order. Like Google's engineers, it adds a model-graded
step for what fixed checks cannot capture: a second, read-only run that grades style and conventions
against a rubric, constrained to a JSON schema so the result can be compared across runs. It also
tests the skill's triggering, not only its execution, with a small prompt set that includes at least
one negative control — a prompt that should not invoke the skill — to catch the skill firing too
eagerly.

## When It Applies

Google's engineers place these evaluations in the second phase of an agent's development.
Their stated precedent is that when bootstrapping an agent from scratch a team starts with
developer instinct and dogfooding, and that until the agent can dogfood its own codebase —
handling boilerplate, writing its own markdown renderer, executing routine developer
tasks — it does not make sense to run evaluations at all. Evals belong to ensuring forward
progress and guarding against regressions, and they state the primary purpose of a suite
is not to celebrate a 2% improvement but to give confidence that a prompt tweak, tool
schema change or model upgrade did not make the agent holistically worse.

The practice assumes the agent's intermediate steps are observable and assertable — their
example asserts over the tool calls returned on a response — and that the team can name a
specific behaviour worth holding. Their suggested starting point is a three-step loop:
pick one failure mode from a recent mistake the agent actually made; write assertions
matched to task complexity; and automate batch evaluations to monitor stability.

They are explicit about two ways the practice is misapplied. Writing rigid single-turn
assertions on a fixed tool sequence fails for complex tasks, where the model may take an
unexpected but entirely correct path — for those they recommend fuzzier, outcome-based
checks such as [[DefinedTerm/llm-as-a-judge]]. And blocking pull requests on single eval
runs is unsound because model nondeterminism makes them noisy; they recommend tracking
aggregate pass rates over time and treating that directional signal as the thing to act
on.

As to how well-established it is: Google's account is one engineering team's recommended
practice, published on their employer's developer blog and illustrated with their own
SDK, not a measured result or an industry consensus. OpenAI's guide is the same kind of
source — a vendor's recommended practice for its own agent, reporting no measured results. OpenAI's version shares the incremental starting point: it recommends 10–20
prompts for a single skill, growing the set from real failures, and adding slower checks
such as builds or runtime smoke tests only where they reduce risk. They are careful to present it as
complementary rather than replacing larger end-to-end suites — in their framing macro
benchmarks verify the final destination while micro behavioural evals enable safe, rapid
iteration, and the recommendation is to adopt both.

## Related Terms

- [[DefinedTerm/harness-engineering]] — the broader discipline these evaluations serve
- [[DefinedTerm/llm-as-a-judge]] — the fuzzier assertion style recommended for complex tasks
- [[DefinedTerm/trajectory-evaluation]] — another approach that looks at what an agent did rather than only its output
- [[DefinedTerm/verification-loop]] — the general concern with checking an agent's work
