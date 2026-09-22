---
source:
  type: url
  url: 'https://simonwillison.net/2026/Feb/7/software-factory/'
  hash: sha256:f037b61ef74329e98d22e3f5e86498585708d651d71581e420890095020b0ad3
  license:

schema:
status: partial
last_generated_at: "2026-09-22"
extracted_tokens: 3356
generated_pages:
  - .wikicommit/entity/en/BlogPosting/how-strongdms-ai-team-build-serious-software-without-even-looking-at-the-code.md
  - .wikicommit/entity/en/DefinedTerm/software-factory.md
  - .wikicommit/entity/en/DefinedTerm/digital-twin-universe.md
  - .wikicommit/entity/en/Organization/strongdm.md
  - .wikicommit/entity/en/SoftwareApplication/attractor.md
  - .wikicommit/entity/en/SoftwareApplication/cxdb.md
failed_pages: []
---

## Summary
Simon Willison writes up StrongDM's AI team's first public account of their "Software Factory":
non-interactive development in which specifications and scenarios drive agents, under the team's
stated rules that code must not be written by humans and must not be reviewed by humans. Most of
the post is about how they gain confidence without reading the code — scenarios kept outside the
codebase like a holdout set, a probabilistic "satisfaction" measure over observed trajectories, and
a Digital Twin Universe of agent-built behavioural clones of Okta, Jira, Slack and Google services.
He flags their stated $1,000-per-engineer-per-day token figure as the term that decides how far the
pattern generalises.

## Generation Notes
- "StrongDM": `coverage_gap_note` — the source dates and sizes the company's AI team (formed July 2025, three people) rather than StrongDM itself, and `Organization.md` has no `properties:` field for a subdivision's founding date or headcount, so both are recorded in the body only.
- "Simon Willison": excluded, `exclude_reason: privacy` — the post's author, a living individual, which `.wikicommit/entity-policy.md` rules out (`exclude_living_persons: true`); no page exists for him.
- "Jay Taylor": excluded, `exclude_reason: privacy` — a living member of the named StrongDM AI team, quoted for the Digital Twin Universe fidelity strategy; the policy rules out both living individuals and members of a named project team. No page exists for him.
- "Dan Shapiro": excluded, `exclude_reason: privacy` — a living individual, credited by the source with the "Dark Factory" framing; no page exists for him.
