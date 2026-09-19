---
title: "Sandboxing"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/agentic-engineering/sandboxing/'
    hash: sha256:fa1d62f87add57f7ca59294cf760dfbbfcf9a829c2af19ebb1535d78ede47485
  - type: url
    url: 'https://simonwillison.net/2025/Oct/20/claude-code-for-web/'
    hash: sha256:45fb7060c3561e36111229e2a76520baefc9e1538596494a73f3ba55f27fb826
  - type: url
    url: 'https://simonwillison.net/2025/Sep/30/designing-agentic-loops/'
    hash: sha256:616bc39546fd4aab969e3a8ec0a6fa01330405714c063a028ab4419f84132964
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The practice of running an AI coding agent in an isolated environment — a container, VM, separate branch, or disposable workspace — so its actions can't affect production systems or the real codebase."
---

Sandboxing is the practice of running an AI coding agent in an isolated environment — a container, a virtual machine, a separate branch, or a disposable workspace — where it can read files, write code, and run commands without affecting real production systems. If the agent makes a mistake, such as deleting a directory, corrupting a config file, or installing a bad dependency, the damage is contained to the sandbox and the real codebase stays untouched.

## Usage

Concrete forms of sandboxing include: git worktrees (an isolated copy of the repository for the agent to work in, merged if the result is good and deleted otherwise), containers (running the agent inside Docker with limited network access and filesystem isolation), cloud sandbox services such as GitHub Codespaces or Gitpod providing ephemeral dev environments, branch-based isolation where the agent works on a separate branch and CI verifies the changes before human review, network restrictions preventing the agent from making external API calls or accessing production services, and permission scoping (read-only access for most directories, write access only to specific paths) as a lighter-weight form of isolation even without full sandboxing.

[[BlogPosting/designing-agentic-loops]] sets out a middle option between isolating the agent locally
and simply accepting the risk: running it on **someone else's computer**, so that a rogue agent's
blast radius is bounded by not being your machine. That post's author names it as his own favourite,
gives GitHub Codespaces as his instance of it, and bounds the worst case as code checked out into the
environment being exfiltrated or bad code being pushed to the attached repository — with the CPU
being burned belonging to someone else. It reports hosted code-interpreter modes as able to go a
surprisingly long way in the same role, and reports the author having had a lot of success using
OpenAI's Codex Cloud that way.

## When It Applies

Sandboxing matters more as an agent is given more autonomy: agents can misinterpret instructions, hallucinate solutions, or execute commands with unintended side effects, and without isolation every action carries real risk, so each command needs review and approval before it runs. With sandboxing in place, an agent can experiment freely and only the final result needs review, which is described as dramatically speeding up workflows. It is presented as a general best practice for autonomous agents rather than one party's specific proposal, summarized as treating agent output like an untrusted pull request: let it work in isolation, review the result, and merge only after verification.

Where the account above treats network restriction as one isolation technique among several,
[[BlogPosting/claude-code-for-web-async-coding-agent]] singles it out as the hard part and the one
that carries the security argument. Reporting on Anthropic's sandboxing work, it describes filesystem
isolation as relatively easy and network isolation as the difficult problem, and quotes Anthropic's
approach: internet access permitted only through a unix domain socket connected to a proxy server
running outside the sandbox, which enforces which domains a process may reach and handles user
confirmation for newly requested ones. The post's stated reason this matters is
[[DefinedTerm/lethal-trifecta]] — the best defence against those attacks is to cut off one of the
three legs, and restricting outbound network access is how the exfiltration leg is removed. It also
notes the limit of a partial cut: an allow-list running to dozens of dependency-installation domains
left the author uneasy about exfiltration paths surviving inside it, whereas a no-network mode leaves
nothing to worry about on that axis.

That post also supplies the argument for why sandboxing is worth the effort rather than simply
approving each action: it reads Anthropic's investment as an acknowledgement that agents run without
step-by-step permission prompts are far more productive than agents that require them, which makes
convenient safe execution — not tighter approval — the problem to solve. The author describes this
approach as the only one that feels credible to him.

How reliably any of this is achieved in practice is treated more sceptically in
[[BlogPosting/designing-agentic-loops]]. That post reports that coding agents implement their own
levels of sandboxing but that its author has not seen documentation of them convincing enough to
trust — his own assessment rather than a tested finding — and treats Docker or Apple's container tool
as a reasonable risk to accept for most people while noting that container escapes exist. Its blunter
observation is about uptake rather than technique: offered a sandbox, someone else's machine, or
simply taking the risk, most people are said to choose the third. The same post quotes Anthropic's
Claude Code documentation recommending that `--dangerously-skip-permissions` be used in a container
without internet access, and endorses restricting an agent to a list of trusted hosts as a way to
stop exfiltration of private source code.

## Related Terms

[[DefinedTerm/guardrails]], [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/tool-use]], [[DefinedTerm/agentic-engineering]], [[DefinedTerm/lethal-trifecta]], [[SoftwareApplication/claude-code-for-web]], [[DefinedTerm/yolo-mode]]
