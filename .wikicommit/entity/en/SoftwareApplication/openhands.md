---
title: "OpenHands"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-coding, agent-architecture, open-source, multi-agent]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2407.16741'
    hash: sha256:93aed96e187f2e30f86b5bb87cf1cad0852515081dc699763752bf89e6c8e93d
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An open-source platform, formerly OpenDevin, for building AI agents that write code, run bash commands and browse the web inside a sandboxed environment, with a shared event-stream state, a community agent hub, and built-in evaluation benchmarks."
  applicationCategory: "DeveloperApplication"
  license: "https://opensource.org/license/mit"
---

OpenHands, formerly known as OpenDevin, is an open-source platform for developing AI agents that interact with the world in the same ways a human developer does — by writing code, using a command line, and browsing the web. It is documented in [[ScholarlyArticle/openhands]], which describes it as supporting the implementation of new agents, safe interaction with sandboxed environments for code execution, coordination between multiple agents, and the incorporation of evaluation benchmarks.

## Overview

An agent in OpenHands perceives an environment state and produces an action. The state's central component is an event stream: a chronological record of past actions and observations, including both the agent's own actions and user interactions such as instructions and feedback. Alongside it the state tracks the accumulated cost of LLM calls and the metadata needed for multi-agent delegation.

Its interface to the environment is a small set of general actions rather than a large tool catalogue. `IPythonRunCellAction` and `CmdRunAction` execute arbitrary Python and bash inside the sandbox, and `BrowserInteractiveAction` drives a browser through a domain-specific language. Because the action space is a programming language, conventional tools remain expressible within it: a user can write a Python function and expose it to the agent through the same primitive.

## Features

**AgentSkills** is an extensible tool library shipped as a Python package whose functions are automatically imported into the agent's IPython environment, so contributing a tool means writing a Python function. The project's stated inclusion criteria keep the library deliberately small: a skill is added only when writing the code directly is not readily achievable for an LLM — file editing that replaces specific lines is the example given — or when it requires calling an external model. Shipped skills include file-editing utilities adapted from SWE-Agent and Aider, `scroll_up` and `scroll_down` for viewing different parts of a file, and `parse_image` and `parse_pdf` for reading multi-modal documents.

**Agent delegation** lets one agent hand a subtask to another through a dedicated `AgentDelegateAction`, the documented example being the generalist CodeActAgent delegating web-browsing work to a specialized BrowsingAgent.

**AgentHub** collects community-contributed agent implementations that end users can choose between and that serve as baselines for different tasks. Its default generalist is **CodeActAgent**, which at each step either converses in natural language — to ask for clarification or confirmation — or performs the task by executing code, whether bash, Python, or the browser's own language.

A user interface lets users view files, inspect the bash commands and Python code that were executed, observe the agent's browser activity, and interact with the agent directly.

## History

The project is released under the MIT license and described in its paper as a community project spanning academia and industry, with more than 2,100 contributions from over 188 contributors as of that writing. Its reported benchmark results are its authors' own: on SWE-Bench Lite, CodeActAgent v1.8 with claude-3.5-sonnet reached a 26% resolve rate, and on the Python split of HumanEvalFix the agent fixed 79.3% of bugs in a 0-shot setting.
