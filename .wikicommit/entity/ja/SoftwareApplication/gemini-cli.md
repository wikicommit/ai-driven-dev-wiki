---
title: "Gemini CLI"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェンティックコーディング, CLI, AI支援プログラミング]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/gemini-cli.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Gemini のコマンドラインからのエージェント的インターフェース。2025年5月の Gemini Agent Mode に続き、2025年6月にリリースされた。GEMINI.md のコンテキストファイルと .gemini/ ディレクトリによって設定される。2,926 の GitHub リポジトリを対象とした2026年2月の研究では、調査対象の5つのツールのうち最も出現頻度が低かった。"
  applicationCategory: "エージェンティック AI コーディングツール（CLI）"
---

Gemini CLI は Gemini のコマンドラインからのエージェント的インターフェースであり、[[ScholarlyArticle/configuring-agentic-ai-coding-tools]] で調査された5つのエージェンティック AI コーディングツールの一つである。同研究のツールの年表は、Gemini のリリースを2024年2月、Gemini Agent Mode を2025年5月、Gemini CLI そのものを2025年6月と記録している。研究のサンプルにおいて5つのうち最も出現が少なく、2,926 リポジトリのうち 186 に現れた。

[[SoftwareApplication/github-copilot]] や [[SoftwareApplication/cursor]] と同様、Gemini の利用を示すリポジトリ内のファイルは会話型インターフェースとエージェント的インターフェースの双方に適用されるため、この研究は成果物の存在だけからエージェント的な利用を切り分けることができない。

## 概要

Gemini のリポジトリはサンプルのなかで最も数が少ないものの、最も活発な部類に入る。コントリビュータ数の中央値はいずれのツール群よりも高い 66（サンプル全体では 42）であり、コミット数の中央値も最も高い 3,322（全体では 2,106）である。ソースサイズの中央値 58k KB もサンプルの中央値を上回る。

## 機能

Gemini は、この研究がカタログ化した8つの設定メカニズムのうち6つについて、リポジトリレベルの成果物を提供している。

- [[DefinedTerm/context-files]] — `GEMINI.md`
- Settings — `.gemini/settings.json` または `.gemini/config.yaml`
- [[DefinedTerm/agent-skills]] — `.gemini/skills/`
- Commands — `.gemini/commands/`
- Hooks — `.gemini/settings.json` の内部で定義
- MCP サーバ — こちらも `.gemini/settings.json` 経由で設定

[[DefinedTerm/subagents]] も Rules も提供していない。

## 沿革

研究の年表は、Gemini の初回リリースを2024年2月、そのエージェントモードを2025年5月、CLI を2025年6月に置いている。そのコンテキストファイル `GEMINI.md` は実践においては依然まれで、研究が見つけたのは 159 件、サンプル中の全コンテキストファイルの 3.3% である。GEMINI.md は、他のファイルを指し示すポインタとして振る舞うことが観察されたコンテキストファイルの種類にも含まれており、研究は外向きの参照において CLAUDE.md と AGENTS.md に次ぐと指摘している。
