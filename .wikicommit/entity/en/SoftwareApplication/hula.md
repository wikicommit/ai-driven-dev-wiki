---
title: "HULA"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, human-oversight, multi-agent]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2411.12924'
    hash: sha256:50d1957ea820f6e5f810bb7b7dfbb7a37c553436a744ca397d1443636efc1a41
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A human-in-the-loop LLM-based software development agent framework, integrated into Atlassian JIRA, in which AI planner and coding agents work with the assigned engineer to turn a JIRA issue into a pull request."
  applicationCategory: "Human-in-the-loop software development agent"
  featureList: "JIRA issue and repository selection; AI Planner Agent for file localization and coding plans; AI Coding Agent for code changes with self-refinement against compilers and linters; human review, editing and regeneration of files, plans and code; pull request creation in Bitbucket or a new code branch"
  author: "[[Organization/atlassian]]"
---

HULA (Human-in-the-loop LLM-based Agents) is a framework for software development in which
LLM-based agents and a software engineer work together to resolve a JIRA issue. It is introduced in
[[ScholarlyArticle/human-in-the-loop-software-development-agents]], whose authors designed,
implemented and deployed it into Atlassian JIRA for internal use. Rather than aiming to fully
automate software development, it is designed to function as an assistant, incorporating the
engineer's feedback at each step.

## Capabilities

HULA consists of three agents. The AI Planner Agent is an LLM that takes a JIRA issue and a source
code repository, identifies the files relevant to the issue, and generates a coding plan describing
how each file should change. The AI Coding Agent is an LLM that takes the plan and generates code
changes, refining them iteratively against feedback from code validation tools such as compilers and
linters until they pass or a maximum number of attempts is reached. The Human Agent is the engineer
assigned to the task, who reviews and edits the plan and code and raises the pull request.

The workflow runs in four stages inside the JIRA issue's user interface. The engineer sets up the
task by selecting an issue and a repository; in planning, the engineer can review, edit and confirm
the relevant files, then review the plan, add instructions and regenerate it or edit the change plan
for each file; in coding, the engineer reviews the proposed changes and can give further
instructions to regenerate them; and finally the approved changes are raised as a pull request to
Bitbucket for review by other practitioners, or checked out as a new branch for further changes.
The agents follow a Decentralized Planning Decentralized Execution paradigm with no communication
among agents, sharing only the JIRA issue and the repository as common memory.

## Adoption & Ecosystem

HULA was rolled out inside Atlassian gradually: first to an alpha group of 45 engineers across two
teams for two weeks, then from early July 2024 to 260 practitioners, expanding to 2,600 by
mid-September 2024, with more than 22,000 eligible issues. The paper's survey of practitioners who
used it reports that it helped reduce initial development time and effort and that its reliance on
issue descriptions encouraged documentation, while users asked for the ability to move back and
forth between the planning and coding stages, richer input context, and test case generation. The
paper uses GPT-4 as HULA's backbone model and describes the framework as architecture-agnostic. It
is an example of [[DefinedTerm/human-in-the-loop]] design for coding agents.
