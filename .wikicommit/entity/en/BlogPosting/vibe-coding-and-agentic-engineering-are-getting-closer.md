---
title: "Vibe coding and agentic engineering are getting closer than I'd like"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, agentic-engineering, code-review, trust]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/May/6/vibe-coding-and-agentic-engineering/'
    hash: sha256:d5efc58fb9f6c8e44c88eb246031dace67556db67152702ac3bb82b8c358bb3a
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Simon Willison's account of realising that the line he drew between vibe coding and agentic engineering has begun to blur in his own production work, because he no longer reviews every line the agents write."
  author: "[[Person/simon-willison]]"
  datePublished: "2026-05-06"
  publisher: ""
---

This post collects highlights from a podcast conversation, and centres on what the author calls a disturbing realisation: that [[DefinedTerm/vibe-coding]] and [[DefinedTerm/agentic-engineering]] have started to converge in his own work. He had staked out a firm distinction between the two — vibe coding as the mode where you are not looking at the code at all, agentic engineering as a professional practice using the same tools to the highest of one's ability — and the post is the admission that the line no longer holds where he works.

## Key Points

- **The original distinction, restated.** Vibe coding is asking for a thing, getting a thing, and if it works, great — with no attention to code quality or additional constraints. His stated view of it remains positive with a boundary: fantastic for a personal tool where a bug hurts only you, "grossly irresponsible" for software built for other people, because other people are hurt by your bugs.
- **What changed.** As coding agents became more reliable he stopped reviewing every line, "even for my production level stuff." His example is that a JSON API endpoint running a SQL query is something Claude Code will simply get right, with tests and documentation added, and he does not read the result.
- **The analogy he uses to make peace with it** is the internal-dependency one: as an engineering manager he would not read every line another team wrote for, say, an image-resize service — he would read their documentation, use it, ship his own features, and only dig into their repository if problems appeared. He treats agents the same way, as a semi-black box he does not look at until he needs to.
- **Why the analogy is uncomfortable.** "Claude Code does not have a professional reputation!" A human team can build one and is accountable for what it does; an agent cannot take accountability. What he has instead is a track record of the model churning out straightforward things correctly in the style he likes.
- **The named risk** is the normalization of deviance: every time a model turns out to have written the right code unmonitored, there is a risk of trusting it at the wrong moment later and getting burned.
- **Evaluating software has become harder.** A repository with a hundred commits, a good readme and comprehensive tests used to signal care and attention; he can now produce one in half an hour that looks identical. His substitute signal is usage — a vibe-coded thing someone has used daily for two weeks is worth more to him than something spat out and barely exercised. The enterprise form of the same rule: he would not want a CRM unless two other large enterprises had run it successfully for six months.
- **The lifecycle was built for a slower rate.** Going from 200 to 2,000 lines of code a day breaks things upstream as well as downstream: he relays a design leader's argument that heavy design process exists because getting the design wrong used to cost three months of engineering, and that if building no longer takes three months the design process can afford to be riskier.
- **Why he is not afraid for his career**: the tools are amplifiers of existing experience, his conversations with agents are "moon language" to most people, and producing software remains ferociously difficult regardless of tooling. He quotes a commentator's line that he would rather professionally managed software companies use AI to make better products than vibe code himself, and compares it to preferring to hire a plumber over watching enough YouTube.

## Context

This is a personal reflection assembled from podcast remarks, and it is explicit about that framing — the author notes that podcasts sometimes push him to think out loud in a way that surfaces an idea he had not previously put into words. Its value is as a firsthand record of a boundary eroding in practice, from the person who drew that boundary, rather than as a general claim about how anyone else should work.
