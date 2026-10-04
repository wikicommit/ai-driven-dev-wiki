---
title: "Vibe coding – Was nun?"
type: "schema:BlogPosting"
lang: en
tags: [ai-assisted-programming, agentic-coding, prototyping, code-quality]
sources:
  - type: url
    url: 'https://www.codecentric.de/wissens-hub/blog/vibe-coding-was-nun'
    hash: sha256:70cefba72a447488040405c4b7a7af3c3f7095bf18585232db3eed1169522ba1
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A German-language codecentric blog post from April 2025 that looks past the hype around vibe coding, weighs the strengths and weaknesses of generative AI in software development, and concludes that vibe coding suits prototypes, idea generation and small well-specified modules but not applications put into production."
  author: ["Goetz Markgraf"]
  datePublished: "2025-04-12"
  publisher: "codecentric"
---

This post on codecentric's German-language blog ("Vibe coding – what now?"), by Goetz Markgraf, asks whether AI really lets people build applications without being able to code, with a fraction of the effort and time, as social-media posts were claiming. It explains that the term [[DefinedTerm/vibe-coding]] was coined by Andrej Karpathy in a tweet in early February 2025, describing it as not caring about the code, using only AI-supported tools, always accepting the AI's suggestions and passing error messages straight back to the AI to fix.

The post draws a boundary around the term: not every use of generative AI is vibe coding. Someone who uses Copilot, ChatGPT, Claude, Cursor or Windsurf as one tool among many to write, change or understand code is not a "vibe coder"; the term refers only to a way of working in which one does not, or barely, look at the generated code. Drawing on more than a year of client projects with GitHub Copilot, his own experiments with agentic tools and exchanges with colleagues, the author then weighs what AI-supported development can and cannot yet do.

## Key Points

- The next generation of AI tools, the post says, are agent systems that use AI to make a plan which is then worked through step by step by classic tools and AI; it names [[SoftwareApplication/cursor]], [[SoftwareApplication/windsurf]], V0 and, more recently, the agent mode of [[SoftwareApplication/github-copilot]]. Such tools can read code, look up architecture agreements, create or change code, fix compile errors and write and run tests — taking minutes and many paid tokens, but delivering much better results than a plain chat.
- The author personally expects the quality of the underlying models not to rise much further in the near future, but the quality of agents that combine AI with classic automation to do so.
- Strengths of generative AI in software development, as the author and his colleagues observe them: taking over repetitive tasks such as filling data structures, mappings and scaffolding; access to already-solved problems, often faster and better tailored than a search engine or Stack Overflow when the AI can see the codebase; occasionally creative solutions one would not have thought of; and building individual modules or functions that can be described simply and completely.
- Weaknesses, which the post says apply to agent systems too: mastering complexity as software grows, partly offset by larger contexts and project files such as coding guidelines; ensuring correct behaviour, since the AI does not understand what it does and cannot fully prevent side effects; non-deterministic output, so similar components end up structured differently and drift apart under repeated changes; maintainability, with AI-generated code increasingly noticeably harder to maintain than code that went through a proper four-eyes review; and quality requirements such as operational safety, IT security and resource use, which much of the code the AI learned from — largely tutorials — does not address.
- That last weakness becomes critical, the author argues, when someone without IT knowledge puts such a solution online, giving attackers easy access to insecure systems.
- His overall assessment: AI can produce certain code very quickly and efficiently, its solutions are sometimes surprisingly good and creative, and the tools are fun once learned — but in large applications one quickly reaches limits where the AI helps little or does harm, and almost nobody would take its code into production unchanged; it has to be reviewed more critically than a colleague's.
- Karpathy is not wrong, the post argues, because most people overlook a sentence in his tweet: "It's not too bad for throwaway weekend projects, but still quite amusing." He described vibe coding as a method for throwaway weekend projects, not for productive use.
- With its risks in mind, the author sees professional uses in rapid prototyping (sample applications for user tests or for showing stakeholders tangible approaches, not for production), generating ideas in the discovery phase, and creating individual code blocks and modules that can be fully described in a few sentences, provided they are checked thoroughly.
- On claims that AI makes developers superfluous, the post suggests asking who makes them and why — tool vendors, management justifying staff cuts, business departments in a hurry, or beginners hoping to shorten the learning curve — and says the author has not heard such a claim from an experienced developer.

## Context

The post is an early (April 2025) practitioner's response to the term, written from the perspective of a consultancy that builds large applications for clients, and its assessments are explicitly the author's own, based on his and his colleagues' experience rather than measurement. It closes by agreeing with Karpathy that vibe coding can be an exciting and fun weekend pastime and, in small doses, useful professionally, but says the author would never put an application built that way live.
