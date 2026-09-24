---
title: "SWE-chat: Coding Agent Interactions From Real Users in the Wild"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, evaluation, vibe-coding, human-oversight, security]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.20779'
    hash: sha256:2da8cc42c5f1fad936e428f3013e1a312598cbf5a01c8c1112ea9578963593b4
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Stanford preprint introducing SWE-chat, a living dataset of real coding-agent sessions from public GitHub repositories with line-level human-versus-agent code attribution, and using it to characterize how developers use coding agents in the wild and how those agents fail."
  author: ["Joachim Baumann", "Vishakh Padmakumar", "Xiang Li", "John Yang", "Diyi Yang", "Sanmi Koyejo"]
  abstract: "The paper presents SWE-chat, described as the first large-scale dataset of real coding-agent sessions collected from open-source developers in the wild, containing about 6,000 sessions with more than 63,000 user prompts and 355,000 agent tool calls. It finds that coding patterns are bimodal — agents author virtually all committed code in 41% of sessions and humans write all of it in 23% — that only 44% of agent-produced code survives into commits, that agent-written code introduces more security vulnerabilities than human-authored code, and that users push back against agent outputs in 44% of turns."
  keywords: ["coding agents", "human-agent interaction", "vibe coding", "code survival", "in-the-wild evaluation"]
---

This preprint from Stanford University starts from the observation that AI coding agents are being
adopted at scale while evidence on how people actually use them remains largely anecdotal: most
software engineering benchmarks are curated problems with well-defined, verifiable solutions and
complete upfront instructions, and none captures how developers prompt, steer, override and finally
commit or discard what an agent produces. To fill that gap the authors built [[Dataset/swe-chat]], a
dataset of real sessions collected from public GitHub repositories whose developers opted into
session logging with [[SoftwareApplication/entire-cli]], which links each session to commits with
line-level human-versus-agent authorship attribution. At the time of writing it held almost 6,000
sessions across more than 200 repositories, with over 63,000 user prompts and 355,000 agent tool
calls; about 85% of the data comes from [[SoftwareApplication/claude-code]].

The analysis addresses two questions — how users interact with coding agents on real tasks, and how
agents fail in practice and how users respond. Sessions and prompts were annotated with LLM judges
selected after validation against 100 human gold labels per task (for user intent, pushback, persona
and session success), and efficiency was measured directly from session logs and commit attribution.
Security was assessed by running the Semgrep static analyzer on each commit's before and after
snapshots.

## Key Points

- Authorship is strongly bimodal. The authors define three coding modes by the share of committed code
  the agent wrote: human-only (22.7% of sessions), collaborative (36.5%), and
  [[DefinedTerm/vibe-coding]], operationalized as sessions where more than 99% of committed code was
  agent-authored (40.8%). Over the three-month observation window the vibe-coding share doubled from
  about 20% to over 40%.
- Agents are used for much more than writing patches: understanding existing code or behavior was the
  most common specific intent (19.0% of prompts), and a third of agent tool calls were bash commands,
  predominantly git operations. The authors conclude that benchmarks focused narrowly on patch
  generation underestimate the operational diversity of real agent work.
- Most sessions were rated as largely successful (90% scored 50 or above), but less than half (44.3%)
  of agent-produced code survived into user commits, mainly because users chose not to commit it. In
  vibe-coding sessions 59% survived, which the authors note may reflect better-targeted output or
  lower user scrutiny.
- Vibe coding was the least economical mode per committed line: a median of 204K tokens per 100
  committed lines, roughly three times collaborative sessions and twice human-only ones, and 12.6
  minutes per 100 lines against 4.8 for collaborative sessions. Collaborative coding was the most
  cost-efficient mode, which the authors read as suggesting that the current push toward full autonomy
  may be counterproductive.
- Vibe-coded commits introduced Semgrep-detected vulnerabilities at 0.76 per 1,000 committed lines,
  roughly nine times the human-only rate (0.08) and five times the collaborative rate (0.14); they
  also fixed more vulnerabilities, but introductions exceeded fixes in every mode. Detected issues
  included path traversal, command injection, unsafe format strings and SQL injection.
- In Claude Code sessions the agent rarely stopped to ask for clarification (1.1%–2.6% of turns),
  while users interrupted it in 3.3%–6.0% of turns and pushed back with corrections, rejections or
  failure reports after 39% of turns regardless of mode; interruptions most often came as the agent
  left plan mode, made a git operation or edited a file. The authors summarize this asymmetry as
  autonomy outpacing oversight, with users compensating for agents that rarely signal uncertainty.
- Most users behaved as "expert nitpickers" who keep a stable goal while issuing precise corrections,
  even in vibe-coding sessions, and changing goals mid-session was less common during vibe coding
  (5% against 10% in other modes) — in contrast, the authors note, to benchmarks that supply complete
  instructions upfront.

## Notes

The authors present SWE-chat as a living dataset whose collection pipeline continually discovers new
sessions, and propose uses beyond this paper: benchmarks grounded in real workflows, more adaptive
human-agent interaction design, and user simulators trained on real trajectories for offline
evaluation. The abstract's figure for pushback (44% of turns) counts interruptions together with
post-turn pushback.

Limitations they state: the data covers only developers who use the Entire CLI on public repositories
and opt into logging, which selects early adopters and excludes proprietary enterprise codebases; a
large fraction of early data came from Entire's own repository; sessions whose output a user
abandoned are not committed and so not captured, which likely overestimates success and efficiency;
line-level attribution misses agent code that survives in rewritten form; and LLM-generated labels
are imperfect, so the authors caution against taking them at face value. The version extracted here
is arXiv:2604.20779v1.
