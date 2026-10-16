---
title: "Hard Budget Cap"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, cost-management]
aliases: ["Default hard budget cap"]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Oct/3/default-hard-budget-caps/'
    hash: sha256:6d4349c14e4efe949ff156fce237da60492a3d27f85c1287196a9656f546a5b6
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "A spending limit on a pay-by-usage service or API that cuts the service off and returns errors once the limit is reached, as opposed to a soft cap that only sends a warning; Simon Willison argues it should be the default because agents make it easy to spin up code that incurs costs."
---

A hard budget cap is a feature of a pay-by-usage service or API that lets a customer say "after $X/month,
cut this thing off and return errors": once the configured spending limit is reached, the service stops
rather than continuing to accrue charges. It is defined against a soft cap, which only sends a warning
— for example an email — when the threshold is crossed and lets usage continue. Simon Willison uses the
phrase **default hard budget caps** for his proposal that such a cap be on by default, with removing it
an explicit opt-in.

## Usage

Willison frames the need in terms of [[DefinedTerm/ai-coding-agent]] use, in
[[BlogPosting/we-are-going-to-need-default-hard-budget-caps]]: coding agents and personal agents greatly
reduce the friction of spinning up code that does useful things, and some of that code costs money —
calls to paid APIs, hosted web applications, or systems that bill for additional storage and compute. A
soft cap does not protect against the case he describes, a rogue service consuming hundreds or thousands
of dollars of usage overnight while its owner sleeps after a midnight warning email. He proposes that
opting out of the cap be a clear, prominent checkbox in which the user accepts that the application will
not be shut down and that they are responsible for subsequent charges, and that agents themselves could
favour recommending providers that offer hard caps and warn inexperienced builders away from uncapped
services.

He points to two cloud providers that had recently added features of this kind: AWS introduced a monthly spend
limit for projects that pauses a project for the month once its limit is reached, still rolling out to
a limited number of customers, and Google Cloud introduced Spend Caps, which set a monthly financial cap
on specific services within a project.

## When It Applies

The proposal is aimed at pay-by-usage services where runaway usage can produce an open-ended bill. Its
main trade-off is stated by Willison himself: businesses may not want hosted applications to start
returning errors because a budget was exceeded. His answer — that most businesses and individuals would
prefer errors to a surprise bill of $10,000 or more — is his own expectation rather than a measured
finding, and making the cap the default is his proposal in a single opinion post rather than an
established convention.

## Related Terms

[[DefinedTerm/ai-coding-agent]]
