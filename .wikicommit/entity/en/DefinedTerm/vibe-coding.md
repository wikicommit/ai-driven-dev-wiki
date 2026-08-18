---
title: "vibe coding"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/May/1/not-vibe-coding/'
    hash: sha256:4c658c9b0548d2a1a6e3cabefbb4299d17ce794ac693027d0c788262d01d7166
review_status: pending
generated_at: "2026-08-18"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Generating code with AI without caring about the code that is produced. Coined by Andrej Karpathy in February 2025 for a way of working in which the developer stops reading the generated code; Simon Willison argues the term is being applied to AI-assisted programming in general, a reading he says is wrong."
---

Vibe coding is generating code with AI without caring about the code that is produced. [[Person/andrej-karpathy]] coined the term on 6 February 2025, describing "a new kind of coding" in which you "fully give in to the vibes, embrace exponentials, and forget that the code even exists" — accepting every suggestion without reading the diffs, pasting error messages back in with no comment, letting the code grow beyond your own comprehension, and working around bugs the model cannot fix by asking for random changes until they go away. Karpathy attributed its feasibility to LLMs getting "too good", and framed it as something that is "not too bad for throwaway weekend projects" rather than as a method for building production software.

## Usage

[[Person/simon-willison]] argues in [[BlogPosting/not-vibe-coding]] that the term is being applied to AI-assisted programming in general, a reading he says is wrong, and that the distinction is not which tools are used but whether the developer engages with the generated code at all: using LLM tools as part of a process for responsibly building production code, on his account, is not vibe coding. He cites two forthcoming books, [[Book/vibe-coding]] and [[Book/vibe-coding-the-future-of-programming]], as titles that adopt the term while describing the professional workflow it was explicitly not about.

Willison also argues the term names an audience rather than a tool: people who are not software developers and do not want to become developers, but who now have a path to building custom software for themselves. He frames the open questions for that audience as which kinds of project can be built this way, and how to handle security, privacy, reliability and the risk of over-spending.

## Related Terms

Willison attributes the broadening of the term's meaning to [[DefinedTerm/semantic-diffusion]], which he describes as an unstoppable force.
