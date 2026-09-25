---
title: "Qoder"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, spec-driven-development]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.12231'
    hash: sha256:08aa95b018a1374f9de491d626d4f394b8efec41d830ef1726a1b8db6a69d9d6
  - type: url
    url: 'https://help.aliyun.com/zh/lingma/user-guide/agent'
    hash: sha256:ff93705ed5a254225f79b1ecef3ff91af0315b170a60a603e666e00fab589c61
  - type: url
    url: 'https://help.aliyun.com/zh/lingma/user-guide/tools'
    hash: sha256:27b9d11864d2f74ffe6990bd1e8d2b4ad8bad43c4735bf75e5d9387db5beda31
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/sdd/overview/'
    hash: sha256:946cf421ab8284921cee80b48fc236a89feb6dfd5c4a90f01ae072227495be73
  - type: url
    url: 'https://help.aliyun.com/zh/lingma/user-guide/code-review-agent'
    hash: sha256:ef40c22a5390c62d3c761a0e5431078665da73fcd3151121c4cfafb64296ad52
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An AI IDE from Alibaba whose rule files live under `.qoder/rules/`, one of five such tools examined in a 2026 mining and survey study of AI IDE rules. Alibaba Cloud separately documents a product it calls Qoder CN, and a third source describes a Qoder built for spec-driven development; the relationship between these accounts the sources held here do not establish."
  applicationCategory: "AI IDE"
  author: "Alibaba"
---

Qoder is an [[DefinedTerm/ai-ide]] published by Alibaba. It is one of the five tools
[[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] selected for study on the basis that each
lets developers explicitly define [[DefinedTerm/ai-ide-rules]] the IDE must follow during code
generation and chat interactions. That study records its release date as 21 August 2025, per the tool's official
changelog.

## Capabilities

Qoder's rule files live under `.qoder/rules/` in the project, and rules are honoured during
generation and chat — see [[DefinedTerm/ai-ide-rules]] for the mechanism as it works across tools.

## A product Alibaba Cloud documents as Qoder CN

Alibaba Cloud publishes a user guide, on `help.aliyun.com` under a `/zh/lingma/` path, for a product
its body text calls **Qoder CN**. Whether Qoder CN is this product under another name, a regional
edition of it, or a different product altogether is not something that guide or the study above
states, and nothing else held here settles it. The guide is recorded on this page because the name
is the nearest thing either source offers to a link between them; the account below is what that
guide says about Qoder CN, and should not be read as established of Qoder.

That guide describes an **agent mode** (智能体模式) which it says can decide for itself what to do,
sense its environment and use tools, carrying a coding task through end to end with project search,
file editing and the terminal. It lists four core capabilities. The guide says the agent makes
project-level changes, breaking a task down itself and editing several files across a project, with
iteration over successive turns and snapshot rollback available. It says the agent senses the project
automatically — framework, technology stack, the files a task needs, error messages — so that context
need not be attached by hand. It says the agent draws on more than ten built-in programming tools at
its own discretion, among them file search, file and directory reading, semantic symbol search within
the project, file modification, error retrieval and terminal execution, and that it does so without
asking the developer to confirm or intervene. And it says the agent decides on, writes and runs
terminal commands as part of carrying out a task.

A separate page of the same guide enumerates those tools by name, grouped by what they are for. The
inventory it gives is:

- **Retrieval** — `search_codebase` (semantic search over the current project), `search_file`,
  `grep_code`, `search_symbol`, `list_dir`, `web_search` (stated to need no API key),
  `fetch_content` (retrieving the content at a URL), `search_memory` and `fetch_rules`.
- **File editing** — `edit_file`, `read_file`, `delete_file` and `create_file`, which the guide says
  the agent uses to make changes across several files in a project.
- **Terminal execution** — `run_in_terminal` and `get_terminal_output`, with commands written from
  what has happened so far in the task.
- **Problem retrieval** — `get_problems`, which reads the code problems shown in the IDE's Problems
  pane.
- **Memory** — `update_memory`, invoked either when a developer asks for something to be remembered
  or when the tool judges that something should be retained automatically.
- **To-do planning** — `add_tasks` and `update_tasks`, which the guide ties to the agent planning for
  itself: it breaks pending work into to-do items and then revises the execution path as it goes.

That page also states that MCP services are supported and freely configurable by the developer,
which is consistent with the agent page's account of MCP tools below. Two small inconsistencies in
the table are worth noting rather than smoothing over: the heading "终端执行" (terminal execution)
appears twice, the second time over the to-do planning rows, and the `update_tasks` row has its
description in the name column.

On confirmation the guide describes two gates. Terminal commands, it says, are by default presented
for confirmation before each run, with Run sending the command to the IDE's terminal window and
Cancel skipping it and returning to the agent, which then plans its next step from that feedback;
commands meant to run in the background are marked as such, and the agent carries on with other work,
checking their output when it needs to. An allowlist of commands that may run without confirmation is
described as configurable in the plugin's chat settings, under an Auto-Run section. Where MCP tools
are configured, the guide says the agent decides for itself whether calling one would help, asks
before each call, and feeds the result back in as context.

The guide also describes planning and task tracking. For a task it judges complex the agent is said to
produce a plan, shown to the developer for review before execution begins, with `/plan` triggering the
same thing deliberately; and to derive a to-do list from the request, extend it when the request is
extended, and show each item's state in the chat window. A separate prompt-optimization control is
described as rewriting a rough instruction into a more detailed one using the surrounding context and
conversation history, which the developer can then edit, submit or undo.

A further page of the same guide describes a **Code Review agent** built into agent mode, which it
says needs no separate configuration. The developer switches the chat panel to agent mode and uses a
`/code-review` command, or describes the review wanted in natural language, naming the scope: the whole
project, specific files, a Git diff or a pull request. The agent is said to review that scope across
several dimensions — logic defects, security vulnerabilities (SQL injection and XSS are the examples
given), performance bottlenecks and code-style problems — and to produce a structured report sorted by
severity into errors, warnings and suggestions, each giving the code location, a description of the
problem and a suggested fix. For large changes the page advises reviewing module by module to get
finer-grained feedback, and, where a change involves specific business logic, briefly explaining that
background in the request. See [[DefinedTerm/code-review-agent]] for the pattern across tools. That
page also carries a notice that a new documentation site for the Qoder CN series has gone live at
docs.qoder.cn, and that the content on the guide's own site may not reflect the product's latest
features and changes.

Note that the guide describes what is being configured as a plugin, with commands sent to a host
IDE's terminal window — which is a different shape from the standalone AI IDE the study above
describes Qoder as being. That is a further reason not to treat the two accounts as describing one
product.

## A third account, in a spec-driven-development survey

A chapter of Jimmy Song's online handbook 智能体构建指南, surveying representative implementations of
[[DefinedTerm/spec-driven-development]], lists a **Qoder** among them and describes it as an AI
programming assistant designed specifically for SDD scenarios, built on the idea of specification as
code. On that account it supports writing specifications in structured Markdown, generates project
structure, code and test cases from them, and helps the developer refine and evolve a specification
over successive rounds of conversation; it is said to integrate LLM, code generation, testing and
deployment capabilities, and to suit team collaboration and complex engineering work.

That chapter gives no URL, vendor or version for the tool it is describing, so whether it means the
AI IDE above, the plugin Alibaba Cloud documents as Qoder CN, or something else again is not
established by anything held here. It is recorded as a third account under the same name rather than
merged into either of the two above.

## Adoption & Ecosystem

Two figures from that study bear on adoption, and they measure different things. In its repository
mining, an initial search returned 125 candidate Qoder projects; after keyword and rule-file
filtering and manual inspection, 1 remained in the final dataset of 83 projects declared as
built with an AI IDE. In its practitioner survey, 16 of 99 respondents reported currently using
Qoder for development. The mining figure reflects how many public projects both use the tool and say
so in their README or description, which the study notes undercounts projects that use an AI IDE
without declaring it; the survey figure reflects self-reported use among developers who had committed
changes to rule files.
