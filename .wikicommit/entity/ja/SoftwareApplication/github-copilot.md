---
title: "GitHub Copilot"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェンティックコーディング, AI支援プログラミング]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/github-copilot.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "2021年10月に初回リリースされ、のちにエージェント的な能力を獲得した AI コーディングアシスタント。2025年2月にエージェントモードが、2025年9月に CLI が追加された。主に .github/ 以下のコンテキストファイルによって設定される。2,926 の GitHub リポジトリを対象とした2026年2月の研究では、調査対象の5つのツールのうち2番目に多く出現した。"
  applicationCategory: "エージェント的能力を備えた AI コーディングアシスタント"
---

GitHub Copilot は会話型のツールとして始まり、のちにエージェント的な能力を獲得した AI コーディングアシスタントである。[[ScholarlyArticle/configuring-agentic-ai-coding-tools]] は、その初回リリースを2021年10月、2025年2月に追加されたエージェントモード、そして2025年9月の Copilot CLI を記録している。同研究のサンプルにおいて、調査対象の5つのツールのうち2番目に多く、2,926 リポジトリのうち 958 に現れた。

研究は Copilot を、会話モードとエージェントモードが同じリポジトリ内のファイルを共有するツールの群——[[SoftwareApplication/cursor]] と [[SoftwareApplication/gemini-cli]] とともに——に置いている。つまり成果物に基づく検出では、これらについてエージェント的な利用と会話的な利用を切り分けられない。

## 概要

Copilot のリポジトリが [[DefinedTerm/context-files]] より先へ広がることはまれである。研究はこの点で [[SoftwareApplication/codex-cli]] と同じ群に位置づけており、Claude Code の広い設定のフットプリントや Cursor の Rules と Commands の重視とは対照的である。Copilot を採用しているリポジトリはサンプル中で最も古く、年齢の中央値は 7.1 年であった。

## 機能

Copilot は、研究がカタログ化した8つの設定メカニズムのうち4つを、リポジトリレベルのファイルを通じてサポートしている。

- [[DefinedTerm/context-files]] — `.github/copilot-instructions.md` および `.github/instructions/*.md`。Copilot は他のツールのコンテキストファイル形式——CLAUDE.md、[[DefinedTerm/agents-md]]、GEMINI.md——も読む
- [[DefinedTerm/agent-skills]] — `.github/skills/`
- [[DefinedTerm/subagents]] — `.github/agents/`
- Hooks — `.github/hooks/*.json`

Settings と MCP サーバは、プロジェクトのリポジトリ内のファイルではなく GitHub のウェブインターフェースを通じて設定されるため、研究のファイルベースの検出の範囲外にある。Copilot は Commands も Rules も提供していない。

### エージェント的ワークフローのデフォルトエンジンとして

[[SoftwareApplication/github-agentic-workflows]] についての GitHub のドキュメントは、Copilot をそれらのワークフローのデフォルトのコーディングエージェントとして挙げている。複数のエンジンがサポートされ、フロントマターの `engine` プロパティで選択される——ほかに名指されているのは Anthropic Claude、OpenAI Codex、Google Gemini である——そして「何も指定されない場合、GitHub Copilot がデフォルトのエンジンである」。利用には GitHub Copilot のプランが必要で、各エンジンにはそれぞれの認証シークレットをリポジトリに設定する必要がある。

課金の経路はエンジンによって異なり、デフォルトの場合については Copilot の条項に記載されている。推論は AI クレジット（`1 AIC = 0.01 米ドル`）で従量計測され、デフォルトの Copilot エンジンについてはその AIC の使用が GitHub Copilot の課金における AI クレジットへ対応づけられる。サードパーティのエンジンの場合は、代わりにそのプロバイダによって課金される。組織が Copilot のプランを持つ組織所有のリポジトリについては、GitHub は個人アクセストークンではなく組み込みの `GITHUB_TOKEN` を通じて組織へ課金することを推奨している。組織の管理者が Copilot のポリシー設定で「Copilot CLI」と「Allow use of Copilot CLI billed to the organization」を有効にし、各ワークフローがフロントマターの `permissions` の下に `copilot-requests: write` を宣言する。GitHub は、Actions のトークンが組織からの Copilot アクセスを持たない場合、ワークフローが Copilot へリクエストを送る時点で失敗するため、代わりに `COPILOT_GITHUB_TOKEN` を設定しなければならないと指摘している。

## 沿革

2021年10月にリリースされた Copilot は、研究に登場するエージェント的ツール群より数年先んじている。そのエージェント的な能力は2025年2月のエージェントモードと2025年9月の Copilot CLI とともに到来した。そのコンテキストファイル copilot-instructions.md は2024年に現れ始めた成果物の一つで、エージェント的な能力の導入後に増加し、サンプル全体で 1,344 ファイル（コンテキストファイルの 27.7%）に達し、リポジトリの 35.1% に現れている。主要言語が Java、C#、C++ のリポジトリでは支配的なコンテキストファイルの種類であり、他の言語で CLAUDE.md が先行するなかでの例外となっている。研究はまた、copilot-instructions.md から始まったリポジトリが、Copilot がすでに主要なコンテキストファイルの種類をすべてサポートしているにもかかわらず、のちに CLAUDE.md や AGENTS.md を追加することが多いとも観察している。
