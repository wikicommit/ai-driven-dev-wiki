---
title: "AgentClick: A Skill-Based Human-in-the-Loop Review Layer for Terminal AI Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, human-oversight, agent-skills]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.16520'
    hash: sha256:2601c1408563f747b2ac732af43342b6d4d14231aace9b4a2e0aa4d33ba3f674
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A demo paper presenting AgentClick, a browser-based review layer that attaches to existing terminal AI agents through Markdown skills and replaces raw terminal output with task-specific interfaces for reviewing and editing an agent's proposed emails, plans, code changes, memory and execution traces."
  author: ["Haomin Zhuang", "Hanwen Xing", "Xiangliang Zhang"]
  datePublished: "2026"
  keywords: ["human-in-the-loop", "AI agents", "agent skills", "terminal agents", "review interfaces"]
---

This demo paper argues that although autonomous agents such as [[SoftwareApplication/openai-codex]] and [[SoftwareApplication/claude-code]] make it practical to delegate consequential work, the interfaces through which people supervise that work have not kept up. The authors identify three specific problems with terminal-based and chat-relayed interaction: terminal output interleaves reasoning traces, tool logs and proposed actions in a single stream so it is hard to see what actually requires review; feedback is cumbersome because users must type free-form corrections even for small local edits; and consequential actions are surfaced as opaque events or binary prompts, leaving no room for targeted inspection. They argue these barriers fall hardest on non-expert users and become sharper when agents run on remote or headless infrastructure where the terminal is not merely a poor medium but often an inaccessible one.

Their response is [[SoftwareApplication/agentclick]], a review layer built around four components — human, browser, backend and agent. Rather than acting immediately, the agent submits proposals to a backend that maintains session state, serves a browser interface over HTTP, records edits and returns approval or correction signals. The paper's central design claim is that different agent outputs require different review affordances, so instead of one generic approval dialog the system provides interfaces matched to the structure of each artifact: an inbox and paragraph-level editing for email, typed step cards for plans, expandable diffs with per-hunk approval for code, explicit listings for memory, and a structured view of tool calls and retries for trajectories.

Integration is handled through what the authors call a hierarchical skill design: the agent consumes a set of Markdown skills rather than an SDK, with a main skill that bootstraps the server and dispatches to sub-skills that define each domain's payload schema and review actions. The authors present this as the mechanism that makes the layer portable — any agent able to read and follow Markdown instructions can adopt it without modification to its codebase.

## Key Points

- The system is positioned as improving collaboration rather than merely gating execution: users can approve, edit directly, delete content, adjust constraints or request a targeted rewrite, which the authors argue matters most when output is mostly correct but needs localized changes.
- Skills are chosen over a dedicated SDK on two stated grounds — they require no instrumentation of the agent's codebase and add no runtime dependencies, and they are portable to any agent that can follow Markdown instructions.
- The memory interface is motivated by context compaction specifically: the authors observe that when a session grows long the agent summarizes and clears the conversation, but the resulting summary often omits content the user needs, and anything that should persist must be manually reloaded by locating a file in the project tree. AgentClick surfaces the generated summary for review and editing before it is saved.
- Trajectory inspection is framed as an active oversight channel rather than post-hoc debugging: users can annotate specific steps with guidance that is saved to memory and used on similar tasks later.
- Preference capture works through reason-tagged edits — when a user edits or deletes part of an artifact and gives an explicit reason, the system records it to a structured memory file the agent reads in future runs.
- Remote review is demonstrated by running an agent under [[SoftwareApplication/openclaw]] on a server exposed through a tunnel, with the user reviewing and editing an email draft from a mobile browser before the server-side agent dispatched it.
- In a plan-review walkthrough the terminal surfaced a framework choice as a multiple-choice prompt with no visibility into downstream steps, while the same plan appeared in the browser as step cards covering the full pipeline, into which the user injected two constraints before execution began.
- An email walkthrough reports that after the user requested a lighter style with emoji and gave that as an explicit reason, the agent adopted the preference automatically on the next email without the instruction being restated.

## Notes

The authors are explicit about the limits of their evaluation. They evaluate through the lens of human-agent collaboration rather than autonomous task completion, and state plainly that the three walkthroughs are capability-oriented illustrations rather than a formal controlled user study; the capability table that summarizes them records which capabilities each walkthrough exercised, not measured outcomes. They release the codebase and demo scripts to let others verify and extend the workflows.

The paper situates itself against three lines of prior work. It distinguishes itself from human-in-the-loop agent systems by aiming at a lighter-weight layer deployable over existing terminal agents with explicit preference capture; from remote-access and terminal-forwarding interfaces by providing task-specific artifact interfaces rather than exposing a chat or terminal view; and from debugging and execution platforms by attaching to existing agents and intervening before or during execution rather than re-hosting them or analysing traces afterwards.
