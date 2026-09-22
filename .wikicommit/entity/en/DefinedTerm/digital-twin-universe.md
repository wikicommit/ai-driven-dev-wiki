---
title: "Digital Twin Universe"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, agents, evaluation, verification, agent-tooling]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Feb/7/software-factory/'
    hash: sha256:f037b61ef74329e98d22e3f5e86498585708d651d71581e420890095020b0ad3
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "StrongDM's AI team's term for a set of agent-built behavioural clones of the third-party services their software depends on, replicating those services' APIs, edge cases and observable behaviours so that scenarios can be run against them at volumes and in failure modes the live services would not permit."
---

The Digital Twin Universe, abbreviated DTU, is [[Organization/strongdm]]'s AI team's term for
behavioural clones of the third-party services their software depends on, built to replicate those
services' APIs, edge cases and observable behaviours. Twins were built for Okta, Jira, Slack, Google
Docs, Google Drive and Google Sheets. The point of a twin is not fidelity for its own sake but
somewhere to run validation: with the DTU in place, the team state they can validate at volumes and
rates far exceeding production limits, test failure modes that would be dangerous or impossible
against live services, and run thousands of scenarios per hour without hitting rate limits,
triggering abuse detection or accumulating API costs.

## Usage

The twins are themselves agent-built, which is what makes the idea cheap enough to act on. As
[[BlogPosting/how-strongdms-ai-team-build-serious-software-without-even-looking-at-the-code]]
understood the technique, a twin is produced by feeding a service's full public API documentation
into the team's agent harness and having it build an imitation as a self-contained Go binary, with a
simplified UI generated over the top to complete the simulation. An update to that post relays the
DTU's creator stating a repeatable strategy for fidelity: use the most popular publicly available
reference SDK client libraries as compatibility targets, with the goal always being 100%
compatibility.

Within the team's [[DefinedTerm/software-factory]], the DTU is what a scenario runs against. Their
scenario tests become scripts for agents to execute continuously against systems as those systems
are being built, and the twins are populated with simulated users and traffic — the illustration
given is a Slack twin carrying a stream of simulated directory users about to need access to
different simulated systems.

## When It Applies

The conditions are set by what the software under test talks to: the DTU addresses software whose
behaviour is mostly mediated by third-party SaaS APIs, where the validation a team wants is blocked
not by difficulty but by the live services' rate limits, abuse detection, costs and irreversibility.
It assumes those services have public API documentation thorough enough for an agent to build
against, and that a client-library-level compatibility target is a good enough proxy for the
behaviour that matters.

The team's own argument for why this is new is economic rather than technical: creating a
high-fidelity clone of a significant SaaS application was always possible but never economically
feasible, and they state that generations of engineers may have wanted a full in-memory replica of a
system to test against but self-censored the proposal to build it. The corresponding exposure is
that a twin is an imitation — its fidelity is asserted against reference client libraries, not
against the real service's full behaviour — so what it can miss is whatever the compatibility target
does not exercise.

How well established it is: this is one team's named practice, described by them and relayed by a
practitioner who saw it demonstrated, with the build technique explicitly given as his
understanding rather than their documentation. It is not a measured result or a convention with
independent practitioners.

## Related Terms

[[DefinedTerm/software-factory]], [[DefinedTerm/agent-harness]], [[DefinedTerm/behavioral-evaluation]], [[DefinedTerm/trajectory-evaluation]], [[DefinedTerm/data-aware-testing]]
