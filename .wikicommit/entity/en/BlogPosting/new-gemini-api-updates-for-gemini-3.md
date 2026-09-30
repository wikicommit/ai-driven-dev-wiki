---
title: "New Gemini API updates for Gemini 3"
type: "schema:BlogPosting"
lang: en
tags: [llm, tool-use, prompting]
sources:
  - type: url
    url: 'https://developers.googleblog.com/new-gemini-api-updates-for-gemini-3/'
    hash: sha256:5c0c9a076fa04762c9220c98f1a90a42776dffeff714891ebb38383da16fa94f
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A Google for Developers blog post describing the changes made to the Gemini API to support Gemini 3 — new controls for reasoning depth and media processing, enforced thought signatures, and hosted tools combined with structured outputs — followed by prompting best practices for Gemini 3 Pro."
  author: ["Shrestha Basu Mallick", "Philipp Schmid"]
  datePublished: "2025-11-25"
  publisher: "[[Organization/google]]"
---

The post, on the Google for Developers blog, accompanies Gemini 3's availability to developers
through the [[SoftwareApplication/gemini-api]]. It describes Gemini 3 as Google's most intelligent
model and says that several API updates were rolled out to support its reasoning, autonomous coding,
multimodal understanding and agentic capabilities. The stated aim of the changes is to give developers
more control over how the model reasons, how it processes media, and how it interacts with the outside
world.

The first half lists what is new in the API; the second gives recommendations for getting the best
results from Gemini 3 Pro, which the post calls Google's most advanced model for agentic coding, and
points to a System Instructions template that Google's research team created for it and that the post
says improved performance on several agentic benchmarks.

## Key Points

- A new `thinking_level` parameter controls the maximum depth of the model's thinking before it
  responds. Gemini 3 treats the levels as relative guidelines for reasoning rather than strict token
  guarantees; the post suggests "high" for complex tasks such as strategic business analysis or
  scanning code for vulnerabilities, and "low" for latency- and cost-sensitive work such as structured
  data extraction and summarization (see [[DefinedTerm/reasoning-effort]]).
- A `media_resolution` parameter sets how many tokens are used for image, video and document inputs,
  per media part or globally, trading visual fidelity against token usage and latency; if it is left
  unspecified, the model uses defaults based on the media type.
- Starting with Gemini 3, the API enforces the return of [[DefinedTerm/thought-signature]]s, encrypted
  representations of the model's internal thought process that keep its chain of reasoning intact
  across a conversation. Function calling validates them strictly on the current turn and image
  generation or editing for all model parts, both answering a missing signature with a 400 error;
  text and chat generation does not enforce them strictly, but omitting them degrades reasoning and
  answer quality. The official SDKs with standard chat history handle them automatically.
- Gemini's hosted tools — specifically Grounding with Google Search and URL context — can now be
  combined with structured outputs, which the post presents as useful for agents that fetch live
  information from the web and extract it into a precise JSON format.
- Pricing for Grounding with Google Search moves from a flat per-prompt rate to a usage-based rate
  per search query.
- The prompting recommendations for Gemini 3 Pro are Google's own: keep temperature at its default of
  1.0; keep a uniform prompt structure and define ambiguous terms; ask explicitly for a more
  conversational answer, since the model is by default less verbose; treat text, images, audio and
  video as equal-class inputs; put behavioral constraints and role definitions in the system
  instruction or at the top of the prompt; and for long contexts, put the specific instructions at the
  end, after the data.

## Context

The post is a vendor announcement written for developers adopting the new model, and each change it
describes is framed around agentic use: thought signatures as critical for multi-step agentic
workflows, grounding combined with structured outputs as a building block for agents, and the pricing
change as better supporting dynamic agentic workflows. It names vibe coding among the uses it reports
wide excitement for with Gemini 3 Pro, alongside zero-shot generation, mathematical problem solving and
complex multimodal understanding. It directs readers to the Gemini 3 documentation and developer guide
for implementation details.
