---
title: "Qoder"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.12231'
    hash: sha256:08aa95b018a1374f9de491d626d4f394b8efec41d830ef1726a1b8db6a69d9d6
  - type: url
    url: 'https://help.aliyun.com/zh/lingma/user-guide/agent'
    hash: sha256:ff93705ed5a254225f79b1ecef3ff91af0315b170a60a603e666e00fab589c61
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An AI IDE from Alibaba whose rule files live under `.qoder/rules/`, one of five such tools examined in a 2026 mining and survey study of AI IDE rules. Alibaba Cloud separately documents a product it calls Qoder CN, whose relationship to this one the sources held here do not establish."
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

Note that the guide describes what is being configured as a plugin, with commands sent to a host
IDE's terminal window — which is a different shape from the standalone AI IDE the study above
describes Qoder as being. That is a further reason not to treat the two accounts as describing one
product.

## Adoption & Ecosystem

Two figures from that study bear on adoption, and they measure different things. In its repository
mining, an initial search returned 125 candidate Qoder projects; after keyword and rule-file
filtering and manual inspection, 1 remained in the final dataset of 83 projects declared as
built with an AI IDE. In its practitioner survey, 16 of 99 respondents reported currently using
Qoder for development. The mining figure reflects how many public projects both use the tool and say
so in their README or description, which the study notes undercounts projects that use an AI IDE
without declaring it; the survey figure reflects self-reported use among developers who had committed
changes to rule files.
