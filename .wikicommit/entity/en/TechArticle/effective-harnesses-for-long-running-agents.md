---
title: "Effective harnesses for long-running agents"
type: "schema:TechArticle"
lang: en
tags: [agentic-coding, agent-architecture, context-engineering, agentic-loop]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
    hash: sha256:2fa27ef4cd354e98bc9fd4d6cc5bec7f182d3b5a96745c6de6f694f18541f1a6
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An Anthropic engineering post of 26 November 2025 describing a two-part harness — an initializer agent that builds the environment on the first run and a coding agent that makes incremental progress in every session afterwards — developed to let the Claude Agent SDK work across many context windows. Each of its four components is introduced as the fix for a specific observed failure mode."
  author:
    - "Justin Young"
  datePublished: "2025-11-26"
  publisher: "[[Organization/anthropic]]"
---

"Effective harnesses for long-running agents" is an engineering post published by [[Organization/anthropic]] on 26 November 2025, written by Justin Young. It reports an internal experiment in getting the Claude Agent SDK to make consistent progress on a task spanning many context windows, and accompanies a public quickstart with code examples.

The post states the core problem as discontinuity rather than capability: agents must work in discrete sessions, and each new session begins with no memory of what came before. Its analogy is a software project staffed by engineers working in shifts, where each new engineer arrives with no memory of the previous shift. Its stated position is that [[DefinedTerm/compaction]] alone does not close this gap — even a frontier coding model, which the post names as Opus 4.5, running on the Agent SDK in a loop across multiple context windows "will fall short of building a production-quality web app if it's only given a high-level prompt," the running example being "build a clone of claude.ai."

The prescription is a two-part harness: an **initializer agent** whose specialized prompt sets up the environment on the very first session, and a **coding agent** that runs every session afterwards to make incremental progress and leave structured updates. A footnote qualifies the split — the two are called separate agents only because they have different initial user prompts; the system prompt, tool set, and overall harness are otherwise identical. The post connects this to the updated Claude 4 prompting guide's recommendation of "a different prompt for the very first context window."

## Key Practices

The post organises the environment the initializer builds into three components, each introduced as the fix for a specific failure it observed.

- **A feature list, in JSON.** To stop the agent from one-shotting the app or declaring the project finished early, the initializer writes a comprehensive file of feature requirements expanding on the user's prompt — over 200 features for the claude.ai clone example, each a end-to-end description such as "a user can open a new chat, type in a query, press enter, and see an AI response," with structured `steps` and a `passes` field. All are marked failing initially, so later agents have a clear outline of what full functionality means. Coding agents are prompted to edit the file only by changing a `passes` status, reinforced with strongly-worded instructions such as "It is unacceptable to remove or edit tests because this could lead to missing or buggy functionality." The post gives a concrete reason for the file format: after experimentation they settled on JSON because "the model is less likely to inappropriately change or overwrite JSON files compared to Markdown files."
- **Incremental progress, one feature at a time.** The coding agent is asked to work on only one feature per session, which the post calls critical to addressing the agent's tendency to do too much at once.
- **A clean state at the end of every session.** The post defines "clean state" concretely as the kind of code appropriate for merging to a main branch — no major bugs, orderly and well-documented, such that a developer could begin a new feature without first clearing up an unrelated mess. The mechanism it found most effective was asking the model to commit to git with descriptive commit messages and to write progress summaries into a progress file, which also lets the model revert bad changes and recover working states.
- **End-to-end testing through browser automation.** The post reports Claude marking features complete without proper testing: it would make code changes and even run unit tests or `curl` commands against a development server, yet fail to recognise that the feature did not work end-to-end. Explicitly prompting it to use browser automation tools and test as a human user would largely fixed this, and the post credits those tools with dramatically improved performance because the agent could find bugs not obvious from the code alone. It records a stated limit: Claude cannot see browser-native alert modals through the Puppeteer MCP server, and features relying on those modals tended to be buggier as a result.

Every coding session is prompted to run a fixed orientation sequence before doing anything else: run `pwd` to see the working directory, read the git logs and progress files to catch up on recent work, and read the feature list to choose the highest-priority feature not yet done. The initializer additionally writes an `init.sh` script that starts the development server, so each session can run a basic end-to-end test before implementing anything new — in the clone example, starting the server and using the Puppeteer MCP to open a chat, send a message, and receive a response. The post's argument for this is that an agent that begins implementing a new feature on top of a broken app will only make the problem worse.

The post closes this material with a table mapping four observed failure modes to the initializer and coding-agent behaviours that address each: declaring victory too early, leaving the environment buggy or undocumented, marking features done prematurely, and spending time figuring out how to run the app.

## Scope & Caveats

The post presents itself as "one possible set of solutions" and names its own open questions. It states it is still unclear whether a single general-purpose coding agent performs best across contexts or whether a multi-agent architecture would do better, suggesting specialised testing, quality-assurance, or code-cleanup agents as plausible improvements. It also notes the demo is optimised for full-stack web app development, and offers generalising the findings to fields such as scientific research and financial modeling as future work.

The evidence is Anthropic's own internal experimentation with its own SDK and models, reported qualitatively — the post gives observed behaviours and the prompts that changed them, not measured comparisons between harness designs.
