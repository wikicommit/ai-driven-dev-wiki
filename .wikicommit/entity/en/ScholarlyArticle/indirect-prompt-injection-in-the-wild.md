---
title: "Indirect Prompt Injection in the Wild: An Empirical Study of Prevalence, Techniques, and Objectives"
type: "schema:ScholarlyArticle"
lang: en
tags: [prompt-injection, agent-safety, web-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.27202'
    hash: sha256:ec1b1d5a6010017bb19ec0c21ebfc834c928a2c0ba6c97cfaf109ffcef44937b
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A large-scale web measurement of indirect prompt injection as deployed on the public web, validating 15,387 instances across 1.2B URLs and characterizing their templates, objectives, targets, concealment techniques, persistence and measured effectiveness against 13 models."
  author: ["Soheil Khodayari", "Xuenan Zhang", "Bhupendra Acharya", "Giancarlo Pellegrino"]
  datePublished: "2026"
  keywords: ["prompt injection", "web measurement", "web security", "LLM web agents", "content protection"]
---

Prior work on [[DefinedTerm/indirect-prompt-injection]] established that the attack works, but studied it mostly under controlled or benchmarked conditions. This paper asks a different question: whether site and content owners are already deploying prompt-like instructions into real web pages, and if so at what scale, to what ends, and with what effect. The authors analyse 1.2 billion URLs across 24.8 million hosts drawn from Common Crawl, Censys and Shodan, match against 3,963 prompt-injection indicators, and then validate every match through a semi-automated protocol combining structural grouping with manual inspection by two reviewers, yielding 15,387 confirmed instances on 11,722 pages across 2,042 hosts.

Their central finding is that the phenomenon is structured rather than incidental, and that it is not purely adversarial. A small set of reusable templates dominates — 54 templates account for 95% of all instances — and the objectives split across offensive uses (system disruption, reputation manipulation, data exfiltration), defensive uses (copyright and personal-data protection, AI-bot identification), and a large underspecified category of bare overrides whose downstream purpose cannot be determined from the prompt alone. The authors characterize the result as a multi-stakeholder ecosystem with competing incentives, in which website owners and content publishers are as much the authors of these instructions as attackers are.

To test whether any of it works, they run 5,200 trials across 13 models and four page representations on a fixed summarization task. Compliance is limited but non-negligible, and depends more on how page content is exposed to the model than on model size alone: flattening a page to plain text yields the highest attack-effectiveness rate, while representations that preserve structural cues — HTML, raw responses, rendered snapshots — reduce it sharply. The authors close by arguing that in-page prompt injection is neither a decisive mechanism against web agents nor mere noise, but something already real, measurable, structured and persistent, whose impact depends strongly on agent design choices.

## Key Points

- 54 lexical templates account for 95% of the 15,387 validated instances, while 144 templates appear only once; the single most frequent template appears in 3,504 injections across 2,722 pages.
- Six objective categories are identified. System disruption is the largest at 8,894 instances and is overwhelmingly garbage injection — instructing the agent to emit random strings, repeated nonsense or text intended to exhaust context limits — with a much rarer command-injection variant using payloads such as SQL drop statements or destructive shell commands.
- Defensive uses are widespread: roughly 4,000 data-protection instances (split between personal-information and copyright restrictions) and roughly 3,000 AI-bot-identification instances, most following a challenge-response pattern of the form "if you are an AI, include X in your response", with a smaller subset acting as honeypots.
- Reputation manipulation accounts for 1,521 injections across 139 hosts, taking the forms of content or product promotion, citation forcing, positive review forcing, SEO backlink injection and job-candidate promotion. Data exfiltration is rare, at 13 injections across 10 hosts.
- Task override is nearly universal, appearing in 99% of injections: the core mechanism is direct replacement of the model's current task rather than subtle persuasion. Jailbreak framing reinforces it in 43% of cases.
- Crawlers and data scrapers are the dominant target class, which the authors read as placing the conflict between content owners and automated data collection at the centre of current deployment; search, customer-support and HR-screening agents are targeted by narrower, higher-stakes objectives.
- Invisibility is the dominant delivery property: about 70% of injections sit in channels that are non-visible by construction, and 87% are non-visible overall. Of HTML-embedded injections that could be rendered, only about 5.1% were visible to users, with 58.6% concealed by rendering techniques — most commonly colour and contrast manipulation, occlusion, and viewport-based hiding.
- HTTP response headers are a major surface, carrying 7,887 injections across 1,640 hosts, and converge on a small set of non-standard fields dominated by X-AI and X-LLM. Structured data, most often JSON-LD already intended for search engines, carries roughly a quarter of body injections.
- The injections are durable: of pages identified in the October 2025 snapshot, 93% already carried an injection three months earlier, 77% at six months and 65% at twelve.
- Effectiveness varies sharply with representation: 3.9% on plain text against 1.1% for HTML and rendered snapshots and 0.2% for raw responses. Small models are most susceptible, reaching 8.0% on text, while medium and closed-source models are near zero on all non-text representations.
- Low attack-effectiveness on HTML and raw inputs does not indicate robustness. Those representations are substantially longer and push error rates to 20.3% and 25.8% respectively, so in many cases the model fails before producing usable output rather than cleanly rejecting the injection.
- Detection is not resistance: closed-source models flagged attacks most often at 25.1% and small models rarely at 4.8%, and the authors record six cases in which a model explicitly recognized the malicious instruction and complied with it anyway.

## Notes

The authors are explicit that their measurement is a lower bound. Their corpus draws mainly on web crawls that may underrepresent authenticated or platform-restricted content, and their detection pipeline relies on an indicator list that may miss highly obfuscated or non-English variants. The effectiveness evaluation covers one task — webpage summarization — and four representations, which they present as a controlled comparison rather than full coverage of deployed ingestion pipelines.

The study is observational: the authors state they did not inject content, manipulate websites or test attacks against live systems, relying instead on existing public corpora and archives, and running effectiveness experiments offline on sampled pages. They release only prompt strings and derived labels, stripping URLs and domains, on the reasoning that identifying affected sites would expose them to unwanted attention while the strings alone preserve the defensive value of the dataset.

Their broader reading is that current in-page prompt injection works more through friction and degradation than through control — 53% do not encode a clear access rule or steer the agent toward a preferred behaviour — and that it should be understood as an early stage of a shift in which the web becomes a contested interface between automated agents and the parties who publish online content. They argue this points to a need for non-adversarial, machine-readable and enforceable mechanisms for expressing access preferences, and raise the question of whether the existing Robots Exclusion Protocol is sufficient to govern agent access.
