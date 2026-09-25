---
title: "Mitigating Prompt Injection Attacks in Software Agents"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agent-safety, security, prompt-injection, sandboxing]
sources:
  - type: url
    url: 'https://openhands.dev/blog/mitigating-prompt-injection-attacks-in-software-agents'
    hash: sha256:c531528526e6141ec71ff79c2e5e157b6f4eed38552de696dcc4c7135b39d6ff
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An OpenHands blog post on the prompt-injection risk facing highly autonomous coding agents, arguing that a model's refusal is only a soft block and surveying confirmation mode, security analyzers, sandboxing and hard policies as mitigations."
  author: ["Robert Brennan"]
  datePublished: "2025-08-14"
  publisher: "OpenHands"
---

This post from the [[SoftwareApplication/openhands]] blog addresses what it calls a major security
dilemma in working with AI agents: an agent given a certain combination of capabilities becomes
vulnerable to [[DefinedTerm/prompt-injection]] attacks, and merely giving an agent access to `curl` is
enough to both expose it to injected content and give it a means to exfiltrate data. The post treats
this as a serious problem for highly autonomous agents like OpenHands, which typically run without a
human watching them, and sets out steps to reduce the chance of a breach.

Its argument runs in two halves. Current models often see through obvious attacks, but that protection
rests on an LLM's fuzzy, non-deterministic behaviour and differs between models, so it cannot be relied
on alone. The post then places the risk alongside threats developers already accept — piping install
scripts into a shell, running `npm install` on unfamiliar projects — and works through four families of
mitigation, weighing what each gives up.

## Key Points

- When OpenHands running Claude Sonnet 4 was asked to browse to a pastebin message telling it to `curl` a script and pipe it to `bash`, it identified the security risk and warned the user instead of running the command; in a second test it refused to send the user's GitHub token to an innocuous-looking domain.
- The post calls this a *soft* block rather than a hard one: with a more innocuous-looking URL the agent did not run the script but went further, examining it first, which the author takes as showing the behaviour is non-deterministic.
- Different models behave differently; the post credits Anthropic with putting a lot of resources into red-teaming Claude and says OpenHands may be more willing to take destructive actions when powered by other models.
- It frames prompt injection against agents as an old problem with a new form factor, comparing it to developers running `curl | bash` setup scripts or `npm install` on unfamiliar projects, both of which give an attacker unrestricted access to the filesystem and environment, and to past compromises of an official install script and of npm packages, including one reached through a popular framework's transitive dependency.
- **Confirmation mode** — having the agent ask permission before almost any action — is the approach the post attributes to both Claude Code and the OpenHands CLI, and it calls this especially important on a local workstation; the author nonetheless judges it a stopgap that limits the value of agents without adding much security.
- **Security analyzers**, such as the one OpenHands added with Invariant Labs, assess the actions an agent wants to take for potential threats and can stop to ask for explicit permission or refuse to proceed; the post says they help both against deliberate injection and when an agent simply gets confused and tries something dangerous, while noting they have issues of their own.
- **Sandboxing**: every OpenHands conversation runs inside a Docker container, so even `rm -rf /` only breaks the agent's own environment; but the environment may still hold secrets that can be exfiltrated or used destructively, and with `curl` and the source code still available the agent could exfiltrate proprietary logic (see [[DefinedTerm/sandboxing]]).
- **Hard policies**: organizations self-hosting OpenHands on Kubernetes can use network policy and eBPF tooling to restrict what the agent may do inside its sandbox — blocking a site, allowlisting trusted domains, or blocking `curl` — and agents can be given different policies per task or seek a human's approval to escalate permissions. The post applies the principle of least privilege to agents, and notes that such policies take effort to set up, which large organizations may already have invested in while small startups generally have not.
- Its main advice is the same as for humans using `git clone`, `curl` and `npm install`: stick to trusted sources, since the user controls the agent's top-level instructions.
- The author reports having seen proof-of-concept attacks that got OpenHands to act on instructions the user did not give, but no real-world attack at the time of writing, and expects the threat to grow as agents become more popular and more powerful.

## Context

The post is written from the vendor's side, by OpenHands about its own agent, and its assessments of the
mitigations — confirmation mode as a stopgap, hard policies as the stronger option — are the author's
judgement rather than measured results. Its tests of model behaviour are a few illustrative prompts, not
a systematic evaluation.
