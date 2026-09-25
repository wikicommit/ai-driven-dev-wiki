---
title: "GitHub Copilot Code Review"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, agents, coding-tools]
sources:
  - type: url
    url: 'https://docs.github.com/en/copilot/concepts/agents/code-review'
    hash: sha256:5288bbf7e00b1255000a7c40ad0d7129e795426d5c72d9dc46584d8c359c2ce8
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/60-million-copilot-code-reviews-and-counting/'
    hash: sha256:0fb7098fdd6a821dd84f639e8def29c0543822c62545b031dd7e3d62fdf5b5e2
  - type: url
    url: 'https://github.blog/changelog/2026-03-05-copilot-code-review-now-runs-on-an-agentic-architecture/'
    hash: sha256:12ca08274c792d7ac18521d05720988b8978f43e4ff157f7d9b66e8b3d9e27b0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "GitHub's pull-request review feature, in which Copilot reviews a pull request, identifies issues and suggests applicable fixes. Its agentic capabilities — whole-repository context gathering and handing suggestions to the cloud agent — run on GitHub Actions runners, and reviews can be requested manually or triggered automatically."
  applicationCategory: "AI code review"
  featureList: "Reviews pull requests in any language with applicable suggested fixes; whole-repository context gathering; passing suggestions to the Copilot cloud agent; automatic review on PR creation, on new pushes, or on drafts; Lite and Balanced review effort levels; approval assessment and optional approving reviews; use of repository agent skills and MCP servers during review; agentic tool-calling retrieval of repository context; memory across reviews; multi-line and clustered comments; batch autofixes"
  author: "[[Organization/github]]"
---

GitHub Copilot code review is a feature of [[SoftwareApplication/github-copilot]] in which Copilot reviews a pull request, identifies issues and suggests fixes that can be applied in a couple of clicks. GitHub's documentation states that it reviews code written in any language and looks at the change from multiple angles. It is described as a purpose-built product using a tuned mix of models, prompts and system behaviours, and model switching is deliberately not supported — the documentation's stated reason is that changing the model is likely to compromise reliability, user experience and the quality of review comments.

The documentation places it among the surfaces where it can be used — GitHub.com, the GitHub CLI, GitHub Mobile, VS Code, Visual Studio, Xcode, JetBrains IDEs, and Azure DevOps in public preview — and notes that where Copilot comes from an organization, that organization must enable the Copilot code review policy for reviews on GitHub.com and GitHub Mobile. Organization members without a Copilot license can be granted access on GitHub.com under Copilot Business and Copilot Enterprise plans, through two policies an administrator enables; that route is stated as unavailable in IDEs.

The documentation is explicit that the feature is not a substitute for human review: Copilot is stated as not guaranteed to spot all problems, as sometimes making mistakes, and its feedback is to be validated carefully and supplemented with a human review.

GitHub's own account of the product's aims, in [[BlogPosting/60-million-copilot-code-reviews-and-counting]], is that its target shifted after building began in 2024 from thoroughness to high-signal feedback that helps a pull request move forward quickly, tuned through a continuous evaluation loop against accuracy, signal and speed. On that account the feature deliberately stays silent when it has nothing worth saying — GitHub reports it surfaces actionable feedback in 71% of reviews and says nothing in the rest — and will accept slower reviews for better findings, citing one model change that raised positive feedback by 6% while increasing latency by 16%.

## Capabilities

A GitHub changelog entry dated March 5, 2026 announced that Copilot code review now runs on an agentic tool-calling architecture, gathering broader repository context as needed — relevant code, directory structure and references — so that feedback reflects how a change fits into the larger architecture, and that it was generally available. GitHub's blog post of the same day describes the redesign in more detail: the agent explores the repository to understand logic, architecture and invariants; records issues as it reads instead of finalizing them only at the end, which GitHub says often led to "forgetting" early discoveries; can keep memory across reviews, so a pattern flagged in one part of the codebase can inform later reviews; maps out a review strategy ahead of time for long, complex pull requests; and reads linked issues and pull requests to catch code that looks reasonable in isolation but does not match the project's requirements. GitHub attributes an initial 8.1% increase in positive feedback to this shift. The same post describes presentation changes made alongside it — comments attached to multi-line code ranges rather than single lines, repeated instances of one pattern error clustered into a single comment, and batch autofixes that apply a whole class of suggested fixes at once.

Separately, the product documentation describes two agentic capabilities that extend the basic review. The first is full project context gathering, which analyses the entire repository to better understand the context of a change; the second is the ability to pass suggestions to the Copilot cloud agent, which automates creating a new pull request against the branch with the suggested fixes applied — stated as public preview and subject to change. Both are enabled automatically on all plans that include the feature. They run on GitHub Actions, using standard GitHub-hosted runners by default, with larger GitHub-hosted runners or self-hosted runners as options; GitHub Actions need not be enabled in the organization for them to work, but where GitHub-hosted runners have been disabled the capabilities are unavailable and reviews fall back to a more limited form. If Actions is unavailable or the workflows fail, reviews are still generated without these features.

Two review effort levels are offered. Lite, the default, is described as a standard review giving fast, targeted feedback on common issues such as bugs, security vulnerabilities and style inconsistencies. Balanced routes the pull request to a higher-reasoning model for longer analysis of complex logic, security-sensitive code and cross-service changes, using more AI credits and possibly marginally more Actions minutes. The documentation recommends Balanced for security-sensitive code, multi-service pull requests and repositories with strict quality standards, and Lite where fast feedback matters more than exhaustive analysis. The effort level used is shown in the pull request overview comment after each run.

Reviews can be automatic rather than requested. By default Copilot reviews a pull request only when assigned to it; individual users on Copilot Pro or Pro+ can have all their own pull requests reviewed automatically, repository owners can enable it for a repository and organization owners for some or all repositories. Triggers depend on configuration: the basic setting fires when a pull request is opened and the first time a draft is switched to open, with further settings for reviewing every new pushed commit and for reviewing drafts. Unless configured to review each push, Copilot reviews a pull request once.

Every review includes an approval assessment in the overview comment indicating whether Copilot judged the pull request ready to approve, and by default this does not count toward required approvals. Copilot approvals — stated as public preview — can be enabled in repository, organization and enterprise settings, after which Copilot can submit an approving review satisfying a required-approval rule as a teammate's would; the approval is dismissed if new commits are pushed afterwards.

Some file types are excluded from review: dependency management files such as `package.json` and `Gemfile.lock`, log files, and SVG files.

## Adoption & Ecosystem

The documentation describes four customization surfaces a review can draw on and distinguishes them by scope. `.github/copilot-instructions.md` holds repository-wide, always-on rules specific to Copilot; path-specific `*.instructions.md` files under `.github/instructions/` hold always-on rules scoped to certain paths or file types; [[DefinedTerm/agents-md]] at the repository root holds always-on rules meant to be shared across AI tools and agents; and skills under `.github/skills/` hold task-specific workflows run on demand or automatically when relevant. GitHub summarizes the distinction as "Copilot, always know this for this repository" against "Any agent, always know this" against "Do this when needed".

Repository-level [[DefinedTerm/agent-skills]] and [[DefinedTerm/model-context-protocol]] servers can both be used during a review when relevant. The documentation states that Copilot reads custom instructions, agent instructions and skills from the head branch rather than the base branch, so changes to them can be tested in the same pull request that introduces them. It also describes what makes skill and MCP use more likely — review-focused skill directory names, custom instructions that reference MCP context, and pull request descriptions carrying identifiers such as issue keys or incident IDs. The GitHub MCP server and Playwright MCP server are enabled by default, repository MCP configuration applies to both the cloud agent and code review, and a repository setting allowing MCP tools during review is on by default and can be disabled for review alone. Copilot Memory, in public preview for Copilot Pro, Pro+ and Max plans, lets Copilot store details learned about a repository and use them when reviewing.

GitHub positions GitHub Code Quality as a complement rather than an alternative: where code review looks at the changes in a pull request, Code Quality adds rules-based CodeQL-powered analysis on pull requests and the default branch, test-coverage metrics, one-click Copilot-powered fixes including delegation to the cloud agent, and optional merge gating through rulesets.

Usage is metered in AI credits, and the documentation gives the cost as having two components — credits for the model interaction and Actions minutes for the agentic capabilities. It does not publish a fixed price for a review, giving instead estimated ranges that it says may change as models evolve, and notes that consumption generally rises with pull request size and with repository custom instructions. Attribution follows who asked: automatic reviews are attributed to the pull request author, a manually requested review to the requester, and for pull requests authored by the cloud agent, first to the human co-author and otherwise to the organization. Where access has been granted to users without a Copilot license, their consumption is billed directly to the organization or enterprise rather than against any individual budget. Under Copilot Business and Copilot Enterprise, reaching a user-level budget or exhausting an enterprise or cost-center spending limit blocks code reviews along with other credit-consuming features.
