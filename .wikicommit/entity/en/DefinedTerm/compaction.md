---
title: "compaction"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://www.langchain.com/blog/context-engineering-for-agents'
    hash: sha256:07e9475327ca11aeabb710cea3b419188e2ca4380d3cf4fd055291761f52fb8f
  - type: url
    url: 'https://code.claude.com/docs/en/best-practices'
    hash: sha256:92807ef3d58f63fbea435ea928df49e2f3341e118eb8c40db08800c100a4c4c5
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
    hash: sha256:2fa27ef4cd354e98bc9fd4d6cc5bec7f182d3b5a96745c6de6f694f18541f1a6
  - type: url
    url: 'https://arxiv.org/pdf/2606.22528'
    hash: sha256:ef37298f918eb3603bb29e729bf5490c27887bfadf9b5c6794e31dee79647cc2
  - type: url
    url: 'https://www.anthropic.com/engineering/managed-agents'
    hash: sha256:0e4e8bf6d9cb724da07f95297d00f7077a224890c85346851d0d455eba93d529
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Taking a conversation approaching the context window limit, summarising its contents, and reinitiating a new context window with that summary — the usual first technique applied when an agent's session must outlast its context window."
  termCode: ""
  inDefinedTermSet: ""
---

Compaction is the practice of taking a conversation nearing the context window limit, summarising its contents, and reinitiating a new context window with the summary. [[TechArticle/effective-context-engineering-for-ai-agents]] gives that definition and describes it as typically the first lever reached for in [[DefinedTerm/context-engineering]] to drive better long-term coherence: at its core it distills a context window's contents in a high-fidelity manner so the agent can continue with minimal performance degradation.

## Usage

Anthropic describes its implementation in Claude Code as passing the message history to the model to summarise and compress the most critical details — preserving architectural decisions, unresolved bugs, and implementation details while discarding redundant tool outputs or messages — with the agent then continuing from that compressed context plus the five most recently accessed files. Its stated goal is that users get continuity without having to think about context window limits.

The Claude Code documentation exposes this to users as automatic compaction when approaching context limits, plus manual controls: `/compact <instructions>` to steer what is preserved, an example being `/compact Focus on the API changes`; a rewind menu offering "Summarize from here" and "Summarize up to here" to condense only part of a conversation; and instructions in `CLAUDE.md` to customise the behaviour, its example being "When compacting, always preserve the full list of modified files and any test commands." It also recommends `/clear` between unrelated tasks as the blunter alternative — resetting context entirely rather than summarising it.

[[BlogPosting/context-engineering]] places compaction in its "compress" bucket, distinguishing summarization, which uses a model to distill, from **trimming**, which filters or prunes by hard-coded heuristics such as removing older messages. It notes summarization can be applied at points other than the end of a conversation — after token-heavy tool calls, or at agent-to-agent boundaries to reduce tokens during knowledge hand-off — and relays that Cognition uses a fine-tuned model for the step, which it presents as an indication of how much work can go into it.

The named risk is loss. Anthropic warns that overly aggressive compaction can discard subtle but critical context whose importance only becomes apparent later, and recommends tuning the compaction prompt on complex agent traces by first maximising recall and then improving precision. Its example of safe, low-hanging compaction is tool result clearing: once a tool has been called deep in the message history, the agent rarely needs to see the raw result again.

Where a task outlasts many context windows rather than one, the same vendor reports compaction as necessary but not sufficient. [[TechArticle/effective-harnesses-for-long-running-agents]] states that even a frontier coding model looped across multiple context windows on the Claude Agent SDK falls short of building a production-quality web app from a high-level prompt, and attributes part of the shortfall to compaction specifically: an agent that runs out of context mid-implementation leaves the next session with a half-implemented, undocumented feature, and this "happens even with compaction, which doesn't always pass perfectly clear instructions to the next agent." That post's prescription is to put the cross-session state into durable artifacts — a progress file, git history, a structured feature list — rather than to rely on the summary alone.

### What compaction is optimised for, and what that costs

The risk named above is loss of *task* context. [[ScholarlyArticle/governance-decay]] identifies a second class of loss with a different character: compaction also deletes the standing rules an agent is operating under, and does so precisely because it is working correctly. Its argument is that a summarizer optimising for task continuity has no reason to keep a policy — "the policy is 'old,' it is not the current sub-goal, and it competes for a shrinking token budget against the active task state" — so compaction "treats standing policies as low-salience content."

The measured consequence, across seven model families and four compaction strategies pooled over 1,323 episodes of the [[Dataset/constraintrot]] benchmark, is that compaction raises tool-call violation rates from 0% to 30%, and to 59% in the worst configuration. Conditioning on the summary isolates deletion as the mechanism rather than context length: 0% violation where the constraint survives compaction, 38% where it is dropped. The erosion is uneven in a way that matters operationally — 8.3× larger for soft organizational policies than for hard safety norms, so the rules that disappear are exactly the deployment-specific ones an operator wrote.

Where a rule lives determines whether compaction can reach it. In that paper's channel comparison, a policy in the preserved system message showed no decay, against +50, +45, and +33 percentage points as a standing user instruction, a memory entry, and a tool output respectively. The paper's proposed remedy, Constraint Pinning, quarantines governance constraints from lossy compaction and integrity-checks them across turns, restoring violation to 0% for roughly 47 pinned tokens; it also reports where naive pinning still fails. Its broader conclusion reframes what kind of decision compaction is: not only an economic one about the token budget, but "a first-class agent-governance surface."

### Storing context instead of deciding what to discard

[[TechArticle/scaling-managed-agents]] frames the standard answers to exceeding a context window — compaction, memory files, context trimming — as sharing one property: they all "involve irreversible decisions about what to keep." Its stated objection is epistemic rather than technical: it is difficult to know which tokens future turns will need, and once a compaction step transforms messages and the harness removes them from the window, they are recoverable only if they were stored somewhere.

The alternative it describes is to keep context as an object living *outside* the context window, durably stored in an append-only session log. A `getEvents()` interface then lets the agent interrogate that store by positional slices — picking up where it last stopped reading, rewinding a few events before a moment to see the lead-up, or rereading context before a specific action. Compaction and other transformations still happen, but in the harness on the way into the window, not destructively at the storage layer.

The stated reason for splitting these concerns is that the specific context engineering future models will need cannot be predicted, so the durable layer guarantees only that the record survives and can be queried, leaving what to do with it to whatever harness is running.

## Related Terms

Compaction is one of three standard techniques for long-horizon work, alongside [[DefinedTerm/agentic-memory]] and [[DefinedTerm/multi-agent-orchestration]]; Anthropic matches it specifically to tasks requiring extensive back-and-forth. [[DefinedTerm/adaptive-context-compaction]] describes a more specific variant in which reduction is applied in graduated stages as context pressure rises rather than as a single event at a hard limit. The underlying problem it exists to manage is [[DefinedTerm/context-rot]].
