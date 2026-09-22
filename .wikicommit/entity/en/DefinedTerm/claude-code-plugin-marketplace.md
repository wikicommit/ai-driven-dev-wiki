---
title: "Claude Code Plugin Marketplace"
type: "schema:DefinedTerm"
lang: en
tags: [agent-skills, claude-code]
sources:
  - type: url
    url: 'https://techblog.zozo.com/entry/cc-plugin-marketplace'
    hash: sha256:3ea931e475eb0d34cf89d80370d5fb142dc0684ce20d67ed208b882d87f015b1
  - type: url
    url: 'https://toss.tech/article/harness-for-team-productivity'
    hash: sha256:c578d09dce25f7293277154d1741cd800ad5d6afd7700ee897468e966f53f939
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A catalog for distributing Claude Code plugins, which handles discovery, version management and automatic updating together. Its concrete form is a single JSON file at the root of a Git repository listing every plugin it distributes and the in-repository path to each, while each plugin carries its own metadata file alongside its components."
---

A Claude Code plugin marketplace is a catalog through which plugins for [[SoftwareApplication/claude-code]] are distributed, covering discovery, version management and automatic updating in one place. A plugin is itself a package bundling several kinds of component: Skills, which hold the guidelines Claude refers to and are also where a slash command such as `/create-pr` actually lives; Agents, sub-agents that carry out a particular job autonomously; Hooks, processing that fires on a particular event such as task completion; and MCP server settings for connecting to outside services (see [[DefinedTerm/model-context-protocol]]).

## Usage

Getting to a usable plugin takes two steps rather than one, and the distinction matters in practice: adding a marketplace only makes its catalog visible, with no plugin installed yet, and each plugin is then installed individually from it (`/plugin marketplace add <org>/cc-plugin-marketplace`, then `/plugin install my-plugin@cc-plugin-marketplace`).

The structure is two-tiered. The marketplace itself is one JSON file, `.claude-plugin/marketplace.json`, at the root of a Git repository, listing the name and in-repository path of every plugin it distributes. Each plugin directory then carries its own `.claude-plugin/plugin.json` holding that plugin's own metadata — name, version, description. An entry in the marketplace file is the contents of a plugin's own metadata plus a `source` path, and because that path is relative, plugins do not have to be arranged in any particular place inside the repository; a marketplace can group them however it likes, so long as the paths match. That relative form only reaches plugins inside the same repository, though plugins in other repositories can be referenced by other means such as a GitHub source.

Version handling has a deliberately minimal option. Omitting the `version` field from a plugin's metadata makes Claude Code treat the Git commit SHA as the version, so merging is itself the act of shipping the latest version.

Validation is available as a first-party command. The structural defects worth catching in a catalog are given as JSON syntax, missing required fields, duplicate plugin names, defects in `SKILL.md` and agent frontmatter, and `hooks.json` syntax, and almost all of that checking can be delegated to `claude plugin validate`; the presence of a README, and a plugin that has its own metadata file but was never registered in the catalog, are named as things the command does not cover. It also rejects a `source` path that points outside the marketplace root, such as one using `../` — plugins are copied into a cache directory at install time, so a source outside the root risks not working or reaching an unintended location rather than merely being malformed.

A second account, [[BlogPosting/raising-productivity-floor-with-harness]], is concerned with what
an organization would distribute this way rather than with how a catalog is built. Its argument is
that the mechanism is better read as a platform for publishing an organization's way of working:
shared modules become workflow plugins and library publication becomes marketplace upload, with
only the contents changing from code to prompts and agent logic. Two uses are sketched — a hook
that catches a commit attempt on the main branch and redirects the agent to create a feature
branch, which that post contrasts with a linter that only blocks; and a single slash command
carrying a strong engineer's whole feature workflow so that any team member can invoke it. The same
post argues a marketplace is more predictable than retrieval-augmented generation for this purpose,
on the grounds that a plugin is explicit text a developer fully controls, and that it can be
revised and validated locally without a deployment. All of that is offered there as a direction
rather than a result, and a commenter on it argues that tracking which of many layered plugins are
active would become its own visibility problem.

## When It Applies

The mechanism suits distributing a set of plugins that people are expected to discover and adopt rather than be handed, which is why discovery and update are bundled into it rather than left to whoever installs. It assumes a Git repository the consumers can reach, and — for the relative-path form — that the plugins live in that same repository.

Its structural weak point, as described in [[BlogPosting/shared-claude-code-plugin-marketplace]], is that everything a marketplace distributes is enumerated in one shared file. Where several teams contribute to one catalog, every change lands in that file, so merges collide; and because the file is what the catalog is, a syntactically broken one makes `/plugin marketplace update` fail across the whole marketplace, leaving every consumer unable to fetch anything new. That account also notes what the format does not express: a plugin's metadata records its author, but nothing in the structure says whether a plugin is meant for one team or for everyone, or who is responsible for fixing it when it breaks.

How well established it is: the mechanism itself is Claude Code's own, documented by its vendor; the operational characterization above comes from one organization's roughly ten-month account of running a shared marketplace, dated by its authors to August 2026.

## Related Terms

- [[DefinedTerm/agent-skills]] — the component a plugin most often exists to distribute
- [[DefinedTerm/agent-hooks]] — another component type a plugin can bundle
- [[DefinedTerm/model-context-protocol]] — the protocol behind the MCP server settings a plugin can carry
- [[DefinedTerm/progressive-disclosure]] — a convention applied to the `SKILL.md` files distributed this way
- [[DefinedTerm/executable-ssot]] — the argument for holding team knowledge as a plugin rather than a document
- [[DefinedTerm/raising-the-floor]] — the organizational goal one account gives for distributing plugins
