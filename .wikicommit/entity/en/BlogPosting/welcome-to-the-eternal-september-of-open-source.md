---
title: "Welcome to the Eternal September of open source. Here’s what we plan to do for maintainers."
type: "schema:BlogPosting"
lang: en
tags: [open-source, ai-generated-contributions, maintainers]
sources:
  - type: url
    url: 'https://github.blog/open-source/maintainers/welcome-to-the-eternal-september-of-open-source-heres-what-we-plan-to-do-for-maintainers/'
    hash: sha256:c1bafd4aa912256b3554c364a09e4a2ec4b6c944adcf4554fd75d4b281e8767d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A GitHub blog post arguing that generative AI has pushed open source into an Eternal September — contributions are cheap to create but not to review — and setting out what GitHub has shipped and is exploring to help maintainers cope."
  author: ["Ashley Wolf"]
  datePublished: "2026-02-12"
  publisher: "[[Organization/github]]"
---

A post on GitHub's blog, published on February 12, 2026 and updated the following day, by GitHub's
Director of Open Source Programs. It borrows the Usenet-era term Eternal September to describe the
present state of open source (see [[DefinedTerm/eternal-september]]): collaboration runs on trust,
trust used to be protected by the friction of contributing, and generative AI has removed much of that
friction, so that a pull request, issue or security report can be generated in seconds while the cost
of reviewing it has not dropped.

The post is careful to say that most contributors act in good faith and that noisy inbound is not new;
the problem it identifies is volume that grows faster than maintainers' review capacity. It then lists
what [[Organization/github]] has shipped and is exploring for maintainers, surveys approaches the
community is building itself, and argues that the answer is better signals and tools rather than walls.

## Key Points

- Friction is framed as a balancing act: too much keeps people and ideas out, too little strains the
  trust open source depends on. The pull request and "Good First Issues" lowered friction, which the
  author calls a good thing.
- The cost to create a contribution has dropped with generative AI but the cost to review it has not;
  when volume outpaces review capacity, even well-intentioned submissions can overwhelm maintainers.
- The author argues low-quality or "AI slop" contributions are not a new phenomenon, citing the Linux
  kernel's web-of-trust philosophy and Developer Certificate of Origin, Mozilla's and GNOME's formal
  triage systems, and earlier waves of automated scanner reports.
- The imbalance the post identifies is one of benefit: the contributor may get the credit, the CVE or
  the visibility, while the maintainer gets the maintenance burden. It cites curl ending its bug bounty
  after AI-generated security reports surged, Ghostty moving to invitation-only contribution, and
  projects adopting explicit rules on AI-generated contributions as rational responses.
- Features GitHub says it has shipped include repository-level controls to limit pull request creation
  to collaborators or disable pull requests, pinned comments on issues, banners discouraging "+1"
  comments, faster pull request diffs and issue navigation, and temporary interaction limits; deleting
  pull requests from the UI is described as coming soon.
- Directions GitHub says it is exploring with maintainers are criteria-based gating, such as requiring
  a linked issue before a pull request can be opened, and improved triage tools that might use
  automated triage to check contributions against a project's own guidelines such as
  `CONTRIBUTING.md`. The post says these should support decisions, not replace them, and that the
  controls are optional because restrictions can fall hardest on good-faith first-time contributors.
- Community responses cited include invitation-only workflows, custom GitHub Actions for contributor
  triage and reputation scoring, the [[SoftwareApplication/vouch]] trust-management project, and
  education and onboarding work in communities such as Python and Kubernetes.
- The author argues against building only blocks and bans — "a fortress, not a bazaar" — and says
  GitHub wants to surface non-code contributions such as issue triage and documentation as trust
  signals, pointing to WordPress's "props" credit as a model.

## Context

The post is written from GitHub's position as a platform vendor and describes GitHub's own product
roadmap; its list of shipped features and explored directions is GitHub's account of its own work. It
opens a community discussion to gather maintainers' feedback. The explicit rules on AI-generated
contributions it mentions are the subject of [[DefinedTerm/ai-contribution-policy]].
