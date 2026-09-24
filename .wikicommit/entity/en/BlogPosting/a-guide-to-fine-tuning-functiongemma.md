---
title: "A Guide to Fine-Tuning FunctionGemma"
type: "schema:BlogPosting"
lang: en
tags: [agents, tool-use, llm]
sources:
  - type: url
    url: 'https://developers.googleblog.com/a-guide-to-fine-tuning-functiongemma/'
    hash: sha256:04fc7d0d05af957da0b49f748286546b544a53c9541dea52a2541b70e8f5dda3
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Google DeepMind tutorial on fine-tuning FunctionGemma, a small function-calling model, so that it chooses between similar-looking tools according to an organization's own policy, together with a no-code demo tool for doing the same."
  author: ["Juyeong Ji"]
  datePublished: "2026-01-16"
  publisher: "[[Organization/google]]"
---

This post, from the AI DevX team at Google DeepMind, is a tutorial on adapting FunctionGemma — which it describes as a version of Google's Gemma 3 270M model fine-tuned specifically for function calling, released the month before — to the tool-calling rules of a particular organization. Its framing is that tool calling is what turns natural language into executable actions for an agent, and that a generic model does not know a business's own rules about which tool should handle which request.

The problem it targets is tool-selection ambiguity: choosing between two or more functions that look similar. Its case study trains the model to route questions between an internal knowledge-base search and a public web search, so that a question about the company's travel reimbursement limit goes to the internal documents rather than to Google. It then introduces the FunctionGemma Tuning Lab, a demo on Hugging Face Spaces that runs the same process without writing training code.

## Key Points

- Three reasons are given for fine-tuning a model that already supports tool calling: resolving which of several similar tools should be selected, specializing in niche tasks or proprietary formats absent from public data, and distillation — using a large model to generate synthetic training data for a smaller, faster one.
- In the case study, the base FunctionGemma model evaluated on the `bebechien/SimpleToolCalling` dataset is described as performing suboptimally: it chose the wrong tool, or offered to "discuss" a policy instead of calling a function.
- The case study used a 50/50 train-test split rather than the 80/20 the post calls standard for production, chosen to show the improvement on a large volume of unseen data.
- The post's main caution concerns data order: shuffling was disabled because that dataset was already shuffled, but on data sorted by category the same setting would train the model on one tool and test it on the other. Its recommendation is to pre-mix custom data, or set `shuffle=True` when the order is unknown.
- After supervised fine-tuning with Hugging Face TRL's `SFTTrainer` for 8 epochs, the model is described as adhering strictly to the enterprise policy — for example, calling the knowledge-base search for a question about creating a new Jira project. The post shows the training-loss curve but reports no accuracy figure.
- The FunctionGemma Tuning Lab is presented as a no-code interface: function schemas defined as JSON in the UI, training data uploaded as a CSV of prompts, tool names and arguments, learning rate and epochs set by sliders, live loss curves, and an automatic evaluation before and after training. It can also be downloaded and run locally.
- All of the above is Google's own account of its own model and tooling, written as a tutorial rather than as an evaluation.

## Context

The post sits on the model side of [[DefinedTerm/agentic-tool-use]]: rather than changing how tools are described to an agent, it changes the model so that it picks the right one. It presents the result as turning a generic assistant into a specialized agent that follows strict business logic, and closes by pointing to Google's technical guide on fine-tuning FunctionGemma and to a separate guide on fine-tuning it for mobile actions.
