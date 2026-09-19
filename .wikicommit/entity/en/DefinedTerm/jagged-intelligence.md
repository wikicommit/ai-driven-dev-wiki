---
title: "Jagged intelligence"
type: "schema:DefinedTerm"
lang: en
tags: [llm, terminology, evaluation, human-oversight]
sources:
  - type: url
    url: 'https://karpathy.bearblog.dev/sequoia-ascent-2026/'
    hash: sha256:5f0fc28c7d2ce3663820af50aba485b5ec93384a47528a92d2935967dd678dc4
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Andrej Karpathy's term for the uneven capability profile of large language models — brilliant in some domains and bizarrely weak in adjacent ones — which he attributes to two things at once: whether a task can be automatically verified, and how much attention frontier labs paid it in training."
---

Jagged intelligence is Andrej Karpathy's term for the way a large language model's capability
spikes in some places and collapses in others rather than rising smoothly. His first explanation is
verifiability: traditional software automates what you can specify, while this generation of models
automates what you can verify, because labs train them in large reinforcement-learning environments
with verification rewards. Tasks with an automatic success signal — maths, code, tests, benchmarks,
games — are resettable, repeatable and rewardable, so models practise them and improve quickly,
while everything outside that space stays rough. He offers this as the reason coding agents feel so
much better than ordinary chatbot use: coding gives the model feedback, in tests that pass or fail,
programs that run or crash, diffs that can be inspected.

Verifiability alone, on his account, is not the whole story. Capability also depends on whether a
domain was emphasised during pretraining, post-training, synthetic data generation and
reinforcement learning — on what the labs chose to care about. He writes the combination as a rough
formula in which a capability spike goes with verifiability multiplied by training attention, data
coverage and economic value, and offers chess as the illustration: when model chess ability jumped,
he argues, that was plausibly not general intelligence improving smoothly everywhere but a large
amount of chess data entering the training mix. His summary is "verifiable plus labs care".

## Usage

The consequence he draws is that a frontier model arrives without a manual. It is an artifact of
pretraining mixtures, RL environments, benchmark pressure, product priorities and economic
incentives, so the practical question for anyone building on it is whether their task sits on the
model's rails. Inside a region that is both verifiable and heavily trained, the model may fly;
outside it, it may fail in surprisingly basic ways, and the answers he names are better context,
tools, fine-tuning, one's own evaluations, or one's own reinforcement-learning environment. He
illustrates the gap with a model that can refactor a very large codebase or find zero-day
vulnerabilities while advising someone to walk fifty metres to a car wash rather than drive the car
being washed.

For founders he turns the same analysis into an opportunity: domains that are valuable and
verifiable but undertrained by the frontier labs. Where a domain-specific environment can be built
in which models try actions and receive reliable rewards, he argues fine-tuning or reinforcement
learning can lift performance even where the base model is not already strong — and that the
obvious domains, coding and maths, are already heavily targeted. He adds the caveat that almost
anything can be made verifiable to some degree, even writing (his example being a council of model
judges), so the distinction is one of difficulty rather than of kind.

Jaggedness is also his argument for keeping a person involved: so long as models behave this way,
he says, they have to be treated as tools with someone in the loop and in touch with what they are
doing. He connects this to a separate framing of his — that these systems are not animals with
drives and curiosity but statistical simulations shaped by training and incentive — on the grounds
that anthropomorphic expectations lead people to expect a smooth mind where there is a jagged one.

## Related Terms

[[DefinedTerm/software-3-0]], [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/behavioral-evaluation]], [[DefinedTerm/llm-as-a-judge]]
