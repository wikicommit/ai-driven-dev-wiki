---
title: "TOI"
type: "schema:SoftwareApplication"
lang: en
tags: [code-generation, platform-engineering, coding-tools]
sources:
  - type: url
    url: 'https://toss.tech/article/52885'
    hash: sha256:e856fa940d5aebd5b630258f50c137d6ab0362f88e157ef8793d464a0625b252
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An internal platform at Toss for building admin tools, on which a user registers the APIs a tool needs and then describes the screens they want in natural language, with a model generating React code against the registered schemas and the platform supplying both the security policies and a browser-based runtime that renders the result."
  applicationCategory: "Internal admin-tool building platform"
  featureList: "API registration with proxied calls and automatic call logging; per-API policies for personal-information masking, download encryption and access-reason capture; natural-language screen requests generating React against registered request/response schemas; in-browser build over a layered virtual file system; prebuilt package combinations supplied through an import map"
---

TOI is an internal platform at Toss for building admin tools. A user registers the APIs their tool
will call, then describes the screens they want in natural language; a model generates React code
using the request and response schemas of those registered APIs as its reference. It is described
in [[BlogPosting/from-ai-generated-code-to-admin]], which reports that it was opened inside the
company in February 2026.

The problem it addresses is given as repetition and cost. Many teams at Toss build and revise admin
tools, and each one previously repeated the same development, security and deployment work —
scaffolding a project, choosing a build tool, adding authentication, configuring deployment, and
then the requirements peculiar to an admin tool: masking personal information, capturing a stated
reason for a lookup, encrypting downloaded files.

TOI splits that work in two. Policy belongs to the platform: calls to a registered API pass through
the TOI server on their way to the original one, a record of the call is kept automatically, and
per-API settings are applied in transit, while the security policies that are mandatory are
applied automatically. The screens — drawing the table, attaching filters, linking through to a
detail page — are what the model writes.

## Capabilities

The part the source describes in most detail is the runtime that makes generated code appear as a
working screen, which runs in the user's own browser.

- **A layered virtual file system.** A browser has no project file system for a bundler to resolve
  import paths against, so TOI supplies one: four layers, ordered by ownership and rate of change —
  the current page's code as the model generated or the user edited it, code shared across a
  project's pages, preview shell templates, and the preview runtime itself — queried front to back so that the first layer holding
  a path wins and the bundler sees a single file system.
- **Building in the browser.** The bundler is a WebAssembly build of esbuild, chosen because it
  runs in the browser as-is and because its plugin interface allows file lookups to be intercepted
  and answered from the virtual file system. TypeScript and JSX are converted and local imports
  bundled into one ESM bundle, with the work moved off the main thread into a web worker. An import
  that resolves neither to a local file nor to a registered package fails the build.
- **Packages supplied through an import map.** Third-party packages are left out of the bundle and
  connected at run time through the browser's import map, which maps a bare specifier such as
  `react` to a prebuilt file.
- **Package combinations rather than packages.** The source's reasoning is that dependencies do not
  divide cleanly one package at a time — bundling a package separately can embed its own copy of a
  shared dependency, so an app and a library end up with different instances of something that has
  to be a singleton. TOI therefore treats a project's whole dependency set as one unit, identified
  by hashing the sorted list of public entry points together with the lockfile, and records that
  hash as a custom field in `package.json`. A combination is prepared by really installing it in an
  empty workspace, so that peer-dependency resolution and version-conflict checks remain the
  package manager's work, then built for the browser and uploaded along with its import map.
  Projects sharing a combination share the hash, so an existing build is reused rather than
  repeated.
- **Whole-document replacement instead of hot module replacement.** Each successful build produces
  a fresh HTML document and the iframe is swapped entirely, so no DOM, component state or module
  global survives from the previous version. The source presents this as giving preview updates the
  character of a transactional commit: a bundle that fails to run is not committed, the last
  version that ran stays on screen, and an error overlay is shown above it.

The source reports time to first preview as 1.3 seconds after this runtime was built.

## Adoption & Ecosystem

In the six months between its internal release in February 2026 and August 2026, the source
reports that 439 projects, and 2,418 pages beneath them, were created on the platform.

The runtime described above is the third design the team tried, and the source is organized around
why the first two were abandoned. A dev server on a server, shown through an iframe, handled live
updates easily and suited a proof of concept, but did not separate execution per user — a compile
error raised by one person editing one page put an error overlay on the screens of others editing
different pages. Moving execution into each user's browser with CodeSandbox's Sandpack fixed the
isolation but took 47 seconds to show a first preview, because it fetched every declared package
when rendering began; the company's private packages also needed an authenticating proxy that
rewrote tarball URLs recursively through the dependency graph, and the sandbox's separate-origin
iframe raised its own cross-origin and private-network-access problems.

Nothing in the final system is novel on its own — the source names the browser's own import map as
what connects packages, and credits the dependency resolution to an ordinary package manager — and
the author presents that as the point: the work was selecting and combining existing tools against
the product's requirements. The conclusion drawn is about where engineering effort sits once
generating code is cheap: making the platform guarantee the policies an admin tool must observe,
and designing a structure in which generated code can be run safely.
