---
title: "Initializer Agent"
type: "schema:DefinedTerm"
lang: en
tags: [long-running-agents, harness-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
    hash: sha256:26ce4c203cbb030f31253f1eb174b46b2c0203c9b44576aa4654b89b4d7be777
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The first session of a long-running agent run, given a different prompt from every session after it: instead of doing the work, it builds the environment later sessions will work inside — a startup script, a progress log, an initial commit, and a structured list of every feature the task implies."
---

An initializer agent is the first agent session in a long-running run, distinguished from the
sessions that follow it only by its prompt: rather than making progress on the task, it lays the
foundations that all later sessions depend on. In the account it comes from, that means writing an
`init.sh` script that can start the development server, a progress file recording what agents have
done, an initial git commit showing the files added, and a structured list of every feature the
user's prompt implies, each marked as not yet passing. The source is explicit that the separation is
one of prompt only — the system prompt, tool set and harness are otherwise identical to the coding
agent's.

## Usage

The role exists to answer a specific failure. A [[DefinedTerm/long-running-agent]] given a
high-level goal tends to attempt the whole thing at once and exhaust its context mid-implementation;
and once some progress exists, a later session can look around, see work has been done, and declare
the job finished. Neither is fixed by better in-session behaviour, because neither session can see
what the task as a whole requires. An up-front enumeration of the work — the feature list, every
entry failing — gives each later session both a clear outline of full functionality and an
unambiguous next thing to do.

The artifacts it produces are what a fresh context window reads to get its bearings, alongside the
git history. The source reports choosing JSON for the feature list after experimentation, on the
grounds that the model is less likely to inappropriately change or overwrite a JSON file than a
Markdown one, and reinforces this by permitting later agents to edit only a feature's pass status,
with strongly-worded instructions against removing or editing tests.

## When It Applies

The pattern assumes a task large enough to span multiple context windows and a goal concrete enough
to be decomposed up front into verifiable features — the worked example expanded a single prompt into
over 200 of them. It assumes durable storage the later sessions share, since the entire mechanism is
artifacts on disk plus git history; and it assumes each later session can actually verify a feature,
which in the source's setting meant browser automation.

Its misapplication is the mirror of the failure it fixes: a feature list that does not anticipate what
the prompt requires leaves later sessions working towards the wrong outline, and the source's own
guard against later agents rewriting that list is prompt wording rather than enforcement. How
well-established it is should be read with its provenance in mind — it is reported by Anthropic from
internal experimentation on a single full-stack web application built with its own SDK, presented as
one possible set of solutions, with whether a multi-agent architecture of specialists would do better
left explicitly open. See [[BlogPosting/effective-harnesses-for-long-running-agents]].

## Related Terms

[[DefinedTerm/long-running-agent]], [[DefinedTerm/harness-engineering]],
[[DefinedTerm/checkpoint-and-resume]], [[DefinedTerm/structured-note-taking]],
[[DefinedTerm/compaction]], [[DefinedTerm/planner-worker-model]]
