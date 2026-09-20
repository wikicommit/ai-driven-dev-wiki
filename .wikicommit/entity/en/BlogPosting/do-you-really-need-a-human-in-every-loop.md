---
title: "Do you really need a human in every loop?"
type: "schema:BlogPosting"
lang: en
tags: [agents, human-oversight, guardrails, governance, coding-agents]
sources:
  - type: url
    url: 'https://www.port.io/blog/human-in-the-loop-for-ai-coding-agents'
    hash: sha256:766abcbeb6946c92580399d54cd8330c0edeb8fda6e8e61aefb36579d744524c
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A vendor post arguing that the useful question is not whether a human is in the loop but what pulls the human in, distinguishing deterministic rule-based gates from agent-scored risk-based gates and giving a lookup-versus-judgment test for choosing between them."
  author: "Matar Peles"
  publisher: "Port"
---

The post opens by answering its own title: no, you do not need a human in every loop, and trying to
put one there is how teams stall their move to autonomous engineering. The pattern it describes is
a team that starts running AI agents and, to stay safe, puts a person in front of everything the
agent does — which worked while agents only suggested code, because reviewing a diff is something
engineers already do, but which starts holding the team back once the agents act in production,
deploying services, restarting workloads and resolving incidents. The author reports that when Port
surveyed engineering leaders at a recent meetup, half the room said they still gate only code
merges and pull requests, which the post characterises as the same review they ran before agents
existed and one that breaks the moment an agent does something a pull request never covered.

Its reframing is that the fix is not more gates or fewer gates but the right gate in the right
place, and that the useful question is no longer whether a human is in the loop but what pulls the
human in. Two kinds of guardrail answer that question, and the post presents them as opposites in
how they decide: a [[DefinedTerm/rule-based-gate]] is a fixed checklist you own, and a
[[DefinedTerm/risk-based-gate]] is a judgment an agent makes on the spot.

## Key Points

- [[DefinedTerm/human-in-the-loop]] is defined here as an oversight model in which agents do the
  work but cannot make irreversible changes without a human's approval. The post argues the phrase
  gets treated as a single setting to turn on when it is really an oversight pattern that has been
  changing underfoot: reviewing every output was enough when agents only proposed changes, and does
  not scale once they take real actions.
- The test for which gate fits a given action is whether you can write the condition down. If the
  trigger can be stated as a rule that is right every time, use a rule-based gate — the post is
  explicit that this includes time windows, so rules handle "when", not just "what". If deciding
  means weighing signals you cannot reduce to a clean condition, use a risk-based gate.
- The dividing line is stated as lookup versus judgment rather than as whether context matters,
  since rules handle plenty of context such as time and environment. The post's worked examples put
  service tier, a Friday release freeze and data classification on the rule side, and blast radius
  across a dependency graph, how severe an incident really is, and whether a deploy is anomalous
  for a given service on the risk side. It expects most teams to run both.
- Running a rule-based gate properly means making the condition explicit and giving it an owner so
  it can be audited and changed on purpose, having the condition read from real data rather than a
  hardcoded guess, and logging every time the gate fires.
- Running a risk-based gate properly means setting a clear threshold for the score that flips an
  action from "let it run" to "block for review" and expecting to tune it, tracing every decision
  including what the model scored and what context it used, and defaulting to the stricter path
  when the model is unsure — so that thin context produces a human review and never a silent pass.
- The post's unifying claim is that both gates are only as trustworthy as the context underneath
  them: a rule with no real data to check is a guess, and a risk score over thin context hides a bad
  guess behind a number. It treats that shared dependency as what makes the problem a platform
  problem rather than a per-workflow one.

## Context

This is a vendor post, and its argument lands on that vendor's product: the case it builds is that
because both gate types need thresholds, tracing and safe fallbacks and both run on the same live
context, hand-wiring them into every workflow stops being an option, and what is needed is one
platform where both are native composable steps. What [[SoftwareApplication/port]] offers against
that description is set out in the post's closing sections, and the framing and the product are not
separable here. The post also states the position that oversight then stops being a tax on
velocity, because a governed workflow becomes the easy one to build.
