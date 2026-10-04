---
title: "学生よ、コーディングエージェントを使え。"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, programming-education, coding-tools]
sources:
  - type: url
    url: 'https://zenn.dev/pochipochitudoi/articles/2026-06-05-coding-agent'
    hash: sha256:f0706e89b97ac1c76d9ab100fdea618f340d4ae20d7ec9e3756802ccc01ac264
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A university student who teaches beginners in an app-development club argues that students should move from pasting code into browser chat assistants to using coding agents, sets out cautions for learners, and recommends free or low-cost agents."
  author: "あんぽぽ"
  datePublished: "2026-06-05"
  publisher: "ぽちぽちのつどい"
---

This post is written by a student for students. Its author teaches programming to incoming members of a university app-development club and observes that beginners already use AI heavily, but mostly by copying code and error messages into a browser chat assistant and pasting the answer back. The post's single message is an invitation to step beyond that copy-and-paste style and use a [[DefinedTerm/ai-coding-agent]] instead. The author notes that the post itself was written together with [[SoftwareApplication/claude-code]].

The argument rests on what the chat style cannot see: real projects span several files, follow existing conventions, and need changes verified by running them, whereas a pasted fragment gives the assistant none of that. Much of the post, though, is about how a learner should use an agent without losing the learning, followed by a list of agents a student can start with at little or no cost.

## Key Points

- The author describes a coding agent as an AI that works directly in the developer's environment — reading project files itself, editing across several files, running terminal commands, and choosing its next action from the results — as opposed to a chat assistant that sees only what is pasted into it.
- A comparison table sets the two side by side on input, file operations, command execution, multi-file edits, context and autonomy, and the author advises beginners not to worry about choosing between them: for programming, using a coding agent covers most needs.
- The most important caution, in the author's view, is not to let the agent finish an implementation the learner does not understand. Two rules are offered: ask the agent about any generated code until you can explain it yourself before moving on, or do not let it generate code at all and use it only for questions.
- Learners are told not to take output on trust, because the AI can be confidently wrong: check behaviour themselves or write simple tests, and have the agent explain why it chose an implementation.
- Because an agent rewrites files and runs commands itself, the post advises committing work with Git before important tasks and configuring the agent to ask for confirmation so the learner gets used to reading the diff.
- Learners should not give the agent passwords, personal information or API keys, and should read the terms of service, since input to free plans or models may be used for training.
- The author sums up the cautions as keeping control of the pace: the agent's capability tends to run ahead of a beginner's learning.
- The author's first recommendation for students is [[SoftwareApplication/opencode]], an open-source terminal agent, used with the free models offered through OpenCode Zen; the author judges it stronger and more generous in usage than other free agents, which can run out of quota after a few exchanges. This rests on the author's own use.
- Other free starting points listed are the free plan of [[SoftwareApplication/openai-codex]], the free plan of [[SoftwareApplication/google-antigravity]] (presented as easier for those uncomfortable with a terminal), and the free plan of [[SoftwareApplication/github-copilot]], with the caveat that the author could no longer use Copilot's free plan after a recent plan change. Paid upgrades suggested are OpenCode Go and Codex through ChatGPT Plus.

## Context

The post frames itself as one student's experience rather than a survey, and states that the services' prices, free tiers and specifications are as of June 2026 and change quickly, so readers should check official sites before relying on them. It treats free plans as adequate for trying agents out and learning, while warning that their limits and conditions are set by providers and change easily. Its closing claim is that becoming familiar with coding agents while still studying will be a significant advantage, since they are becoming standard in system development.
