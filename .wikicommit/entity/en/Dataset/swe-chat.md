---
title: "SWE-chat"
type: "schema:Dataset"
lang: en
tags: [agents, coding-tools]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.29442'
    hash: sha256:4f54dee1b64331647df773370db022f7f472348a7dbcf5f522b760058dfbf607
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A corpus of CLI coding-agent sessions collected from developers on GitHub who opted into public checkpoint logging, contributing 5,785 sessions across 198 repositories."
  variableMeasured: ["user prompts", "agent responses", "tool-call traces"]
---

SWE-chat is a corpus of real coding-agent sessions introduced by Baumann et al. and used as one of the
two datasets behind [[ScholarlyArticle/how-coding-agents-fail-their-users]]. It covers CLI workflows
specifically, and complements the IDE-weighted SpecStory exports that study pairs it with.

## Contents

A record is a single coding-agent session: interleaved user prompts, agent responses, and tool-call
traces such as file edits and command executions. The corpus contributes 5,785 sessions across 198
repositories. CLI sessions run longer than IDE ones in the study
that uses it: it reports a median of five user-authored messages per session across its CLI group
against three across its IDE group, though the per-agent medians in its combined dataset vary widely
(eight for OpenCode, five for [[SoftwareApplication/claude-code]], one for
[[SoftwareApplication/openai-codex]]).

Agent identity is recorded for these sessions, unlike the early SpecStory exports the study pairs them
with: within the study's CLI group, sessions are attributed to [[SoftwareApplication/claude-code]] (6,648), OpenCode (624),
[[SoftwareApplication/openai-codex]] (517), Gemini CLI (39) and Cursor CLI (32), with 483 of unknown
agent. Those counts describe the study's combined CLI group rather than SWE-chat alone. The study does not
analyse results by model identity, giving two reasons: SpecStory exports do not record it, and within
SWE-chat, Claude-family models account for 94.9% of annotated responses, leaving insufficient variation
for meaningful comparison.

## Provenance

The corpus was collected via Entire.io, a tool that logs CLI coding-agent sessions. It comprises public
checkpoint logs from developers on GitHub who opted in between January and April 2026. The study using
it characterises that public availability as reflecting deliberate developer action rather than
incidental exposure, and reports redacting personally identifiable information — names, emails, phone
numbers and credentials such as API keys and OAuth tokens — from extracted records before analysis.

## Use

[[ScholarlyArticle/how-coding-agents-fail-their-users]] combines SWE-chat with a re-crawl of SpecStory
exports to assemble 20,574 sessions from 1,639 repositories, having first verified that the two
datasets contain no overlapping repositories. That study's CLI-versus-IDE contrasts — notably that CLI
sessions are more prone to constraint violations and to damage reaching project and external state —
draw on SWE-chat for the CLI side. Because the CLI group in that analysis combines sessions from both
datasets, the authors re-ran the comparison within the SpecStory data alone and report that all
directions held, though the absolute values differed.
