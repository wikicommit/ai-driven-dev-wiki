---
title: "Agent Skills"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, context-engineering, agent-tooling]
sources:
  - type: url
    url: 'https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview'
    hash: sha256:3f2567f8a7cd1948e582601407ccfd2804e66152973859636da7ba44f9ff235f
  - type: url
    url: 'https://developers.googleblog.com/closing-the-knowledge-gap-with-agent-skills/'
    hash: sha256:99da78c38e52825287d818db6e10f2cf2d633b7e9479102298bccb809800d651
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A format, documented by Anthropic for Claude, for extending an agent with domain expertise: a directory holding a SKILL.md file of instructions plus optional scripts and reference material, loaded in stages so that an unused skill costs only its name and description in context."
---

Agent Skills is a format, documented by Anthropic for Claude, for packaging modular capabilities
that extend an agent's functionality. Skill packages are also written and published by parties other
than the agent vendor: Google's developer relations team writes that agent skills have surfaced as
an extremely lightweight but potentially effective way to close the gap between a model's fixed
training knowledge and fast-moving libraries and SDKs, and set out to show what any SDK maintainer
could do about that gap. Each Skill bundles instructions, metadata and optional resources such as scripts and
templates, which the model uses automatically when relevant. The vendor's documentation
distinguishes them from prompts on the basis of scope and persistence: prompts are
conversation-level instructions for one-off tasks, whereas Skills are reusable, filesystem-based
resources that load on demand, so the same guidance does not have to be repeated across
conversations. The stated benefits are specializing the model for domain-specific tasks, creating
guidance once rather than repeating it, and composing several Skills for multistep tasks.

As Anthropic documents it for Claude, the format is filesystem-based by design: Skills exist as
directories in Claude's virtual machine environment, and Claude interacts with them using ordinary
shell commands — reading `SKILL.md` to bring its instructions into context, reading further files
when the instructions reference them, and running bundled scripts through the shell so that only
their output, never their code, enters the context window. Other harnesses reach a skill by other
means; Google's evaluation, for instance, gave the model an `activate_skill` tool and a `fetch_url`
tool for downloading the docs.

## Usage

Every Skill requires a `SKILL.md` file with YAML frontmatter carrying two required fields, `name`
and `description`. The documentation states the constraints on each: a name of at most 64
characters, restricted to lowercase letters, numbers and hyphens, with no XML tags and no reserved
words; and a non-empty description of at most 1024 characters, again with no XML tags. The
description must state both what the Skill does and when it should be used, because it is what the
model matches a request against when deciding whether to trigger the Skill.

Content is organized into three levels, each loaded at a different time — the arrangement the
documentation calls [[DefinedTerm/progressive-disclosure]]. Metadata is always loaded, at a stated
cost of roughly 100 tokens per Skill; the `SKILL.md` body loads when the Skill is triggered, at a
stated budget of under 5,000 tokens; and bundled resources cost nothing until read. The documented
consequence is that many Skills can be installed without a context penalty, and that a Skill may
bundle extensive material — comprehensive API documentation, large datasets — that is never charged
against context unless used.

Availability differs across the vendor's products. On the API, Skills require the code execution
tool and are selected by a `skill_id` in the container parameter, with pre-built document Skills for
PowerPoint, Excel, Word and PDF, and custom Skills uploaded through a Skills API and shared across a
workspace. In [[SoftwareApplication/claude-code]] custom Skills are filesystem-based and need no
upload, placed in a personal or project directory, while the pre-built document Skills are not
available there. On claude.ai both kinds work, with custom Skills uploaded as zip files and
individual to each user rather than centrally managed.

## When It Applies

The format applies where an agent needs domain expertise — workflows, context and best practices —
that would otherwise be restated in every conversation. In the arrangement Anthropic documents, it
assumes an execution environment giving the model filesystem access and the ability to run
commands.

The documentation is direct about the security assumption the format carries: Skills should be used
only from trusted sources, because they give the model new capabilities through instructions and
code, and a malicious Skill can direct the model to invoke tools or execute code in ways that do not
match its stated purpose. It advises auditing every bundled file, singles out Skills that fetch data
from external URLs as particularly risky since fetched content may itself carry instructions, and
recommends treating installation like installing software. Enterprise organizations are offered
content scanning for custom Skills uploaded through claude.ai and Claude Cowork; the documentation
notes it does not cover Skills uploaded through the Skills API or the Console.

## Evidence and Limitations

Google reports building a skill for the Gemini API
([[SoftwareApplication/gemini-api-developer-skill]]) and evaluating it against a harness of 117
code-generation prompts, finding that it raised results markedly for its newer models with strong
reasoning support and much less for older ones — a result Google reads as skills working, but
depending on the model's reasoning ability rather than on the skill alone. The method and figures
are on [[BlogPosting/closing-the-knowledge-gap-with-agent-skills]].

Two limitations are named by the same authors. They say they know from Vercel's work that direct
instruction through [[DefinedTerm/agents-md]] can be more effective than using skills, and that they
are therefore exploring other routes to supplying live SDK knowledge, such as MCP servers for
documentation. The Vercel evaluation itself is not among this wiki's sources, so what is recorded
here is what the Google authors say they take from it.
The second is maintenance: Google states there is no good skill update story beyond asking users to
update manually, and warns this could in the long term leave stale skill information in users'
workspaces, doing more harm than good. That concern cuts against the purpose the format is being put
to here, since a mechanism adopted to keep an agent current can itself go out of date in place.

## Related Terms

- [[DefinedTerm/progressive-disclosure]] — the loading strategy the format is built around
- [[DefinedTerm/context-engineering]] — the broader concern this format addresses
- [[DefinedTerm/agents-md]] — another file-based convention for giving an agent standing instructions
- [[SoftwareApplication/claude-code]] — one of the products the format is available in
