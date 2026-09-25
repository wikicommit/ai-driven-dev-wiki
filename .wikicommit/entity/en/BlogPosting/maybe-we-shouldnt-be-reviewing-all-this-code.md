---
title: "Maybe We Shouldn't Be Reviewing All This Code"
type: "schema:BlogPosting"
lang: en
tags: [code-review, pair-programming, review-bottleneck]
sources:
  - type: url
    url: 'https://martinfowler.com/rachels-ramblings/code-review.html'
    hash: sha256:9de193e50154ddd76bb2ec2670e4a6cc068213b39084158e42e1d54f0de4a20a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A September 2026 post by Thoughtworks CTO Rachel Laycock arguing that the flood of AI-generated code exposes code review as having been used to solve the wrong problems. She proposes moving the judgment code review was meant to supply earlier in the process and reserving human review for exceptional changes."
  author: ["Rachel Laycock"]
  datePublished: "2026-09-02"
  publisher: "martinfowler.com"
---

Written as a response to Brian Houck of DX, with whom the author disagreed on a panel at Code Remix,
this post takes up the problem that AI now produces more code than humans can realistically review.
Houck's concern, which the author says she shares, is that automating code review away risks losing
everything else teams use it for: sharing knowledge, teaching junior engineers, building collective
ownership and spreading architectural understanding. Her counter-question is why teams wait until code
review to do any of those things.

The post argues that, rather than AI having broken code review, it has exposed how many
responsibilities were loaded onto it — quality gate, security check, architecture review, mentoring
mechanism, knowledge-sharing system and ownership model. That arrangement worked while humans could
only produce code so quickly, and the author argues the constraint is now disappearing, turning review
into a [[DefinedTerm/review-bottleneck]].

## Key Points

- Following the principle of shortening feedback loops, feedback that is valuable should not be removed
  but moved closer to the decision it informs.
- Each benefit attributed to code review has an earlier home: explore alternative solutions before
  implementing one; get knowledge transfer and let junior engineers learn by pairing; build collective
  ownership through pairing, mob programming or team design sessions; get architectural alignment by
  designing together and encoding the important constraints as fitness functions.
- Formatting, linting, known security problems and anything that can be deterministically tested should
  be automated rather than reviewed.
- Pair programming, trunk-based development, automated testing, static analysis, fitness functions and
  security scanning all move feedback earlier, and agents can increasingly take part in those loops —
  though the author holds that the real thinking still comes from experienced humans.
- Human review should happen by exception — for a fundamental architectural change, a change crossing a
  sensitive security boundary, one with a huge blast radius, an unfamiliar part of a critical system, or
  whenever the team is not confident — rather than as a ceremony applied to every change.
- If an agent can produce ten times the code but every line queues for a senior engineer, the result is
  a backlog and a new bottleneck, not a ten-times engineering organisation.
- Having an AI agent pretend to be the human reviewer only automates the ceremony instead of
  questioning why it exists.
- The author agrees with Houck that teams accumulate cognitive and intent debt as software grows while
  understanding shrinks, but does not see mandatory pull requests as a strong defence; she argues for
  deliberately maintaining understanding through collaborative design, pairing, good boundaries,
  executable architecture and shared operational responsibility — "engineers to understand systems, not
  diffs."

## Context

The post is an opinion piece in the author's personal column on martinfowler.com, written to argue one
side of a debate; she describes herself as having never particularly liked pull requests as the centre
of the development process, and presents the two sides as mostly wanting the same outcomes. The figures
it quotes on growing diff and pull-request sizes come from Houck's side of the argument, not from the
author's own measurements.
