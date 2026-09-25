---
title: "Vibe engineering"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, software-engineering, agentic-engineering, code-review]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Oct/7/vibe-engineering/'
    hash: sha256:5442c0b9be9f6a384ae08f68ce1ee4fcc793a8181cdfd7bddcfe9e6fadde6b4d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A post proposing the name \"vibe engineering\" for experienced engineers accelerating their work with LLMs and coding agents while staying accountable for the result, and arguing that these tools reward existing senior-level engineering practices."
  author: ["Simon Willison"]
  datePublished: "2025-10-07"
---

The post starts from a terminology gap. Its author takes [[DefinedTerm/vibe-coding]] to be well
established as the name for the fast, loose and irresponsible way of building software with AI —
entirely prompt-driven, with no attention to how the code works — and asks what to call the other
end of the spectrum, where seasoned professionals accelerate their work with LLMs while remaining
proudly and confidently accountable for the software they produce. He proposes
[[DefinedTerm/vibe-engineering]], "with my tongue only partially in my cheek".

Most of the post argues that this other end is hard and rewards existing expertise. The author
points to the rise of coding agents — tools such as [[SoftwareApplication/claude-code]], OpenAI's
Codex CLI and [[SoftwareApplication/gemini-cli]] that iterate on code, testing and modifying it
until it reaches a specified goal — and to experienced engineers running several agents in parallel,
which he says he now does himself (see [[BlogPosting/embracing-the-parallel-coding-agent-lifestyle]]).
He contrasts iterating with agents towards production-quality code he can maintain with classic vibe
coding, in which he outsources a simple, low-stakes task and accepts the result if it appears to work.

A later update to the post, dated 23 February 2026, says the term "agentic engineering" appears to be
winning out for this idea (see [[DefinedTerm/agentic-engineering]]).

## Key Points

- There is a terminology gap between vibe coding and responsible, professional use of LLMs for software, and the author proposes "vibe engineering" to fill it.
- Working productively with LLMs on non-toy projects is described as difficult: the tools have depth, there are traps to avoid, and the speed at which they produce working code raises the bar for what the human should contribute.
- According to the author, LLMs actively reward existing top-tier software engineering practices: automated testing (test-first development being particularly effective with agents that iterate in a loop), planning in advance, comprehensive documentation, good version control habits, effective automation such as CI, formatting, linting and preview deployments, and a culture of code review.
- He also lists skills he considers necessary: a "very weird form of management" of agents that resembles managing human collaborators, strong manual QA, research skills, the ability to ship to a preview environment, an instinct for what can be outsourced to AI, and an updated sense of estimation.
- The engineer's role expands to researching approaches, deciding architecture, writing specifications, defining success criteria, [[DefinedTerm/designing-agentic-loops]], planning QA and spending much more time on code review.
- The post's conclusion is that AI tools amplify existing expertise: the more skill and experience an engineer has, the faster and better their results with LLMs and coding agents.
- The name is chosen deliberately: the author calls it cheeky and likely to be controversial, says he wants to reclaim "vibes" for something more constructive, and values the self-contradiction between "vibes" and "engineering" as what may make it stick.

These points are the author's own view, grounded in his experience; the post presents no measured results.

## Context

The author notes that almost all of the practices he lists are already characteristics of senior
software engineers, and says he has disliked the distinction between "coders" and "engineers" as
gatekeeping — but that here "a bit of gatekeeping is exactly what we need". He also records having
tried earlier, with approximately zero success, to make terms such as
[[DefinedTerm/ai-assisted-programming]] stick.
