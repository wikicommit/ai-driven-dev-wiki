---
title: "Outer Loop"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/own-the-outer-loop/'
    hash: sha256:4945c6720401f08dd3c43a7ec8fd0b79a1c8eb6f08bfa4b0da49f6e4a0c6173a
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/how-to-build-reliable-ai-workflows-with-agentic-primitives-and-context-engineering/'
    hash: sha256:f4175892bf17116173c4ae2a309b3b81b227800f09d53afa3ad1ade536e02a2d
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A term this wiki's sources use two ways against the same inner/outer pairing. In Addy Osmani's 'Own the Outer Loop' keynote it is the part of an agentic engineering workflow a human retains ownership of, while an agent runs the inner loop of investigating, implementing and verifying. In a GitHub blog guide it is instead an execution environment — running agent instruction files from a CLI runtime and in CI/CD, as against interactive work in the editor — with no claim about who owns which."
---

In his "Own the Outer Loop" keynote, Addy Osmani frames the outer loop as the part of an agentic coding workflow that a human retains ownership of, distinguished from the "inner loop" that a coding agent runs on its own: investigating a task, implementing a plan, and verifying the result. Where the inner loop is a matter of capability — what a model plus its harness can do — the outer loop is a matter of agency: deciding what should be built, verifying that it was built safely, approving it, and owning the outcome. The claim is that agents have moved from assisting inside the inner loop to running the entire inner loop themselves, which is what makes owning the outer loop the part of the work that is left for engineers.

A second source uses the same inner/outer pairing for something else, and the two do not reduce to
one another. [[BlogPosting/how-to-build-reliable-ai-workflows-with-agentic-primitives-and-context-engineering]]
draws the line between *where work runs* rather than between who is responsible for it: the inner
loop is interactive development, testing and workflow refinement in VS Code with GitHub Copilot,
and the outer loop is agent CLI runtimes providing reproducible execution, CI/CD integration and
production deployment. Its summary advice is to use the inner loop for rapid interactive work and
the outer loop for reliable, repeatable automation. Nothing in that account assigns the outer loop
to a human; on the contrary, its outer loop is the more automated of the two, which is the reverse
of the sense above. A reader meeting the term should establish which pairing a source means before
carrying any claim across.

## Usage

Osmani organizes the outer loop around three terms he names in the keynote: Quality, the checks installed before a system is allowed to run, which produce evidence; Verdict, the production decision made from that evidence — ship, block, redirect, narrow the response, add a guardrail, or reject outright; and Answerability, the guarantee that the person who made the Verdict can explain it if asked. He frames the human's role as not needing to be inside the inner loop to hold the outer loop, occupying instead four narrower loops he names: the constraints loop (what inputs, architectures, instructions, or invariants to set), the sampling loop (how much output to sample and review), the audit loop (what evidence to keep and whether the audit log is effective), and the ownership loop (which part of the production boundary a given person owns).

## When It Applies

It applies once agents are trusted to run the inner loop unattended, at a scale or speed a human could not review turn by turn — the post cites survey evidence that a large and growing share of committed code is AI-generated or AI-assisted, and separate research showing that review and governance have become the bottleneck, typically arriving only after code has already been created and the risk already accepted. It assumes a back-pressure mechanism — ordinary engineering signals such as type checks, tests, hooks, sandbox limits, audit logs, and monitors — that constrains how much autonomy an agent is actually granted, deliberately less than the maximum autonomy it could exercise. Skipping it is described as producing three hidden costs: cognitive surrender, cognitive debt, and the orchestration tax.

In the execution-environment sense, what the outer loop requires is different again: an agent CLI
runtime that can execute an instruction file outside the editor, and files portable enough to run
unchanged in either place. That account describes the transition as turning IDE-bound files into
independently executable workflows, and names command-line execution, CI/CD integration,
environment consistency and native MCP server support as what the runtimes supply. It reports no
evaluation of this arrangement.

## Related Terms

- [[DefinedTerm/agent-primitives]] — the files the execution-environment sense runs in either loop

[[DefinedTerm/loop-engineering]], [[DefinedTerm/harness-engineering]], [[DefinedTerm/cognitive-surrender]], [[DefinedTerm/cognitive-debt]], [[DefinedTerm/orchestration-tax]]
