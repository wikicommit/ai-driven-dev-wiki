---
title: "Sub-agent architecture"
type: "schema:DefinedTerm"
lang: en
aliases: ["Multi-agent architecture"]
tags: [agents, context-window, long-horizon-tasks]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
  - type: url
    url: 'https://www.anthropic.com/engineering/claude-code-best-practices'
    hash: sha256:9aae24f8b850a5f9c8a6f561be1fecf54f29e1ddc4658d00ecded22bccb82b82
  - type: url
    url: 'https://www.anthropic.com/engineering/multi-agent-research-system'
    hash: sha256:9d24a3bfa582cdeb35b5470314362e43ded1cceb6659830329c69fe72147a2e4
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62110/'
    hash: sha256:63c389aa849ff61307fb6c1aeae2debc609bb205fea277d3393d798eacf874da
  - type: url
    url: 'https://zenn.dev/globis/articles/d0c73d2b176ba5'
    hash: sha256:d007e48e9860eef6953063dd12b23e8be1cf1576ddabcc4574d8a292c21d4357
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/agent/agent-basics/'
    hash: sha256:0e39f53f9f6fff0ddac9779101da8aef50cca78d20a39bf6f9814d0647866bf7
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An arrangement in which specialised sub-agents handle focused tasks with clean context windows while a main agent coordinates from a high-level plan."
---

A sub-agent architecture is an arrangement in which specialised sub-agents handle focused tasks
with clean context windows, while a main agent coordinates the work from a high-level plan —
rather than one agent attempting to maintain state across an entire project. Anthropic presents it
as one of three techniques for working around context window limitations on long-horizon tasks,
alongside [[DefinedTerm/compaction]] and [[DefinedTerm/structured-note-taking]].

## Usage

The sub-agents perform the deep technical work, or use tools to find relevant information. Each
might explore extensively — Anthropic puts it at tens of thousands of tokens or more — but returns
only a condensed, distilled summary of its work, which it gives as often 1,000 to 2,000 tokens.
The result is a clear separation of concerns: the detailed search context remains isolated within
the sub-agents, while the lead agent focuses on synthesising and analysing the results.

Anthropic's Claude Code best-practices documentation describes two distinct jobs for the same
mechanism, and separating them is useful because they trade on different properties of a fresh
context. The first is **investigation**: because researching a codebase means reading many files and
every one of them consumes the main conversation's context, delegating the research to subagents that
explore separately and report back a summary keeps the main window clean for implementation. This is
the context-economy argument above, restated for a coding rather than a research setting.

The second is **adversarial review**, where the value is independence rather than economy. A reviewer
running in a fresh subagent context sees only the diff and the criteria it is given, not the reasoning
that produced the change, so it evaluates the result on its own terms — the documentation's framing is
that the longer an agent works unattended, the more an independent check matters before the work counts
as done. Because the reviewer runs as a subagent, its findings return directly to the implementing
session, which can fix them and re-review without a human ferrying findings between windows.

The same documentation states the failure mode of the second use plainly, and it is a caution worth
recording alongside the pattern: a reviewer prompted to find gaps will usually report some even when
the work is sound, because that is what it was asked to do. Chasing every finding is said to lead to
over-engineering — extra abstraction layers, defensive code, and tests for cases that cannot happen —
so the recommended mitigation is to instruct the reviewer to flag only gaps affecting correctness or
stated requirements, and to treat the rest as optional.

A third account, [[BlogPosting/how-we-built-our-multi-agent-research-system]], describes the same
arrangement as it was actually shipped, and names it an **orchestrator-worker pattern**. A lead agent
analyses the user's query, develops a strategy and spawns subagents to explore different aspects
simultaneously; the subagents act as intelligent filters, iteratively using search tools and returning
findings the lead agent synthesises before deciding whether more research is needed. Two details of
that production system are specific to running it at length rather than to the pattern's shape: the
lead agent saves its plan to memory because a context window exceeding 200,000 tokens is truncated,
and a separate CitationAgent processes the documents and the draft report at the end to locate where
citations belong. That post contrasts the whole arrangement with Retrieval Augmented Generation's
static retrieval — fetching the chunks most similar to a query — in favour of a multi-step search that
adapts as findings arrive.

That account also gives an explanation for why the pattern works that is about capacity rather than
cleverness. On the BrowseComp evaluation the team reports three factors explaining 95% of performance
variance, with token usage alone explaining 80% and number of tool calls and model choice the other
two — which it reads as validating an architecture that distributes work across separate context
windows to add parallel reasoning capacity.

A fourth account comes from the adopting side rather than the vendor side, and applies the pattern
to ordinary product development rather than research.
[[BlogPosting/two-engineers-ai-driven-product-development]] describes a two-engineer team running
37 Skills and 24 SubAgents, where a Skill defines expertise or required behaviour — what order to
do things in, what the quality bar is, what to do on failure — and a SubAgent is a specialist agent
for one area that may itself use Skills. A main agent uses a Skill to orchestrate the SubAgents, and
the composition is per phase rather than per query: three SubAgents for business requirements
(analyzer, generator, validator), seven across technical design and task splitting, and a further
set for implementation selected by language, plus two reviewers run in parallel.

Its answer to why not give one agent the whole job is the same context argument stated from
practice: one agent doing everything makes its context balloon and performance drop, whereas
splitting into specialists stabilizes output quality — and adds a second, operational reason none
of the vendor accounts gives *as a rationale for the architecture*, that a phase which fails can be
redone on its own rather than the whole run. (Anthropic does treat mid-run recovery elsewhere, as a
property its system was built to have rather than as a reason to split the work.) That post also supplies a concrete mechanism for keeping subagents independent — a formulation
it credits to an earlier piece rather than claiming as its own: each task file is written to be
self-contained, carrying its own schema, API spec and full Given-When-Then test items so
implementation never has to consult the design document. Its stated
reason is that separate sessions implement these tasks in parallel, so inter-task context
dependency must be zero — the file, rather than a conversation, is the interface between agents.

A fifth account is narrower than the others and concerns how a sub-agent comes to be chosen at all.
[[BlogPosting/growing-ai-code-review-with-single-responsibility]] describes a team defining each
sub-agent as a Markdown file — a name, a `description` and a model setting in the front matter, the
system prompt in the body — and reports that the orchestrating agent picks which one to run by reading
those `description` fields. On that account trigger conditions are not configured anywhere separate
from the description — they are written into it, as an explicit list of the file patterns that should
select this sub-agent — so writing the description concretely *is* the dispatch mechanism, and an
abstract description is given as the cause of both missed and spurious invocations.
The team reports having the model write each description from the sub-agent's own system prompt, while
treating whether it is then invoked as intended as a separate question settled empirically — by
creating test pull requests — since a clear file-pattern trigger is easy for the orchestrator to judge
and other cases are not.

A sixth account, a draft chapter of Jimmy Song's online handbook 智能体构建指南, restates the pattern
for AI programming and gives as its motivation that a single agent's context swells as a conversation
goes on and pollutes the main thread. It describes subagents as specialised, context-isolated sub-roles,
each completing a well-defined subtask in its own context before the results are gathered back into the
main thread, and says platforms such as [[SoftwareApplication/claude-code]] have turned this into a
product feature. It lists four benefits — context isolation; specialisation, with each subagent given
one atomic responsibility such as dependency upgrades, code review or i18n checks; reuse and governance,
through project- or user-level configurations that can set tool and permission boundaries; and
composition, with several subagents run in order as a workflow for reliability and verifiability.

That chapter names three ways a subagent comes to be invoked: automatic delegation, where the platform
matches the subagent's description against the context; explicit invocation in the prompt; and
configuration files such as `.claude/agents/*.md` that state trigger conditions and default behaviour to
make invocation more deterministic. Its design points are atomic granularity; declared inputs and
outputs, including the file paths a subagent produces, so the main thread and other subagents can pass
data to it; intermediate results written out explicitly to files, such as under a temporary directory,
with read and write permissions and file names stated in the description; keywords such as
`use PROACTIVELY` or `MUST BE USED` in the description to raise how often automatic delegation picks it;
and separate model and tool settings per subagent for safety governance. Its worked example is a
reusable workflow for adding a field to a domain model, run as four subagents in sequence — a dependency
upgrader, a domain-model field enhancer, a Maven build specialist and a tester — each one's output
becoming the next one's input, with the main agent or a verification agent doing the final compliance
check.

## When It Applies

- Applies to complex research and analysis where parallel exploration pays dividends. Anthropic
  sets this against compaction, which it recommends for tasks requiring extensive back-and-forth,
  and note-taking, which it recommends for iterative development with clear milestones.
- Assumes a main agent holding a high-level plan and sub-agents that can be given focused tasks
  with fresh context windows, together with the convention that each returns a distilled summary
  rather than its full working context.
- Anthropic reports that the pattern showed a substantial improvement over single-agent systems on
  complex research tasks. Its Research engineering post puts a figure and a configuration to that
  claim: a system with Claude Opus 4 as lead agent and Claude Sonnet 4 subagents outperformed
  single-agent Claude Opus 4 by 90.2% on the team's internal research eval, which is described as
  excelling especially on breadth-first queries pursuing several independent directions at once. The
  worked example given is identifying all the board members of the companies in the Information
  Technology S&P 500, which the single-agent system failed to answer through slow sequential searches.
  The particular eval behind that figure is not described, so its difficulty and coverage cannot be
  checked from here.
- Costs tokens in proportion to the capacity it adds. The same post reports that agents typically use
  about 4× the tokens of a chat interaction and multi-agent systems about 15×, so the arrangement needs
  tasks valuable enough to pay for the performance.
- Does not fit every domain. That post names as poor fits today those requiring all agents to share the
  same context or involving many dependencies between them, and most coding tasks specifically — on the
  grounds that they involve fewer truly parallelizable subtasks than research, and that agents are not
  yet good at coordinating and delegating to each other in real time.
- The adopting account above is a direct counterweight to that last point, and the two are worth
  reading together rather than reconciling. It reports running the pattern across a coding pipeline
  from requirements definition through pull-request review — release remains on its own future-work
  list — and sustaining three to four tasks in parallel, having removed the dependency Anthropic
  names by making each task file self-contained and isolating each run in its own `git worktree` and
  session — so the coordination *between* the parallel task streams is settled in advance, when the
  tasks are written, rather than negotiated at run time. Within a single task run, coordination is
  still real-time and central: an orchestrator Skill picks the specialist SubAgent the task calls
  for, launches it, judges the result and re-delegates fixes. What that setup relocates is therefore
  the inter-task dependency, not agent-to-agent coordination as such. Neither side of this is
  measured: the adopting team reports its own arrangement with no evaluation behind the
  parallel-coding claim, and the vendor's domain-fit limitation is a general statement its post
  makes without an eval behind it either — unlike the figures elsewhere in the same post. So what
  the adopting account establishes is that the limitation is contingent on how tasks are cut, not
  that it is wrong.
- Carries a coordination cost that has to be prompted away rather than assumed. Early versions of that
  system are reported spawning 50 subagents for simple queries and duplicating each other's work when
  task descriptions were vague, which the team addressed with explicit effort-scaling rules and detailed
  delegation instructions rather than with architectural changes.
- A stated limitation of that implementation is synchronous execution: the lead agent waits for each set
  of subagents to finish, which simplifies coordination but means it cannot steer them mid-flight,
  subagents cannot coordinate with one another, and a single slow subagent blocks the system.

- The handbook chapter above names three costs of its own: latency, because each time a subagent
  starts it has to reload context and resources; a context-switching cost, because to keep them
  isolated subagents usually do not inherit the main thread's full context, so parameters or files
  have to be passed to them explicitly; and maintainability, because a team's subagent library needs
  curating and conventions to avoid duplication and conflict.

## Related Terms

- [[DefinedTerm/compaction]]
- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/code-review-agent]] — the review use above, treated as a subject in its own right
- [[DefinedTerm/llm-as-a-judge]] — the same independence argument applied to evaluation
- [[SoftwareApplication/claude-code]] — the tool whose documentation describes the two uses above
