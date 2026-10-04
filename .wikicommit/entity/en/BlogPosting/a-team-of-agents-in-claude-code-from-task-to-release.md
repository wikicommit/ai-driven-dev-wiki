---
title: "Команда агентов в Claude Code: от задачи до релиза"
type: "schema:BlogPosting"
lang: en
tags: [multi-agent, practitioner-report, agent-roles, code-review]
sources:
  - type: url
    url: 'https://habr.com/ru/articles/1086832/'
    hash: sha256:9c76f0c74d68bede0b7f7ea5e41acfac5237a0fe31876a274fcd47109094c0b6
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A Russian-language Habr case study by a solo developer who runs Claude Code agents as a twelve-role team through the Agent Teams feature, describing how a task moves from backlog to release with the human deciding at only two points."
  author: ["Sergey Ladygin"]
---

In this post a Go developer and team lead describes six months of building a service on his own, with the code written by [[SoftwareApplication/claude-code]] agents while he sets tasks and accepts results. What began as an experiment became a working scheme of twelve roles, a mandatory order of stages and as much agent autonomy as possible from task to release. The scheme was built on Claude Code's [[DefinedTerm/agent-teams]] feature, in which one session acts as team lead and the others are teammates working from a shared task list with dependencies.

The author explains how the setup grew: after writing a large specification with Claude and running one task per session, he found that he himself was the bottleneck, because Claude produced results faster than he could check them. That led to a QA role that tests in the browser and writes tests, a DevOps role, and a local environment able to exercise the whole product. The post then sets out the roles, the path of one task, why there is no separate code-review stage, the files that hold the team's memory, and how to start.

## Key Points

- Two commands frame the human's involvement: a weekly command in which an analyst role gathers metrics, compares last week's promises with results and proposes tasks, then stops until the author approves; and a per-task implementation command that starts as a tech lead, decomposes the task and leads it through architect, backend and frontend, DevOps, QA and documentation roles. These are the only two points where the author decides. Later the weekly command itself launched the implementation command for each approved task, so several "teams" worked in parallel, each producing a pull request.
- Each role is a markdown prompt file in `.claude/commands`; the tech lead spawns the others as teammates with tasks and dependencies.
- The author's central claim is that roles work when prohibitions are stated more firmly than duties — a QA role that fixes bugs itself stops finding them, because fixes happen silently and never reach the bug register. Even so, a written prohibition does not always hold: the tech lead, told never to write code, once did a small task itself, and did it worse than the frontend role would have.
- Three stages may never be skipped — DevOps rebuild, QA browser testing and documentation — and this rule is written in capitals in the tech lead's prompt after the lead once forgot to hand a task to DevOps and QA tested an old build.
- Developers must attach a "test impact" block naming affected test plans and modules, and the tech lead returns any task without one; the author says this cheap rule saved the most time, because QA runs only the affected modules instead of the full regression.
- There is deliberately no separate code-review stage. The author argues that classic review exists for control and for spreading knowledge, and that with agents control moves before the code (architecture decisions and per-role prohibitions), checking becomes automatic (tests and CI), and knowledge lives in files, since a review comment is useless to an agent that will not remember it. The author reads diffs less and less but always reads the architecture decision record before a merge.
- The team's memory is kept in the repository following a GitOps approach: specification, architecture decision records, a map of known failure diagnoses, a feature-and-coverage map, test cases, strategy and backlog, infrastructure, monitoring and dashboards as files, so that every agent sees the whole system and changes it through the same branch–PR–CI path as code.
- Roles moved between Claude Code and Codex with minimal edits because they are plain markdown files; over six months the models changed eight times without any role having to be rewritten, by the author's account.
- The suggested order for starting is a project map and specification first, then two or three roles as command files with a mandatory stage order, QA in the browser with integration tests as a gate, ADRs and failure notes as required outputs, and finally the weekly cycle.

## Context

This is one developer's account of his own project; the figures in the post (73 ADRs, 409 commits, a 3.9-hour median from first commit to merge across 61 pull requests, and others) describe that repository as of September 2026. The post's conclusion compresses the approach to roles with prohibitions, two human decision points and memory in files.
