---
title: "system reminders"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05344'
    hash: sha256:29a5dfd46c7505affc599f6922ebba2f67d01e7f3a343df5347a42f435a08edc
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Short, single-purpose messages injected into an agent's conversation at the moment of a decision, rather than stated once upfront in the system prompt, to counteract the attention decay that causes long-running agents to quietly stop following their original instructions."
---

System reminders are short, single-purpose messages injected into an agent's conversation exactly when the agent needs them — immediately before the decision point where it would otherwise go wrong. [[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] introduces them to address a reliability problem in long-running sessions: as the conversation grows, the model's attention drifts away from the initial system-prompt instructions, producing silent failures such as premature task completion, abandoned error recovery, and unchecked exploration spirals.

## Usage

The report describes the root cause plainly. The system prompt sits at the very beginning of the conversation; as the conversation grows longer, the model's attention shifts toward recent messages and away from that initial block. The rules are still present in the context window, but their influence fades with distance. The author characterizes this as a predictable, reproducible failure mode observed consistently in sessions exceeding 15 tool calls — for example, an agent told to always run tests after editing code does so for the first few turns, then quietly stops once file contents, search results, and command outputs have piled up.

Two naive alternatives are rejected: putting all instructions up front works initially but degrades over long sessions, while re-injecting the entire system prompt every few turns wastes tokens on instructions the agent does not currently need.

In the documented implementation, event detectors monitor a set of conditions at the boundary between tool execution and the next model call — including tool failure without retry, exploration spirals after several consecutive reads, denied tool re-attempts, premature completion with incomplete task items, plan approval without follow-through, unprocessed subagent results, and empty completion messages. When a detector fires, the corresponding reminder template is resolved from a catalog organized into categories covering phase control, task lifecycle, todo enforcement, error recovery, behavioral correction, and parse retries. All reminder text lives outside source code in plain-text templates, which the report notes makes them auditable and editable without touching program code.

Two design details are emphasized as consequential.

**Reminders are injected with a user role, not a system role.** The stated reasoning is that after dozens of turns another system message blends into the background the model has already partially forgotten, whereas a user message appears at the position of highest recency and is treated as something that just happened and requires a response. The report states that early experiments with system-role injection confirmed this, with user-role reminders producing noticeably higher compliance rates.

**Frequency must be capped per reminder type.** A reminder that fires on every iteration stops being helpful and becomes noise the model learns to ignore, so each type is governed by a counter or a one-shot flag — incomplete-task nudges fire at most twice, error-recovery nudges at most three times, and certain signals exactly once. If the agent does not respond to a capped nudge, the system accepts the agent's judgment and moves on rather than looping. The report records that before these guards existed, some reminders fired on every iteration and caused the agent to loop on the nudge itself.

The mechanism is designed to degrade gracefully: if a reminder template is missing or retrieval fails, the agent still has its system prompt, because reminders reinforce existing instructions rather than introducing new ones.

A closely related mechanism the report describes is context-injected error recovery, which classifies a failed tool call into one of six categories and injects a targeted recovery template. The stated rationale is the same — specificity is what makes guidance actionable, so "the file has changed since you last read it; re-read the file and retry your edit with the current content" outperforms a generic instruction to try again.

## Related Terms

System reminders are one of the mechanisms grouped under [[DefinedTerm/context-engineering]] and coordinated by the [[DefinedTerm/agent-harness]] at runtime. The report frames them as the "dynamic just-in-time" tier of a three-tier context architecture, sitting between the static system prompt and long-horizon persistent memory.
