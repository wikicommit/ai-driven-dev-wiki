---
title: "Agentic Coding"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, coding-tools, team-practices]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2505.19443'
    hash: sha256:6570a1ae86ae608d97b50f389a3ae52d197c066e9bb8412ba0eaea93265f7f52
  - type: url
    url: 'https://www.anthropic.com/research/claude-code-expertise'
    hash: sha256:0a6863b8e2c10a2517ea14c69053f2df45ca56ecf794fbbe95c1dc977fbf3879
  - type: url
    url: 'https://www.production-ready.de/2026/09/07/agentic-coding-done-efficient.html'
    hash: sha256:b507ecb9845ab7dd33c04b325e8e71953a95bd8024012c732706d7c435df4c1a
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Software development in which autonomous or semi-autonomous AI agents plan, execute, test, and iterate on multi-step coding tasks from a high-level goal, with the developer acting as a supervisor and reviewer rather than a direct implementer."
---

Agentic coding is a mode of AI-assisted software development in which autonomous or semi-autonomous software agents are delegated substantial cognitive and operational responsibility: interpreting a high-level goal, planning and decomposing it into sub-tasks, using tools and resources (compilers, test runners, version control, APIs) to execute them, and iterating based on feedback, with minimal continuous human intervention. The developer's role shifts from low-level implementer to system-level supervisor and goal-setter: specifying objectives and constraints, monitoring execution traces and outputs, and validating results before integration.

## Usage

Reviewed against vibe coding, agentic coding is characterized by moderate-to-high AI autonomy, hierarchical planner–executor architectures (often with specialized sub-agents such as a coder, tester, reviewer, and fixer coordinated by a planner), sandboxed or containerized execution environments, persistent memory across multi-step tasks, and an integrated validation pipeline that automatically synthesizes and runs tests rather than relying on a human to invoke them. Named examples of agentic coding platforms include Codex, which can run `git diff`, apply patches, and generate pull requests automatically; Google's Jules, which clones and analyzes a repository, modifies code, and commits changes to a new branch for review; and Claude Code, built with explainability and oversight features that let a developer audit changes, trace reasoning, and roll back unsafe actions.

## What It Looks Like in Practice

The account above is taxonomic — it describes what agentic coding is designed to be. A large-scale
observational study,
[[ScholarlyArticle/agentic-coding-and-persistent-returns-to-expertise]], reports what roughly 400,000
[[SoftwareApplication/claude-code]] sessions between October 2025 and April 2026 actually consisted of,
and several of its findings qualify the picture.

The supervisor role is real but narrower than "monitoring execution". Measuring who makes which
decisions, that study finds people making about 70% of planning decisions — what to do, which approach,
what counts as done — and the agent about 80% of execution decisions: which files to change, what code
to write, which commands to run. The split is between *what* and *how*, not between doing and watching.

The work is also less exclusively code than the definition suggests. Sessions divide across nine work
modes, of which roughly 56% write, fix, test or orchestrate code; 17% operate software (deploying,
configuring, running pipelines, monitoring); 14% plan or work out how an existing system behaves; and
13% produce data analysis or prose documents. Over the seven months observed, the share of sessions
spent debugging fell by nearly half while usage shifted toward more end-to-end agentic work.

The scale of delegation per instruction is measurable: a typical session runs about four turns, and each
user prompt sets off around 10 agent actions on average, occasionally over 100, with about 2,400 words
of agent output per turn.

What that study adds to the risk picture is a finding about who benefits. Session success rises with the
user's task-specific expertise — verified success 15% for novice-rated sessions against 28–33% for
intermediate and above, as adjusted rates comparing sessions matched on work mode, task-value band,
month, subject and occupation group, and excluding sessions judged to have no clear goal — while
occupation separates outcomes much less, with every one of the ten largest
occupations landing within seven points of software engineers on code-producing sessions. The authors'
reading is that a coding background is becoming less relevant to successful programming while command of
a domain is not. Note that these are transcript-based measures from one vendor's own product, and that
the study observes no real-world outcomes.

## What the Practice Demands

A practitioner account, [[BlogPosting/efficient-agentic-coding]], approaches the term from the
working conditions rather than the taxonomy, and draws the boundary more sharply than the
definition above: on its reading AI-assisted software development is *not* agentic coding, and a
coding agent treated as a chatbot inside the IDE yields no large efficiency gain, because the
constant exchange keeps the developer's attention on the conversation. The gain it identifies comes
from the agent working unattended until a required end state is reached, which leaves the developer
free to do something else — summarized there as not babysitting the AI.

The condition that makes this possible is a description precise enough that the developer need not
be present, and that post's central claim is about what such a description contains. Implementing
by hand involves a continuous stream of decisions made implicitly and often unreflectively — where
a class goes, what a method is named, how tests for this code are structured — because that is how
it has always been done or because it seems obvious; none of that is available to a model unless it
is said. The work of development is recast accordingly as making those decisions in advance and in
the open, at several levels of abstraction: the system and the context the feature sits in, user
personas, the feature definition from the user story, acceptance criteria, technical constraints,
and where it matters the required class and method names. Prompts of several dozen lines are
described there as unremarkable. That post also attributes dissatisfaction with agent output to
missing context rather than to model capability, which it holds is adequate for most coding tasks,
and sorts context by scope: what can be derived from the existing codebase by pointing at a
particular class, what holds project-wide and belongs in an `AGENTS.md` file, and what is specific
to the task and belongs in the prompt.

Its second condition is a feedback signal the agent can act on without a human: static analysis,
linters, and above all test coverage, so that the result is semantically and not merely
syntactically correct. That post holds end-to-end tests the most valuable kind and argues an agent
can produce good ones alongside the implementation where writing them by hand would have been too
laborious, and that a test-first workflow transfers directly — asking for a failing test before the
fix or feature, which then goes green.

On review it reframes the question from whether a human reviews to when: skipping code review does
not remove the review, it moves it onto staging or production and onto a product owner, and a
defect found there costs a full pipeline run to correct. The difficulty of reviewing AI-generated
code is attributed there not to AI but to how reviews were already handled, with AI only amplifying
it — large pull requests touching dozens of files along no clear line are not sensibly reviewable
regardless of who wrote them. The practices it recommends are continuous with pre-AI advice: slice
stories small, break them into implementable tasks, change one thing per pull request, review
synchronously with colleagues, and review promptly and in batches.

Finally it treats non-determinism as something to use rather than tolerate. Repeated prompts give
varying results, which that post attributes to temperature and calls a feature of language models;
its argument is that the development process was never deterministic either, since different people
and the same person at different times arrive at different solutions, and that the variation
occasionally produces an approach the developer would not have reached — while code once generated
is deterministic like any other.

## When It Applies

It suits feature-level or system-level tasks where correctness, traceability, and automation matter more than exploratory speed: end-to-end feature implementation, complex multi-file refactoring, system migrations, and CI/CD pipeline automation. It assumes an execution environment that can safely grant an agent write access and tool use (a sandbox or container with resource and namespace isolation), and it introduces risks distinct from vibe coding: reduced human oversight can lead to skill atrophy in developers who stop engaging with implementation details, and autonomous changes across multiple modules can propagate errors silently if the agent lacks rollback mechanisms or observability hooks. It is presented as complementary to, rather than a replacement for, vibe coding — suited to the implementation and operational phases of a project that vibe coding's exploratory prototyping feeds into.

## Related Terms

[[DefinedTerm/vibe-coding]], [[DefinedTerm/ai-coding-agent]], [[DefinedTerm/harness-engineering]], [[DefinedTerm/agent-harness]], [[DefinedTerm/agents-md]]
