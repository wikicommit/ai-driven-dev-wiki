---
title: "We’re going to need default hard budget caps on pretty much everything"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, cost-management]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Oct/3/default-hard-budget-caps/'
    hash: sha256:6d4349c14e4efe949ff156fce237da60492a3d27f85c1287196a9656f546a5b6
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "A short post arguing that pay-by-usage services and APIs need hard budget caps that cut a service off once a spending limit is reached, enabled by default, because coding agents and personal agents make it much easier to spin up code that runs up costs."
  author: ["Simon Willison"]
  datePublished: "2026-10-03"
---

The post argues for a product feature its author expects the world to need a great deal more of:
[[DefinedTerm/hard-budget-cap|default hard budget caps]] on pay-by-usage services and APIs. By a hard
cap he means a setting that says "after $X/month, cut this thing off and return errors"; a soft cap
that only sends a warning email once the threshold is crossed, he says, will not cut it.

His reason is tied to agents. Coding agents, and personal agents — which he describes as coding agents
wrapped in a less threatening UI — greatly reduce the friction of spinning up code that does useful
things, and some of those things cost money: calls to paid APIs, hosted web applications, or systems
that can bill for additional storage and compute. The failure he has in mind is waking up to a
midnight warning email and finding that a rogue service has consumed several hundred, or several
thousand, more dollars of usage overnight.

He takes the counter-argument — that businesses do not want hosted applications to start throwing
errors because a budget was exceeded — and answers it with an expectation rather than a measurement:
most businesses and individuals, he expects, would prefer errors to a surprise bill of $10,000 or
more. Going beyond the cap should therefore be opt-in, behind a clear, prominent checkbox stating that
the application will not be shut down and that the user is responsible for subsequent charges.

## Key Points
- Pay-by-usage services and APIs should offer hard budget caps that stop the service and return
  errors once a spending threshold is reached; a warning-only soft cap is not enough.
- The cap should be on by default, with removing it an explicit opt-in.
- Coding agents and personal agents lower the friction of creating code that incurs costs, which is
  why the author expects the need for such caps to grow.
- The author expects most businesses and individuals to prefer service errors over an unexpectedly
  large bill — stated as his expectation, not as a measured result.
- AWS is the service he most wanted this from, based on stories he has heard of people avoiding it
  for personal projects for fear of a runaway bill, and of others who were seriously burned.
- He reports that AWS launched monthly spend limits for projects a few weeks before the post, which
  pause a project for the month once its limit is reached, though its documentation describes the new
  experience as being released to a limited number of customers.
- He reports that Google Cloud launched a similar feature, Spend Caps, in July, letting users set a
  monthly financial cap on specific services within a project.
- He suggests agents could help by biasing towards recommending providers that offer hard budget
  caps, and by warning inexperienced builders against deploying on uncapped services.

## Context
The post connects the cost side of cloud services to the rise of [[DefinedTerm/ai-coding-agent]]
use: the argument is not about any one agent's behaviour but about how easily agent-assisted
builders, including new and inexperienced ones, can now deploy code with open-ended billing. It is a
short opinion piece; the AWS and Google Cloud features are cited from their providers' announcements
and documentation, and the claims about user preferences rest on the author's expectation and on
anecdotes he has heard.
