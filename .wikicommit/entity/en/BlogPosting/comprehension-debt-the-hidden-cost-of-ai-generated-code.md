---
title: "Comprehension Debt - the hidden cost of AI generated code."
type: "schema:BlogPosting"
lang: en
tags: [code-review, ai-assisted-programming, human-oversight, verification]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/comprehension-debt/'
    hash: sha256:da802296819d229a36cbb9502e0af206d1b18ce700c94403b60734702be8a1e8
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A March 2026 post naming the growing gap between how much code exists in a system and how much of it any human genuinely understands, arguing that tests and specs each have a hard ceiling as substitutes for that understanding, and that nothing in conventional delivery metrics captures the deficit."
  author: ["Addy Osmani"]
  datePublished: "2026-03-14"
---

This post defines [[DefinedTerm/cognitive-debt]] — which it calls comprehension debt — as the
growing gap between how much code exists in a system and how much of it any human being genuinely
understands. Its central contrast is with technical debt: technical debt announces itself through
mounting friction, while comprehension debt breeds false confidence, because the codebase looks
clean and the tests are green right up until the reckoning arrives.

The mechanism the post gives is a speed asymmetry. Human review of a colleague's pull request was
always a bottleneck, but a productive one — it forced comprehension, surfaced hidden assumptions and
distributed knowledge across the people responsible for maintaining the system. AI-generated code
breaks that loop by volume, and its output carries exactly the surface signals that historically
triggered merge confidence. Osmani states the inversion sharply: when code was expensive to produce,
senior engineers could review faster than junior engineers could write; AI flips that, so a junior
engineer can now generate code faster than a senior engineer can critically audit it, turning what
was a quality gate into a throughput problem.

Most of the post is spent on why the obvious remedies do not close the gap. Tests are necessary but
not sufficient; specs are appealing but incomplete; and the measurement systems organisations
already run cannot see the deficit at all. Its conclusion is that making code cheap to generate does
not make understanding cheap to skip, and that the comprehension work is the job.

## Key Points

- The post defines comprehension debt as the growing gap between how much code exists in a system and how much of it any human genuinely understands, and argues it is more insidious than technical debt because technical debt is usually a conscious tradeoff with a known location while comprehension debt accumulates invisibly.
- Its stated mechanism is a speed asymmetry: AI generates code far faster than humans can evaluate it, and the rate-limiting factor that used to keep review meaningful — that writing was slower than reviewing — has been removed.
- Osmani argues that surface correctness is not systemic correctness: AI output that is syntactically clean and well-formatted triggers merge confidence while comprehension hollows out underneath.
- On tests, the post's claim is that a suite covering all observable behaviour would often be more complex than the code it validates, and that you cannot write a test for behaviour you never thought to specify — so tests are necessary but not sufficient.
- It names a specific failure mode: when an AI changes implementation behaviour and updates hundreds of test cases to match, the question becomes whether those test changes were necessary and whether coverage catches what the reviewer is not thinking about, which the post says only comprehension can answer.
- On specs, it argues that translating a spec into working code involves many implicit decisions no spec fully captures, that two engineers implementing the same spec produce observably different systems, and that a spec detailed enough to fully describe a program is more or less the program in a non-executable language.
- The post claims a measurement gap: velocity metrics, DORA metrics, PR counts and coverage can all look healthy while comprehension deficits stay invisible, so incentive structures optimise correctly for what they measure and what they measure no longer captures what matters.
- It argues the organisational assumption that reviewed code is understood code no longer holds, and that liability has been distributed without anyone noticing.
- Osmani predicts a regulation horizon: once AI-generated code runs in healthcare, financial infrastructure and government services, "the AI wrote it and we didn't fully review it" will not survive a post-incident report.
- Its stated redistribution is that as AI volume rises, the engineer who genuinely understands the system becomes more valuable rather than less, and that ability becomes the scarce resource the whole system depends on.

## Context

The post positions itself against several other accounts rather than standing alone. It cites an
Anthropic randomized controlled trial of 52 software engineers learning a new library in which the
group using AI assistance finished in roughly the same time as the control group but scored 17
percentage points lower on a follow-up comprehension quiz, 50% against 67%, with the largest
declines in debugging; the post's emphasis is on the researchers' point that passive delegation
("just make it work") impairs skill development far more than active, question-driven use. It also
reports research indicating that developers who use AI for code-generation delegation score below
40% on comprehension tests while those using it for conceptual inquiry score above 65%, which it
summarises as the tool not destroying understanding — how it is used does. Osmani credits
Margaret-Anne Storey with the account of a student team that could no longer make simple changes
without breaking something by week seven, where the problem was that nobody could explain why design
decisions had been made rather than that the code was messy.

Its closing argument is historical rather than technical: decades of managing software quality
across distributed teams produced practices that do not evaporate because the team member is now a
model. What AI changes, on the post's account, is cost, speed and interpersonal management overhead;
what it does not change is the need for someone with deep system context to hold a coherent
understanding of what the codebase does and why.
