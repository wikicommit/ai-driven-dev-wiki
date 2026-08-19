---
title: "Vibe engineering"
type: "schema:BlogPosting"
lang: en
tags: [ai-assisted-programming, terminology, agentic-coding]
sources:
  - type: url
    url: 'https://simonw.substack.com/p/vibe-engineering'
    hash: sha256:ef207bce62b3ace1d79b606bd1e4f06b56960f2525d3a90b75215d9f9c381aa2
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The newsletter issue in which Simon Willison proposes [[DefinedTerm/vibe-engineering]] for the accountable end of the AI-assisted programming spectrum, and lists the existing engineering practices he argues LLMs reward."
  author:
    - "[[Person/simon-willison]]"
  datePublished: "2025-10-08"
  publisher: ""
---

"Vibe engineering" is an issue of Simon Willison's Newsletter dated 8 October 2025, whose lead item republishes his post of 2025-10-07 proposing the term [[DefinedTerm/vibe-engineering]]. Willison's starting point is a terminology gap: he treats [[DefinedTerm/vibe-coding]] as well established for "the fast, loose and irresponsible way of building software with AI," entirely prompt-driven with no attention paid to how the code works, which leaves no name for the opposite end — seasoned professionals accelerating their work with LLMs while staying accountable for what they ship.

The bulk of the item is a list of established software engineering practices Willison argues LLMs actively reward, followed by a short defence of the name itself. His framing throughout is that this way of working is *difficult*, and that the pace at which agents produce working code raises rather than lowers the bar for the human participant.

The remainder of the newsletter issue is unrelated link-blogging — OpenAI DevDay coverage, model releases, and a Python release — and is not part of the vibe engineering argument.

## Key Points

- **Coding agents are what changed.** Willison credits the rise of coding agents — naming Claude Code (released February 2025), OpenAI's Codex CLI (April) and Gemini CLI (June) as tools that iterate on code, actively testing and modifying it until it achieves a specified goal — with dramatically increasing the usefulness of LLMs for real-world problems. See [[DefinedTerm/coding-agent]].
- **Running several agents at once.** He reports hearing from experienced engineers running multiple copies of agents in parallel, says he was skeptical at first, and states he has started doing it himself: "surprisingly effective, if mentally exhausting."
- **The practices LLMs reward.** Automated testing (an agent without tests may claim something works without having tested it); planning in advance; comprehensive documentation, which lets a model use APIs it has not read the code for; good version control habits, with LLMs described as "fiercely competent at Git"; effective automation such as CI, formatting, linting, and preview deployments; a culture of code review; "a very weird form of management"; strong manual QA; strong research skills; the ability to ship to a preview environment; an instinct for what can be outsourced to AI; and an updated sense of estimation, which he says AI makes harder rather than easier.
- **Amplification, not replacement.** Willison's summary claim is that AI tools amplify existing expertise — the more skills and experience an engineer has, the faster and better the results — and that almost all the listed characteristics are already those of senior engineers.
- **A deliberately cheeky name.** He concedes it is probably a stupid name, says "vibes" as an AI concept feels tired, and argues that a bit of gatekeeping is exactly what is needed here to signal a harder and more sophisticated way of working. He notes he previously tried to make "AI-assisted programming" stick with approximately zero success, and likes the self-contradiction between "vibes" and "engineering" as something sticky.

## Context

The post is a direct sequel to Willison's earlier insistence that vibe coding means abandoning engagement with the code, a position covered in [[BlogPosting/not-vibe-coding]]. Naming the disciplined counterpart is his way of resolving the terminology pressure that position creates: if reviewing and understanding the code is not vibe coding, the practice still needs a name.

Willison marks the whole space as unsettled — "this whole space is still absurd in all sorts of different ways" — and presents the term as a proposal rather than a settled definition. The post notes it was discussed on Hacker News and lobste.rs.
