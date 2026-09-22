---
title: "AI가 만든 코드가 어드민이 되기까지"
type: "schema:BlogPosting"
lang: en
tags: [coding-tools, code-generation, platform-engineering]
sources:
  - type: url
    url: 'https://toss.tech/article/52885'
    hash: sha256:e856fa940d5aebd5b630258f50c137d6ab0362f88e157ef8793d464a0625b252
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An account of how Toss's internal admin-building platform runs AI-generated React code in the user's own browser, after a shared dev server and a third-party browser sandbox each proved unworkable, and of what the engineering effort turned out to consist of once code generation itself was handled by a model."
  author: "이현재"
  datePublished: "2026-09-04"
  publisher: "토스테크 (Toss Tech)"
---

This post describes the execution environment behind [[SoftwareApplication/toi]], an internal
platform at Toss on which teams build admin tools by registering the APIs they need and then asking
in natural language for the screens they want, with a model writing the React code against the
registered request and response schemas. Its subject is not the code generation but what has to
exist around it: the author's framing is that generating code was never sufficient, because
real-time generated code only becomes a product once there is somewhere to run it and show it.

The post divides an admin tool into policy and screen. Policy — call logging, personal-information
masking, encryption of downloaded files, capturing a stated reason for looking data up — is handled
by the platform, which proxies every registered API call and applies those settings in passing.
Screens are what the model writes. The narrative then follows two failed approaches to running that
generated code and the design that replaced them, closing with an argument about where engineering
effort now sits when code itself is cheap to produce.

## Key Points

- The platform's own scale is reported by its authors: opened internally in February 2026, it had
  accumulated 439 projects and 2,418 pages under them by August 2026.
- A shared server-side dev server, shown to users through an iframe, was workable for a proof of
  concept but not for multiple users: because the execution environment was not separated per user,
  a compile error raised by one person editing one page produced an error overlay on other people's
  screens too.
- Moving execution into each user's browser with a third-party sandbox isolated users successfully
  but introduced a different problem — the first preview took 47 seconds, because the sandbox
  downloaded every declared package at render time.
- Private internal packages compounded that: authentication could not be exposed to the browser
  runtime, and proxying metadata requests alone was insufficient because the tarball URL inside the
  metadata pointed back at the original registry, so it had to be rewritten too, recursively down
  the dependency graph.
- The team's replacement runs the build in the browser itself over a virtual file system, layered
  in four tiers — the current page's code, project-shared code, preview shell templates and the
  preview runtime — searched front to back so that the bundler sees one file system.
- Packages are removed from the bundle and supplied through the browser's own import map, prebuilt
  ahead of time rather than resolved at preview time.
- Dependencies are treated as combinations rather than individual packages, because bundling
  packages separately can give an app and its dependency two different instances of a shared
  singleton. A combination is identified by hashing the sorted list of public entry points together
  with the lockfile's own hash and keeping the first 16 characters, recorded as a custom
  `packageSetHash` field in `package.json`.
- The combination is built by actually installing it — creating an empty workspace, copying the
  project's `package.json` and running the package manager — which the author presents as the point:
  peer-dependency resolution and version-conflict checking stay the package manager's job instead
  of being reimplemented.
- Hot module replacement was rejected in favour of replacing the whole document on every build,
  partly because the bundler used offers no HMR and tracking the module graph would have to be
  built, and partly because a preview is looked at rather than interacted with, so preserving edit
  state buys little. The author notes that whole-document replacement makes each update behave like
  a transactional commit: a bundle that fails to run is never committed, so the preview keeps
  showing the last version that did run, with an error overlay above it.
- Time to first preview is reported as having gone from 47 seconds to 1.3 seconds, which the author
  attributes to moving work that had been repeated on every preview to the moment the package
  combination changes.
- The closing argument is that as the cost of producing code falls, what matters in building a
  product shows more clearly: here, guaranteeing the policies an admin tool must observe and
  designing a structure in which generated code can be run safely. The author notes that almost
  nothing in the system was built from scratch — the work was combining existing tools against the
  product's requirements.

## Context

The post is an engineering account from the team that built the platform, and its figures — the
project and page counts, the 47-second and 1.3-second measurements — are that team's own. It says
nothing about how well the generated screens work or how often they need correcting; its subject is
strictly the environment the code runs in.

Its closing move — treating the model's output as the part that has become cheap and the
surrounding system as where the remaining work is — is one this wiki records elsewhere; compare
[[BlogPosting/raising-productivity-floor-with-harness]]. A commenter endorses that conclusion from
their own experience, describing equivalent work to keep AI-generated frontend components inside a
design system's conventions and security policy, while another asks a question the post does not
answer, about what a team must do to connect a new backend to the platform.
