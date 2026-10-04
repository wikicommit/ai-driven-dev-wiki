---
title: "Codecall"
type: "schema:SoftwareApplication"
lang: en
tags: [tool-use, mcp, agents, sandboxing]
sources:
  - type: url
    url: 'https://github.com/zeke-john/codecall'
    hash: sha256:088c8dadf1684aa880483ee2f14fc8310b9d0a31d04e019dd85036137dbae151
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5"
generated_with: "0.9.0"

properties:
  description: "An open-source TypeScript implementation of programmatic tool calling for AI agents, which gives the model two tools — readFile and executeCode — and a file tree of TypeScript SDK files generated from MCP servers, so the agent writes code that orchestrates the tools in a Deno sandbox instead of calling them one at a time."
  applicationCategory: "Agent tool-calling framework"
  featureList: "readFile and executeCode as the only agent tools; TypeScript SDK files generated from MCP tool definitions; progressive tool discovery through an SDK file tree; Deno sandbox execution with an IPC tool proxy; progress streaming; full stack traces on error; learned-constraint annotations written back to SDK files"
---

Codecall is an open-source TypeScript implementation of [[DefinedTerm/programmatic-tool-calling]] for AI agents, released under the MIT license. Instead of exposing every tool definition to the model and having it make one tool call per inference, it lets the agent write TypeScript that calls the tools like an API and runs that code in a sandbox, so that several tool operations happen in one execution and only the result returns to the model's context.

Its README frames the motivation as four problems with conventional tool calling: every tool definition is sent with every request, so schema tokens grow with the number of tools and the number of turns; each tool operation costs a full inference round-trip that resends the growing conversation; independent operations run one at a time with reasoning in between; and models are unreliable at looking things up in large datasets held in context, where a line of code filtering the data is deterministic. Its answer is to let models do what the README says they are good at — writing code — on the grounds that their training data holds a great deal of real-world TypeScript. The README lists Cloudflare's "code mode" write-up and Anthropic's posts on code execution with MCP and on advanced tool use among the ideas it builds on (see [[DefinedTerm/code-execution-mcp]]).

## Capabilities

The agent is given only two tools, `readFile` and `executeCode`, and a system message containing a directory tree of SDK files — one per available tool — but not their contents, so it discovers tools progressively by reading only the files a task needs. The README argues this keeps a 30-tool setup at about the same base context as a 5-tool one, with only the file tree growing (compare [[DefinedTerm/progressive-disclosure]]). The model still decides what to read, what code to write, when to run it and how to respond.

The SDK files are generated ahead of time from connected [[DefinedTerm/model-context-protocol]] servers. Codecall reads each tool's input and output schemas, descriptions and annotations, has an LLM convert the JSON Schema definitions into typed TypeScript files with doc comments, groups them into folders by server namespace, and saves them for the agent to read. It connects to MCP servers over stdio or HTTP.

`executeCode` runs the model's code in a fresh, short-lived Deno sandbox that by default has no access to the filesystem, network, environment variables or system processes; the only way out is the injected `tools` object. That object is a proxy: a call such as `tools.namespace.method(args)` is sent as a JSON message over the sandbox's standard output to the host process, whose tool registry routes it to the right MCP server or internal function, and the result comes back on standard input to resolve the waiting promise, so from the code's point of view it is an ordinary async call. A `progress()` function streams step-by-step updates to the user while a script runs. On failure, the model gets the full stack trace, and undefined values from bad property access are caught as errors.

Codecall also writes what agents learn back into the SDK files. When an agent recovers from a tool error — the README's example is a task-search tool that rejects a call with no filter — it adds a "learned constraint" banner at the top of the SDK file that misled it, so that the next agent reading that file writes correct code from the start. The README argues this matters more for code-based calling than for conventional calling, because one wrong assumption about a tool's input or output fails the whole script.

## Adoption & Ecosystem

Running it requires Node.js, Deno for the sandbox, and an OpenRouter-compatible API key. The repository includes a demo MCP server with 18 user-management tools and a conventional agent that exposes the same tools directly, so the two approaches can be compared side by side on the same task. Its roadmap lists a confirmation prompt, with a stated reason, before destructive tools run inside a script, fuller documentation and an npm package as not yet done.
