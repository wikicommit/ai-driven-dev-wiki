---
title: "vibe coding"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/May/1/not-vibe-coding/'
    hash: sha256:4c658c9b0548d2a1a6e3cabefbb4299d17ce794ac693027d0c788262d01d7166
  - type: url
    url: 'https://arxiv.org/abs/2510.12399'
    hash: sha256:5588850efcf68bd17d3abbdd3e2b8bb1d25989fc40396cf8e62c31913ffe6ef5
  - type: url
    url: 'https://arxiv.org/html/2510.17842v1'
    hash: sha256:787bc8812aeedac3e0166895e837e88ea57a2a23b1f901c470f6e3acf40fce47
  - type: url
    url: 'https://en.wikipedia.org/wiki/Vibe_coding'
    hash: sha256:e6ad2ca6bfbdd4ebfd679daf1a568bb11aba4e0d833594d90a8bcb226803d272
  - type: url
    url: 'https://spectrum.ieee.org/vibe-coding'
    hash: sha256:87985edca59baa125c60b0a99580b29ea959acd84ea651630c63e35084899efa
  - type: url
    url: 'https://qiita.com/hoge_kawamuro/items/b35e91481a9fbfced2f8'
    hash: sha256:e303fc5e4381a6a466fe3dc6ad2721a26e0365999f4412409f115bb354b40445
  - type: url
    url: 'https://sddbook.blob.core.windows.net/downloads/spec-driven-development.pdf'
    hash: sha256:7f897827f00db69ac4a15f3acea3826e5504b1600d0b785cdce210d5414f1eea
  - type: url
    url: 'https://www.jfokus.se/jfokus26-preso/Spec-driven-Development-using-Coding-Agents.pdf'
    hash: sha256:826071b0039518cb28ef1798aa3d05619a61db6492c48424db207313c18d6363
  - type: url
    url: 'https://simonwillison.net/2025/Mar/19/vibe-coding/'
    hash: sha256:e725441983198e989861ffd8eb4fbccea921fa47abf24f5644429df24f706ce5
  - type: url
    url: 'https://simonwillison.net/2025/Mar/23/semantic-diffusion/'
    hash: sha256:bd8b1ebaf3a87c219b7e2befdbb0efc1bb8a0fcf0bb5870fcb6a2bd8732a81cb
  - type: url
    url: 'https://simonw.substack.com/p/vibe-engineering'
    hash: sha256:ef207bce62b3ace1d79b606bd1e4f06b56960f2525d3a90b75215d9f9c381aa2
  - type: url
    url: 'https://arxiv.org/html/2510.00328v1'
    hash: sha256:b2c0a6654af54f57a7e60e8031d5b71ee36c0c875804c8a0ac5cb42ba4d8026b
  - type: url
    url: 'https://simonwillison.net/2026/May/6/vibe-coding-and-agentic-engineering/'
    hash: sha256:d5efc58fb9f6c8e44c88eb246031dace67556db67152702ac3bb82b8c358bb3a
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Generating code with AI without caring about the code that is produced. Coined by Andrej Karpathy in February 2025 for a way of working in which the developer stops reading the generated code; Simon Willison argues the term is being applied to AI-assisted programming in general, a reading he says is wrong. Subsequent academic work has proposed competing formalizations of the practice."
---

Vibe coding is generating code with AI without caring about the code that is produced. [[Person/andrej-karpathy]] coined the term on 6 February 2025, describing "a new kind of coding" in which you "fully give in to the vibes, embrace exponentials, and forget that the code even exists" — accepting every suggestion without reading the diffs, pasting error messages back in with no comment, letting the code grow beyond your own comprehension, and working around bugs the model cannot fix by asking for random changes until they go away. Karpathy attributed its feasibility to LLMs getting "too good", and framed it as something that is "not too bad for throwaway weekend projects" rather than as a method for building production software.

## Usage

[[Person/simon-willison]] set out the narrow reading first in [[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] on 19 March 2025, six weeks after the coinage and at a point when the term had already been featured in the *New York Times*, *Ars Technica* and the *Guardian*. His definition there is "building software with an LLM without reviewing the code it writes", and the line he draws is about engagement with the code rather than about tooling: if an LLM wrote the code and you reviewed it, tested it thoroughly and could explain how it works to someone else, "that's not vibe coding, it's software development," and the use of an LLM is immaterial. He states as a golden rule for production-quality work that he will not commit code to his repository that he could not explain exactly to somebody else. The same post defends the practice on its own terms — as an access story, since it "shaves that initial barrier down to almost flat" for people without a computer science degree or a bootcamp, and as the best available way for experienced developers to build intuition about what LLMs can and cannot do, a claim he backs with more than 80 experiments of his own built this way.

Karpathy replied to that post four days later with a qualification of his own coinage, writing that "it will take some time to settle on definitions" and that while he personally uses "vibe coding" when he feels like the dog in the "I have no idea what I'm doing" GIF — citing an iOS app he had built the night before — "in practice I rarely go full out vibe coding, and more often I still look at the code, I add complexity slowly and I try to learn over time how the pieces work, to ask clarifying questions etc." Willison, recording that reply, had noted on Bluesky the same day that he felt he was "losing the battle on this one", and that a chance at "ONE piece of AI-related terminology with a clear, widely accepted definition" had been lost.

[[Person/simon-willison]] argues in [[BlogPosting/not-vibe-coding]] that the term is being applied to AI-assisted programming in general, a reading he says is wrong, and that the distinction is not which tools are used but whether the developer engages with the generated code at all: using LLM tools as part of a process for responsibly building production code, on his account, is not vibe coding. He cites two forthcoming books, [[Book/vibe-coding]] and [[Book/vibe-coding-the-future-of-programming]], as titles that adopt the term while describing the professional workflow it was explicitly not about.

Willison also argues the term names an audience rather than a tool: people who are not software developers and do not want to become developers, but who now have a path to building custom software for themselves. He frames the open questions for that audience as which kinds of project can be built this way, and how to handle security, privacy, reliability and the risk of over-spending.

Bamil's paper reports that the broader, looser usage has also been recorded lexicographically: by March 2025 the Merriam-Webster online dictionary listed "vibe coding" as a slang term for "writing computer code in a somewhat careless fashion, with AI assistance". Merriam-Webster's own entry defines it as writing code, making web pages, or creating apps by telling an AI program what you want and letting it create the product, noting that the coder does not need to understand how or why the code works and will often have to accept a certain number of bugs and glitches. The term was also named *Collins English Dictionary* Word of the Year for 2025.

Early first-hand accounts came from outside the profession. In February 2025 *New York Times* journalist Kevin Roose, who is not a professional coder, experimented with vibe coding to build several small-scale applications, describing them as "software for one" because of how personalised they could be — while also stating that the results are often limited and prone to errors, in one case fabricating fake reviews for an e-commerce site. Cognitive scientist Gary Marcus responded that the algorithm behind Roose's LunchBox Buddy app had presumably been trained on existing code for similar tasks, and that Roose's enthusiasm stemmed from reproduction rather than originality. Not everyone accepted the name either: in June 2025 Andrew Ng took issue with it, saying it misleads people into assuming that software engineers just "go with the vibes" when using AI tools to create applications.

Reported adoption in the term's first year was rapid. In March 2025 Y Combinator reported that 25% of startups in its Winter 2025 batch had codebases that were 95% AI-generated; in July 2025 the *Wall Street Journal* reported vibe coding being adopted by professional software engineers for commercial use cases. In January 2026 it was reported that Linus Torvalds had used [[SoftwareApplication/google-antigravity]] to vibe code a visualisation tool for his AudioNoise audio effects generator, explaining in the project's README that "the Python visualizer tool has been basically written by vibe-coding."

[[Book/spec-driven-development-ai-native-software-engineering]] treats the term as the industry's own acknowledgement of a gap between tooling and practice. [[Person/kevin-ryan]] writes that the tools have leapt ahead of the practices — "we prompt, we iterate, we get something that mostly functions, and we move on" — and that "the industry has started calling it 'vibe coding' — half joke, half admission that we're making it up as we go."

### Who it suits, and for what

Practitioner accounts converge on a narrow band of appropriate use. [[NewsArticle/engineers-are-using-ai-to-code-based-on-vibes]] reports two non-specialists shipping working internal tools — a mechanical engineer converting a C iPad app to a JavaScript web app in about two hours where the original had taken almost a month, and a data engineering lead building proofs of concept with cloud services he had never used professionally — alongside a 25-year software engineer who argues neither of them was really vibe coding, and who found that taking the definition literally meant "specifying what I want the AI to do is turning out to be a harder problem than doing it myself." All three agree on one point: that the practice helps engineers gain skills in languages and stacks they do not yet know, with the advice to junior engineers being to treat it as an accelerator for acquiring new skills rather than as a speed-up for skills they already have.

A Japanese-language explainer on Qiita reaches a similar shape from the other direction, describing the intended audience as either people already fluent enough in coding to recover when something breaks, or complete beginners with a vision they cannot implement themselves. It lists small projects, personal or workflow-automation tools, and building from scratch as the fitting cases, and characterises the practical loop as instruct, run, and paste errors back without reading the code. Its taxonomy of tooling distinguishes general assistants and chatbots for requirements discussion, editor-integrated agents for final adjustment while looking at files, CLI-based agents for environment setup and bulk file generation, and voice input for dictating instructions — and notes that outcomes depend heavily on the capability of the underlying model. It also sets out a staged practical flow — requirements definition, technology selection, codebase creation, then fine-tuning — under which the human's role becomes largely approving the commands the agent proposes, with frequent Git commits as the safety net; the flow is close enough to specification-first practice that it sits uneasily with the term's strict definition.

### Conditions and safety rails

Willison's March 2025 post sets out conditions for when vibe coding is appropriate: keep projects low stakes, weighing how much harm buggy or insecure code could cause and taking particular care if other people will use it; treat security carefully, watching both for secrets such as the API keys used to access online tools and for private data that might leave the machine; be a good network citizen, since anything making requests out to other platforms increases the load and hence the cost on those services; and beware usage-billed APIs, citing horror stories of features vibe coded against an API with no billing limit racking up thousands of dollars in charges. He recommends that a beginner planning to share vibe-coded software with others get a check from someone more experienced first.

He treats making vibe coding safe as an unsolved design problem whose starting point is the sandbox, praising [[SoftwareApplication/claude-artifacts]]' locked-down `<iframe>` — approved libraries only, no network requests to other sites — as making it very difficult to cause harm while also greatly limiting what such projects can do, and contrasting it with [[SoftwareApplication/cursor]], which he describes as initially intended for professional developers and as having far less safety rails. He says he hopes for "a cambrian explosion" of tooling in this space.

### Criticism

> **Source caveat.** A large part of this section derives from Wikipedia's article on vibe coding, whose "Criticism" section carries a maintenance banner dated August 2026 warning that it "may compromise the article's neutrality" and asking editors to integrate negative information into other sections or remove undue focus on minor criticisms and controversies. The individual reports below are attributed as the article attributes them, but their prominence relative to the rest of the topic should be read with that banner in mind.

The most-cited concerns are code quality and security. Commentators note that developers who commit AI-generated code without comprehending it leave undetected bugs and vulnerabilities behind, and that while the approach may suit prototyping or the "throwaway weekend projects" Karpathy originally envisioned, it poses risks in professional settings where deep understanding is needed for debugging, maintenance, and security. Reported incidents and studies include a May 2025 report that 170 of 1,645 web applications created with the vibe coding app Lovable had an issue allowing anyone to access personal information; an October 2025 Veracode study finding that over three years LLMs became dramatically better at generating functional code while the security of generated code generally did not improve, with larger models no better than small ones; a December 2025 CodeRabbit analysis of 470 open-source GitHub pull requests finding that AI co-authored code contained roughly 1.7 times more "major" issues than human-written code, with misconfigurations 75% more common and security vulnerabilities 2.74× higher; and a July 2025 account from a SaaStr founder whose Replit AI agent deleted a database despite explicit instructions not to make changes.

Two further incidents are recorded. In December 2025 the computer security researcher Etizaz Mohsin discovered a security flaw in the Orchids vibe coding platform, which he demonstrated to a BBC News reporter in February 2026. And when rsync was updated to 3.4.3 on 20 May 2026, several users who could no longer perform incremental file backups found that dozens of git commits since rsync 3.4.1 had been made by "tridge and claude", with Anthropic's Claude used in the coding process; a GitHub issue titled *Please Do Not Vibe Fuck Up This Software* spread to other sites and set off a debate over AI-generated code being accepted into critical open source infrastructure. Tridge responded in a blog post called *rsync and outrage*, stating he had used AI to add test suites and "defence-in-depth hardening techniques" to the code, and adding that OpenBSD's openrsync — the alternative some users were planning to switch to — fails the AI-assisted test suite; OSNews editor Thom Holwerda criticised that last remark as "childish and unnecessary, and reeks of insecurity".

[[Person/arun-gupta]] makes the structural version of the same complaint in [[PresentationDigitalDocument/spec-driven-development-using-coding-agents]], characterising vibe coding as a one-shot, prompt-and-pray approach: no structure, no planning, lots of hallucinated files, misunderstanding of the codebase, and ignorance of corporate standards, producing code that is hard to extend, nearly impossible to safely change once the original mental model is gone, and harder to review. His prescription is not better prompting but an intention-first, code-second approach — see [[DefinedTerm/spec-driven-development]].

On maintainability, an early-2025 GitClear longitudinal analysis of 211 million lines of code changes from 2020 to 2024 found refactoring dropping from 25% of changed lines in 2021 to under 10% by 2024, code duplication increasing roughly fourfold, copy-pasted code exceeding moved code for the first time in two decades, and code churn nearly doubling. On productivity, a July 2025 METR randomized controlled trial in which 16 experienced open-source developers completed 246 tasks in mature repositories found that allowing early-2025 AI tools increased completion time by 19%, against participants' prior prediction that AI would reduce it by 24%.

In September 2025 *Fast Company* reported that the "vibe coding hangover" is upon us, with senior software engineers citing "development hell" when working with AI-generated code. Debugging is a recurring reason: LLMs generate code dynamically and its structure may vary, and since the developer did not write the code they may struggle to understand its syntax and concepts. In May 2026 the *Wall Street Journal* reported criticism from Mario Zechner and Armin Ronacher, the engineers behind the Pi coding harness inside the OpenClaw AI agent system, who warned of a looming "vibe slop" crisis — arguing that companies are trading near-term productivity for longer-term buggy software, service outages, security vulnerabilities and technical debt. Zechner was quoted saying "You have infrastructure that's falling apart, and you have software that's now very, very buggy compared to before. We can play this game for a couple more months, or maybe even years, but eventually it will catch up to us."

Two further strands concern the ecosystem rather than individual codebases. A January 2026 paper titled "Vibe Coding Kills Open Source" argues that vibe coding raises productivity by lowering the cost of using and building on existing code while weakening the user engagement through which many maintainers earn returns, reducing the availability and quality of open-source software despite higher productivity; commentary on the paper adds that models gravitate toward large, established libraries that appear frequently in their training data, removing the organic selection process by which newer tools get noticed. In February 2026 GitHub acknowledged an increase in lower-quality AI-generated contributions overwhelming maintainers, describing it as an Eternal September for open source, citing the cURL project ending its bug bounty programme after AI-generated security reports multiplied, and introducing maintainer controls such as restricting pull request creation to collaborators.

### What practitioners actually report

[[ScholarlyArticle/vibe-coding-in-practice]] is the first systematic attempt in these sources to measure the practice rather than define or argue about it. It codes firsthand practitioner accounts from grey literature into behavioral units across four questions, and the resulting distributions are worth reading together, because the same population reports all four.

Motivation is dominated by speed: **Speed & Efficiency accounts for 62%** of motivation units, with Accessibility & Empowerment at 14% and Learning & Experimentation at 11%. Experience is dominated by success: **Instant Success & Flow, 64%**, with practitioners describing the process as fast, easy and "Magical", and one account describing a "dopamine hit" when prototypes, QA checks and deployments came together quickly — against Prompt Struggle & Iteration at 13%, where some projects required dozens or hundreds of iterations, and Code Breakdown or Abandonment at 11%, where sessions ended in projects being given up rather than debugged.

Judgement of the output is markedly less positive than the experience of producing it: **"Fast but Flawed" is the leading perception at 68%**, with practitioners accepting flaws as an inevitable cost of rapid development while recognising the technical debt, and Fragile or Error-Prone at 19%, with warnings that outputs which look clean can conceal subtle logic errors, performance bottlenecks or security flaws. Only 3% of units describe the code as High Quality & Clean.

The QA distribution is where the paper locates the problem: **Skipped QA at 36%** — no unit or integration tests, no structured review, correctness judged by whether the code ran — followed by Manual Testing or Edits at 29%, Uncritical Trust at 18%, and Delegated QA to AI at 10%, the last being reliance on the same models that introduced the errors to also find them.

The authors name three findings on top of these numbers. The **speed–quality trade-off paradox**: vibe coders knowingly accept flawed code for rapid progress, but "only experienced users have the skills to fix problems when they arise". A **QA crisis in AI-assisted development**, which they attribute to generated code being hard to debug for want of architectural structure and contextual detail, to confusion when trying to understand it, and to false confidence created by the instant-success experience — with the organizational risk that a lowered quality bar becomes a culture where untested code is acceptable. And a **new class of vulnerable developers**: those the 14% accessibility motivation brings in, who can build an application but not diagnose it, and who the paper says risk a "novice developer trap" of reprompt–paste loops. The authors state their findings rest on self-selected practitioner accounts and "cannot be considered generalizable to all vibe coders".

## Academic formalizations

Two 2025 papers propose formal treatments of the practice, and they differ in what they take the defining characteristic to be.

[[ScholarlyArticle/survey-of-vibe-coding-with-large-language-models]] characterises vibe coding as a development methodology in which developers validate AI-generated implementations through outcome observation rather than line-by-line code comprehension — a reading close to Karpathy's original. It formalizes the practice as a Constrained Markov Decision Process capturing the dynamic triadic relationship among human developers, software projects, and coding agents, and synthesizes existing practice into five development models: Unconstrained Automation, Iterative Conversational Collaboration, Planning-Driven, Test-Driven, and Context-Enhanced Models.

[[ScholarlyArticle/vibe-coding-ai-native-paradigm]] proposes a different definition, in which the developer communicates three things to an agent: functional intent, an emotional tone or style — the "vibe" itself, expressed in descriptors such as "playful and engaging" or "minimalist and professional" — and contextual constraints. On this reading vibe coding builds on prompt programming but goes further by placing equal emphasis on the software's functional intent and on the qualitative feel the developer envisions, with the agent selecting language, colours, or architectural patterns accordingly. The same paper also retains the trust element of Karpathy's original description, noting that proponents describe copying and pasting code without reading the diffs and adjusting the result by asking the agent for high-level changes until it looks right.

The two formalizations share the claim that the developer's role shifts away from writing and verifying code, but they disagree on whether the "vibe" in the name refers to the developer's relinquishing of code review (Karpathy's sense) or to a qualitative specification supplied alongside the functional one (Bamil's sense).

### The line, and where its author found it blurring

[[BlogPosting/vibe-coding-and-agentic-engineering-are-getting-closer]] restates [[Person/simon-willison]]'s boundary and then reports it eroding. His restatement keeps the term narrow and non-pejorative: vibe coding is asking for a thing and getting a thing, not caring about code quality or additional constraints, possibly without knowing how to program — and it is "fantastic, provided you understand when it can be used and when it can't." His stated boundary is who bears the cost: a personal tool where a bug hurts only you is fine, while building for other people is "grossly irresponsible" at that standard because other people are hurt by your bugs.

What he reports changing is not the definition but his own conformity to it. As agents grew more reliable he stopped reviewing every line, including for production work, which leaves him with "that feeling of guilt: if I haven't reviewed the code, is it really responsible for me to use this in production?"

The post adds a second-order consequence for anyone judging software from the outside. A repository with a hundred commits, a good readme and comprehensive tests used to signal care; he can now produce one in half an hour that looks identical, and says he cannot tell the difference even for his own projects. The substitute signal he proposes is usage — a vibe-coded tool someone has used daily for two weeks is worth more than something barely exercised — with the enterprise version being that he would not adopt a CRM unless two other large enterprises had run it successfully for six months.

### Where it stops working

Wikipedia's article states the boundary in terms of task structure rather than skill. Generative AI "is capable of handling simple tasks like basic algorithms" — a phrase the article itself tags as needing clarification — but such systems "struggle with more novel, complex coding problems," and it names three shapes specifically: projects involving multiple files, projects depending on poorly documented libraries, and safety-critical code.

That characterisation is worth separating from the productivity findings above, because it describes a different limit. The measured slowdowns concern how much faster the practice makes an experienced developer; this names the categories of problem the article says such systems struggle with, which lines up with the boundary practitioners draw around who bears the cost of a defect.

## Related Terms

Willison attributes the broadening of the term's meaning to [[DefinedTerm/semantic-diffusion]], which he describes as an unstoppable force. He first reached for [[Person/martin-fowler]]'s 2006 term on 23 March 2025, calling what was happening to vibe coding "such a clear example of this effect in action" and reporting that the same had happened over the preceding couple of years to his own coinage, prompt injection.

Bamil's paper positions [[DefinedTerm/vibe-engineering]] as the disciplined counterpart to vibe coding, and suggests vibe coding may evolve into a spectrum of practices spanning experimental prototyping through to that more disciplined end. [[DefinedTerm/agentic-engineering]] is a separately proposed name for the same disciplined end, and [[DefinedTerm/spec-driven-development]] one route to it. The umbrella practice vibe coding sits within is [[DefinedTerm/ai-assisted-software-development]], and the tools that make it possible are covered under [[DefinedTerm/coding-agent]]. In the same period Willison also recorded Thomas Klausner coining [[DefinedTerm/brain-coding]] for a technique Klausner describes as starting with an empty editor buffer and typing the code oneself.

[[Person/dan-shapiro]]'s [[DefinedTerm/five-levels-of-vibe-coding]], which Ryan records as published in January 2026, takes the broad reading as given and grades practice on a 0–5 scale running from "Spicy Autocomplete" through pairing, agent supervision and spec writing to the [[DefinedTerm/dark-factory]]. Ryan adopts it as a maturity diagnostic and reports that in every engagement he ran in the preceding year, teams self-assessed at least one level higher than their actual practice.
