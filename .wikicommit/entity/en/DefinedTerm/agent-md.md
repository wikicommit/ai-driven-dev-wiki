---
title: "AGENT.md"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agent-config, coding-agents]
sources:
  - type: url
    url: 'https://github.com/agentmd/agent.md'
    hash: sha256:4365f280066b75c7dd36a75fac36ea644a7def7defead60293cae1344d78800f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A proposed single, vendor-neutral Markdown file at a project's root, put forward by Sourcegraph's Amp team in July 2025, that gives any agentic coding tool the project context it needs in place of each tool's own configuration file."
---

AGENT.md is a proposed standard format for a single Markdown file, placed at the root of a software
project, that gives any agentic coding tool the context it needs to work on that project — which
commands to run, which conventions to follow, and where the important code lives. It is defined in an
informational, RFC-style specification dated July 2025, written by Geoffrey Huntley for Sourcegraph,
Inc., and published from the `agentmd/agent.md` repository under the MIT license. The specification
frames the file as a replacement for the separate per-tool configuration files developers otherwise
maintain — `.cursorrules`, `.windsurfrules`, `.clauderules` and others — summarised in its own words as
"One file, any agent."

## Usage

The specification states its requirements in RFC 2119 terms. The file MUST sit in the project's root
directory and MUST use Markdown, and it SHOULD cover project structure and organization; build, test
and development commands; code style and conventions; architecture and design patterns; testing
guidelines; and security considerations. Implementations SHOULD support several files in a hierarchy
— a root-level file for general guidance, files in subdirectories for specific subsystems, and a
user-global file at `~/.config/AGENT.md` for personal preferences — and SHOULD merge them, with more
specific files taking precedence over general ones. A file MAY pull in other files through
`@`-mentions such as `@filename.md`.

For tool makers, the specification asks that the file be parsed during project initialisation, that
each tool extract the configuration relevant to its own use case, that there be fallback behaviour
when no file is present, and that existing tool-specific configuration files keep working for
backward compatibility. For projects that already have such files, it gives migration commands that
move the existing file to `AGENT.md` and leave a symbolic link at the old location, so that tools
which only know their own filename read the shared file. Commands are listed for Cline, Claude Code,
Cursor, Firebase Studio, GitHub Copilot, Replit and Windsurf, and for Gemini CLI, OpenAI Codex and
OpenCode the command links `AGENT.md` to an existing `AGENTS.md`. As guidance on content, it suggests
writing what a new team member would need on their first day — a project overview, build and test
commands, code style, testing, security and configuration — and includes a full example file.

The specification lists Amp, Sourcegraph's own agentic coding tool, as supporting the file natively
since 7 May 2025 and multiple files since 7 July 2025, and lists
[[SoftwareApplication/claude-code]], [[SoftwareApplication/cursor]], Firebase Studio,
[[SoftwareApplication/gemini-cli]], [[SoftwareApplication/openai-codex]],
OpenCode, Replit and [[SoftwareApplication/windsurf]] as supporting it
through that symbolic-link arrangement rather than natively.

The name is the point of contention with [[DefinedTerm/agents-md]], the plural form. The
specification says the Amp team is working with other agentic coding tool makers to consolidate
filenames, and that it prefers the singular because it owns the agent.md domain and commits to
keeping it vendor-neutral — something it says could not be said of AGENTS.md at the time — while
adding that it is willing to compromise.

## Related Terms

- [[DefinedTerm/agents-md]] — the plural-named format covering the same role
- [[DefinedTerm/ai-ide-rules]] — the tool-specific rule files AGENT.md proposes to consolidate
