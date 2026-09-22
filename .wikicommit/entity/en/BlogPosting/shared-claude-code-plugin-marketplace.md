---
title: "複数チームで1つのClaude Codeプラグインマーケットプレイスを育てる ── 共同運用で直面した5つの課題と対策"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, ai-adoption, agent-skills]
sources:
  - type: url
    url: 'https://techblog.zozo.com/entry/cc-plugin-marketplace'
    hash: sha256:3ea931e475eb0d34cf89d80370d5fb142dc0684ce20d67ed208b882d87f015b1
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An account of operating one shared Claude Code plugin marketplace across several teams at ZOZO, organized around five problems that shared operation produced and the mechanism used against each: team-owned directories for ownership, a marketplace manifest regenerated in CI from each plugin's own metadata, static validation in CI, an intent-searchable skill index, and an on-demand breaking-change check invoked from a pull-request comment."
  author: "木村, 上國料"
  datePublished: "2026-08-25"
  publisher: "[[Organization/zozo]]"
---

The post starts from a problem that only appears once agent tooling is working: as teams accumulate their own skills and agents, the assets stay inside the team that built them, and the gap between teams that are getting good at AI-assisted development and teams that are not keeps widening. The authors' stated ideal is that another team's development assets should be as readily referenced and reused as one's own, and usable as a starting point for new work. What they built toward that is a single [[DefinedTerm/claude-code-plugin-marketplace]] shared across teams, operated since the second half of 2025.

Sharing one catalog turned out to introduce problems of its own, and the post is organized around five of them, each mapped to a stage of the path a plugin travels from being written to being used by another team — develop, land via pull request, verify, discover and install, improve. All five are described as growing more frequent as the number of participating teams and plugins rises, and each is met with a different kind of mechanism rather than one general fix: structure for the first, code generation for the second, CI enforcement for the third, a separate search surface for the fourth, and an on-demand check for the fifth.

The account is explicit about where it stops. The authors state that a plugin's quality cannot be settled by reviewing text — you find out by installing it and running it — so the automated checks deliberately guarantee only an entry-level floor (does it minimally work, does it follow the conventions, does it duplicate something that already exists), with the mandatory human pull-request review left as what actually assures quality.

## Key Points

- The stated organizing problem is not tool adoption but asset isolation: skills and agents accumulate per team, and without a shared place the difference between teams pulls apart. The post's framing of the goal is that another team's asset should be referenceable and reusable exactly as one's own would be.
- Maintenance ownership is expressed in the directory layout rather than in metadata. Plugins live under a directory per owning team, plus a `common-plugins/` directory for cross-team ones, so the location of a plugin determines who maintains it; whether something belongs in the common directory is decided during pull-request review on the basis of expected cross-team use. The authors note that `plugin.json`'s author field identifies who wrote a plugin but not whether it was meant for one team or for everyone.
- This layout is possible because each catalog entry locates its plugin by relative path, so plugins do not have to sit in one fixed place. The authors record a limit they accepted: relative paths only reach plugins in the same repository, and they chose a single repository over cross-repository references to avoid spreading CI and repository settings across teams.
- The shared manifest is generated, not edited. Each plugin's own `plugin.json` is treated as the source of truth and the catalog manifest is rebuilt from all of them by a script run from CI, which commits the result back to the pull-request branch as a bot commit; developers only ever write their own plugin's metadata. The post states two consequences: regenerating the whole file every time rather than patching it means a deleted plugin cannot be left behind in the catalog, and sorting entries by path means two teams adding different plugins touch different lines, so the merge conflicts that a shared append-at-the-end file produces largely stop happening.
- Information that belongs to the catalog as a whole rather than to any one plugin has no `plugin.json` to be generated from, so it is kept in a separate metadata file that the generation script merges in. The authors state this file does not need editing when plugins are added.
- Structural errors are caught by CI rather than by reviewers, on the stated grounds that they are hard to see in a diff — and that a broken shared manifest fails marketplace updates for every team at once, so one team's mistake stops everyone from getting new plugins. Almost all of the checking is delegated to Claude Code's own `claude plugin validate`; the authors report writing only two checks of their own, for the presence of a README and for a plugin that has a `plugin.json` but was never registered in the catalog.
- Skills are searched by intent, not by description. The authors' stated diagnosis is that a `SKILL.md` description is written by its developer in implementation terms while a user searches in terms of what they want to do, so the two do not meet. Their skill index gives each skill several short task phrases describing situations it would be used in, weights those phrases most heavily in search, and generates them with a daily GitHub Actions job that combines ordinary scripting with Claude and only processes skills whose `SKILL.md` changed. Categories are used only as browsing tabs, not for matching. The post reports 73 skills covered at the time of the screenshot shown.
- Search is deliberately kept simple: the index is published as a static site on GitHub Pages because matching is client-side keyword matching with no embeddings and no LLM inference at query time.
- The fifth mechanism addresses reluctance rather than correctness. Because a developer cannot see how other teams use their skill, changes to a description's trigger conditions, an argument format or an output contract risk breaking unseen callers, so improvements get deferred; typing `@claude` in a pull-request comment runs a mechanical check along two axes — breaking changes (skill name and description triggers, argument and output contracts, agent contracts and status codes, hooks and MCP settings, deletion of referenced files) and marketplace conventions (`SKILL.md` length, description format, progressive disclosure, over-granted `allowed-tools`, MCP service separation, hard-coded secrets).
- Reported effects after about ten months: other teams' work became visible through the shared index, so their `SKILL.md` files can be read and adapted; concrete reuse occurred, with one team's cross-system search skill being split into four independent search agents that another team then called directly when building an incident-investigation skill; and onboarding shifted from building a plugin from scratch to installing existing ones and reading working examples. These are the authors' own account of one organization's experience, not measured results.
- Reported open problems: a catalog that grows easily also accumulates unused plugins that keep appearing in search results, and dependencies between plugins become hard to see; announcing additions and changes has degraded because posting to the dedicated Slack channel is left to individual judgment; keeping up with Claude Code's own pace of change threatens to date the catalog's assets; and the authors observe that every one of the five mechanisms was built after the problem had already surfaced, naming the operating cycle itself as the next thing to engineer.

## Context

The post sits alongside other firsthand accounts in this wiki of organizations standardizing agent use across teams rather than per individual, and it is the counterpart at catalog scale to [[BlogPosting/ai-driven-development-two-commands]], which describes one ZOZO division standardizing its own workflow into two commands. Where that post holds a stable surface over changing internals, this one holds a stable place for assets whose owners differ.

A recurring caveat the authors state is that mechanism is not the same as demand: the checks they built are explicitly an entry floor rather than a quality guarantee, and the closing section reports that the work of making shared operation safe consistently lags the ease of creating plugins. The post's technical account is written against Claude Code's official documentation and is dated by the authors to August 2026.
