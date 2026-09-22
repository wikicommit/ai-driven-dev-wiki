---
title: "ループエンジニアリング実践：プロンプトチューニングをClaude Codeに任せてみた"
type: "schema:BlogPosting"
lang: en
tags: [loop-engineering, agentic-coding, prompt-engineering]
sources:
  - type: url
    url: 'https://techblog.zozo.com/entry/loop-engineering-prompt-tuning'
    hash: sha256:880fb71e74e5d9aa9b6c299e1c29e88f42a7f80015910db287c39b2a378226b4
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A worked example of loop engineering: the author decomposes a prompt-tuning loop previously run by hand for a vision-language model into Claude Code sub-agents, one per step, and reports the result across three tasks. Its design idea is to read the F1 score as a loss and the model's own stated reasoning as a gradient, and an ablation compares withholding that reasoning against supplying it."
  author: "大川"
  datePublished: "2026-08-25"
  publisher: "[[Organization/zozo]]"
---

The post is explicit that it is not proposing a new optimization algorithm. Its question is narrower and, the author argues, more useful: can the prompt-tuning process a person was already running by hand be reproduced by a loop ([[DefinedTerm/loop-engineering]]) an agent drives, and how much faster does it reach the same accuracy? The loop being moved is the familiar one — run inference and compare against ground truth, open the wrong samples and look at the model's output, its stated reasoning and the image, work out why it was wrong, rewrite the prompt's definitions or examples, re-evaluate, and record what helped and what hurt — repeated once per fashion attribute, which the author reports could consume weeks per project.

The decomposition is one-to-one and deliberately so. Each of the five steps the author had been performing is assigned a component of a Claude Code skill invoked as `/tune`, four of them sub-agents and one a plain script: an analyzer that looks at the failures, a planner that identifies the mismatch between the definition and the judgment, an improver that rewrites the prompt, an evaluation script that recomputes F1, and a retrospector that appends what worked and what did not to a lessons file. The author presents the lessons file as the deliberate reproduction of a human tuner's accumulating memory, and the skill's own `SKILL.md` as an orchestrator that does nothing but drive the loop — 115 lines, with the substance delegated to the agent files — alongside a single policy file that every sub-agent follows for improvement priorities, accept/reject decisions and stopping conditions.

Underneath the decomposition is the framing the post is built around. The author maps F1 onto a loss (a scalar saying how far off you are) and the model's stated reasoning onto a gradient (which direction to move), which makes the loop a gradient descent over the prompt as parameter. The post notes the same idea appears in existing research on using an LLM's output as a self-improvement signal, and is careful to present the design as an application of that idea rather than as the author's own.

## Key Points

- The stated goal is transplanting a human procedure rather than inventing an algorithm: the author's advice from the experience is that agent design should start by breaking down how you were solving the task yourself and putting that directly onto the agent, and the post reports the design was not right at the outset but accreted its lessons and strategy files as the loop was run.
- F1 is treated as the loss and the model's reasoning as the gradient, with the prompt as the parameter being updated. This requires the inference step to emit the reasoning alongside the extracted attributes as structured output, which the author states is what makes the signal available at all.
- The ablation is the post's own test of that framing, on one task: supplying the reasoning to the optimizing model (condition A) versus withholding it (condition B). Withholding it produced the higher training score (0.8513 at iteration 7 against 0.8403 at iteration 3), but the test score diverged: A reached 0.8641, while B stood at 0.7983 on test at that same best-training iteration (its own best test score, 0.8494, came earlier). The author reads this as B overfitting the training set, attributing A's advantage to the reasoning letting the optimizer see more of how the vision-language model was thinking.
- On the one task with a hand-tuned baseline, the automated loop reached leaf F1 0.8403 on train and 0.8641 on test against the human's 0.8165 and 0.8473, starting from an initial prompt that merely enumerated the attribute definitions with no prompt engineering at all. The author notes the human side had both more information and more attempts available (around 30 iterations, plus domain knowledge) and still did not come out ahead, which is offered as a suggestion that such a loop can substitute for the human work.
- Effort is reported at two granularities and the distinction matters: one tuning cycle went from about 6 hours to about 2.5 hours (roughly 2.4x), while the full evaluation cycle — tuning, qualitative review by a domain expert, and feeding back the result, repeated up to three times — went from about 3.5 weeks to about one week (roughly 3.5x). The author explains the larger figure as reflecting both fewer iterations and the scheduling and waiting time around the domain expert, and states the numbers are measured.
- Across three tasks with different schema structures leaf F1 improved in every case and no task degraded on test. The author reads the largest training gain (+34.3% on one task) as reflecting an unusually low training baseline rather than an unusually good result, and interprets that gap against the same task's much higher test baseline as difficult samples being concentrated in the training split.
- Stopping is defined rather than left open: the loop halts at whichever comes first of all feature and leaf F1 reaching 0.7, ten iterations, or three consecutive iterations of convergence (leaf F1 improving by less than 0.005 with no change in the number of improved leaves).
- Reported cautions from running it: the prompt grew steadily longer as accuracy rose, and the author names overfitting as what was watched most closely, recommending that train and test splits be prepared at minimum; and because each loop runs inference over every image, API charges accumulate, with a badly designed loop capable of continuing to run inference on the backend and driving costs up unexpectedly.
- The author states the results are a single run with no repeated executions, so run-to-run variance is not assessed, and lists comparison against existing frameworks such as DSPy, raising the sample count, and generalizing the approach into an internal tool as future work.

## Context

The post is a concrete instance of the shift this wiki records under [[DefinedTerm/loop-engineering]] — from writing a good prompt to designing the loop that prompts the model — and the author states it in those terms, describing the field's attention as having moved up a level from prompts to the design of the mechanism that drives the agent, and defining a [[DefinedTerm/agent-harness]] as everything around the model other than the model itself.

It also sits beside this wiki's other material on agent-driven self-improvement, with the distinguishing feature that the thing being improved is a prompt for a separate model: the optimizing agent is Claude Code while the model under test is Gemini, so the reasoning being read as a gradient comes from a different system than the one doing the rewriting. The author positions this work as a step beyond earlier work of their own on guarding the correctness of a model's output, aimed this time at the accuracy itself.
