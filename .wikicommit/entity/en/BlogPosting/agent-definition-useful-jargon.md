---
title: "I think \"agent\" may finally have a widely enough agreed upon definition to be useful jargon now"
type: "schema:BlogPosting"
lang: en
tags: [agents, definitions, tool-use]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Sep/18/agents/'
    hash: sha256:6d9f27a63efffc1ed6b38a09e0c4427dd2728ee4c790cc63fd2321499c95670f
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The post in which Simon Willison adopts \"an LLM agent runs tools in a loop to achieve a goal\" as a definition he is willing to use without qualification, having previously avoided the term as buzzword bingo."
  author: ["Simon Willison"]
  datePublished: "2025-09-18"
---

The post is a change of position rather than a new proposal. Its author had been unwilling to use
"agent" for meaningful communication for a couple of years, on the grounds that everyone used the
word while holding different mental models of it; what the post records is noticing that he had
started using it in conversation without needing to define it, roll his eyes, or wrap it in scare
quotes. The definition he settles on — an LLM agent runs tools in a loop to achieve a goal — is
treated as its own subject under [[DefinedTerm/ai-agent]].

The argument for adopting it is about jargon rather than about agents. The post holds that a term is
useful only when both parties share its definition, and that a contested term actively reduces
clarity, since two people can spend a conversation discussing different concepts with conviction. It
positions this as an old problem, pointing to an earlier remark by Carl Hewitt that the question
"what is an agent?" embarrasses the agent-based computing community in the way "what is
intelligence?" embarrasses mainstream AI.

## Key Points

- The definition adopted is "an LLM agent runs tools in a loop to achieve a goal", with "to achieve a goal" added specifically to supply a stopping condition and rule out infinite loops.
- The "tools in a loop" half is one the post says had been popular for a while and that Anthropic in particular had settled on; the post links back to earlier writing of the author's own on that formulation.
- The post deliberately declines to require that the goal be set by a user, because sub-agent patterns already exist in which another LLM sets the goal.
- Memory is argued not to need separate inclusion: tool calls accumulate in a conversation with the model, which supplies the short-term memory a current goal requires, and long-term memory is best implemented as an extra set of tools.
- The post names "agents as replacements for human staff" as its least favourite definition and argues that category remains science fiction, because accountability — taking responsibility and learning from mistakes — is what remains unique to human staff.
- It observes that humans also have agency, forming their own goals and acting on them, which the post says AI agents cannot do despite the name.
- OpenAI is named as the single biggest source of definitional confusion, with three incompatible usages in play: the CEO's "AI systems that can do work for you independently", a "ChatGPT agent" product feature that is a browser automation system, and an Agents SDK that does fit the tools-in-a-loop idea.
- The post's stated operating rule is asymmetric: assume the tools-in-a-loop meaning when a technical implementer says "agent", but clarify which definition is in use when talking to people outside the field.

## Notes

The post mentions that the author previously collected definitions under a tag on his own site,
including crowdsourcing 211 on Twitter and using a model to group them, and reproduces a
meme — a normal-distribution "IQ bell curve" image — whose two ends both read "an LLM in a loop
with an objective", which he offers as a description of his own trajectory on the question.

The author also quotes a maxim reading "a computer can never be held accountable, therefore a
computer must never make a management decision" as summing up the accountability point.
