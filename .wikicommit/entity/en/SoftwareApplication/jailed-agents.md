---
title: "jailed-agents"
type: "schema:SoftwareApplication"
lang: en
tags: [sandboxing, coding-agents, security]
sources:
  - type: url
    url: 'https://www.codecentric.de/wissens-hub/blog/jailed-agents-beschraenke-den-systemzugriff-deiner-ai-coding-agents'
    hash: sha256:d6d6e424b61cdd2936acabe377c683576ffb6da03be7ce212691ebc30e88d906
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Nix-based tool that runs AI coding agents in a sandbox with restricted system access, sharing almost nothing with the host by default and granting access only through explicit whitelisting declared in a Nix package definition."
  applicationCategory: "Sandbox for AI coding agents"
  operatingSystem: "Linux, macOS, Windows"
  featureList: "Zero-trust sandbox with explicit whitelisting; declarative tooling through one Nix package definition; predefined configurations for several coding agents; custom agents built from the provided functions; jail.nix combinators for sharing host resources"
---

jailed-agents is a [[DefinedTerm/sandboxing]] tool built on the Nix ecosystem that runs AI coding
agents with restricted access to the system they run on. A codecentric blog post from September 2026
introduces it for developers who use coding agents and want to limit what those agents can reach on
their machines. Its core is jail.nix, a Nix wrapper for bubblewrap.

The problem it addresses, in the post's account, is that a coding agent run as an ordinary application
under the user's account gets access to every credential available to that user on the system. The
post wants agents placed in a dedicated environment with limited resources and limited access to the
outside world, while staying flexible enough that access to certain MCPs or other resources
can be allowed for one project and forbidden for another.

## Capabilities

- **Zero-trust sandbox**: by default it shares almost nothing with the host, and everything runs
  through explicit whitelisting.
- **Declarative tooling**: every access and every dependency is provided through the same Nix package
  definition.
- **Predefined configurations** for claude-code, codex, hermes-agents, opencode, pi and others, plus
  the ability to build custom agents with the functions the tool provides.
- **Combinators** from jail.nix supply the flexibility beyond passing through environment variables or
  sharing host folders — for example sharing the host's time zone, overriding the jail's hostname,
  sharing the host's camera, or running code before the agent starts.

The simplest invocation runs only the predefined packages; the post expects most users to customize a
jailed-agent package instead, which can be installed in a nix-profile, a flake, a devshell or
[devenv](https://devenv.sh/getting-started/). Because it builds on Nix, the post says it runs on any
Linux distribution, macOS or Windows.

## Adoption & Ecosystem

The post positions it as a compromise between the alternatives for sandboxing coding agents. VMs — for
example with firecracker — offer the best isolation but carry overhead and are less flexible, and the
effort of building a good workflow around them can be high; Docker could be an option but was never
designed for this use case, and restricting access with it means building extra images and configuring
extra access. Integrated into devenv, the tool can give every developer in a company the same secure
agent setup, and a jailed-agent package can be shared through a common repository or through a module
with shared defaults that each developer extends. The post concludes that it is lightweight and
reusable across developers.
