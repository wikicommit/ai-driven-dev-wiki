---
wikicommit:
  # Do not write pages about living individuals. With this on, /wikicommit-generate's
  # entity-extraction pass drops such an entity as `action: exclude` with
  # `exclude_reason: privacy`, automatically and without asking — the same way an
  # off-`theme` entity is dropped. Off by default: leave it `false` and every entity is
  # generated as before, exactly as an empty `theme` disables the relevance judgment.
  # Whether someone is living is judged by the LLM, as `theme` is: the switch is
  # configuration, the judgment is not. Exceptions go in the prose below, not here.
  exclude_living_persons: true
---

Do not write a page about a living individual. The switch above already drops them, and it
is on deliberately: the people who coined the terms this wiki covers are living public
figures at the centre of its subject, and there is no exception for them here. What they
said and built belongs on the pages for those terms, tools and papers, attributed to them
in the body text, rather than on a page about the person.

Do not write a page about a real individual who is not a public figure, whether living or
not. Authors listed on a paper, members of a named project team, and people quoted in
passing are named by a source without being its subject.

Do not write a page about a real minor.

Do not write a page about a matter under dispute or an incident still unfolding -- a
lawsuit, a licensing conflict, a security investigation still open. These are Event-shaped,
so the switch above never reaches them. Write the settled outcome once there is one.

Do not write a page about unreleased information belonging to whoever runs this wiki:
unannounced products, internal roadmaps, unpublished results.

Nothing else here is narrowed. Organizations, software, papers, datasets, techniques and
terms are this wiki's subject matter, and this file withholds none of them.
