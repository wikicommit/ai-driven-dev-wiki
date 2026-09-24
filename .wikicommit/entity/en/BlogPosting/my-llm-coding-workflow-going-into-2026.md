---
title: "My LLM coding workflow going into 2026"
type: "schema:BlogPosting"
lang: en
tags: [ai-assisted-programming, coding-agents, spec-driven-development]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/ai-coding-workflow/'
    hash: sha256:bb23e1f299d66f8dc6e402e687b71bed11c3c380f0544deff076220a9c992780
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Addy Osmani's account of how he plans, codes and collaborates with LLMs going into 2026 — spec and plan first, small iterative chunks, rich context, supervised agents, thorough testing and review, frequent commits, rules files and CI — arguing that classic engineering discipline matters more, not less, when AI writes much of the code."
  author: ["Addy Osmani"]
  datePublished: "2026-01-04"
---

In this post Addy Osmani describes the workflow he has converged on for coding with LLMs over a year of projects, and distils it into a set of lessons. He calls the approach a more disciplined "AI-assisted engineering": using AI aggressively while staying accountable for the software produced. Its premise is that coding with LLMs is not push-button magic — getting good results means learning new patterns — and that the model is best treated as a powerful pair programmer that needs clear direction, context and oversight rather than as an autonomous decision-maker.

The lessons run from planning to review: begin with a spec and a plan, work in small increments, give the model all the context it needs, pick models deliberately, use coding agents under supervision, test and review everything, commit often, tune the model with rules and examples, and surround it with automation. The post closes by describing its approach as "AI-augmented software engineering" rather than AI-automated software engineering, with the human engineer remaining "the director of the show".

## Key Points

- It recommends starting with a detailed specification brainstormed with the AI — having the model ask questions until requirements and edge cases are fleshed out — compiled into a spec.md, then having a reasoning model turn it into a step-by-step project plan before any code is written.
- It argues for breaking work into small, iterative chunks, implementing one plan step at a time and testing each, because asking for large monolithic output tends to produce inconsistent, duplicated code.
- It stresses packing in context — relevant code, API documentation, constraints and approaches to avoid — and mentions tools that bundle a codebase into a text file for the model, while telling the model explicitly what is out of scope.
- It describes Claude Skills as promising because they package instructions, scripts and domain expertise into reusable capabilities that tools apply automatically, replacing fragile repeated prompting.
- It advises choosing the model best suited to each task and switching to another model when one gets stuck, sometimes running two in parallel to cross-check. The author discloses that he prefers Gemini partly because he worked on it at Google.
- It describes CLI coding agents (naming Claude Code, OpenAI's Codex CLI and Gemini CLI) and asynchronous agents that work in a cloud VM and open a pull request (naming Google's Jules and GitHub's Copilot Agent), and says it uses them in a supervised way rather than letting an agent build a whole feature unattended.
- Its central rule is never to trust LLM output blindly: every AI-generated snippet is read, run and tested as if a junior developer had written it, and the author says he merges or ships code only after he has understood it.
- It argues that agents work best on codebases with strong test suites, since a tight write–test–fix loop depends on tests existing, and recommends AI-assisted review as well — for example having a second model critique code written by the first.
- It describes using [[SoftwareApplication/chrome-devtools-mcp]] in the author's debugging and quality loop to give the agent access to what the browser sees at runtime.
- It recommends ultra-granular commits as "save points", so an AI misstep can be rolled back and the history can brief the model, and running separate AI sessions in parallel in their own [[DefinedTerm/git-worktrees]].
- It recommends steering the model with a rules file such as a CLAUDE.md or GEMINI.md, custom instructions, and in-line examples of the style wanted.
- It treats CI, linters, type checkers and code-review bots as force multipliers, feeding their failures back to the model so that automated checks keep AI output honest.
- It argues that AI amplifies existing expertise: those with solid fundamentals gain productivity, while those without may just amplify confusion, and it suggests periodically coding without AI to keep skills sharp.

## Context

The recommendations rest mainly on the author's own experience, supplemented by other practitioners' published accounts, which the post quotes or links throughout. Its spec-first planning is close to [[DefinedTerm/spec-driven-development]], and the post links to the author's earlier writing on vibe coding and on asynchronous coding agents. It ends by pointing to his O'Reilly book on AI-assisted engineering, [[Book/beyond-vibe-coding]].
