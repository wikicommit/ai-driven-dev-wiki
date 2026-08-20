---
title: "Cursor"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェンティックコーディング, IDE, AI支援プログラミング]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/cursor.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "2023年3月に初回リリースされ、のちにエージェント的な能力を獲得した AI コーディングツール。2025年6月に Cursor Agents が、2025年8月に CLI が追加された。2,926 の GitHub リポジトリを対象とした2026年2月の研究では、これを使うリポジトリが調査対象の他のツールを使うものより Rules と Commands の仕組みを重視していると見出された。"
  applicationCategory: "エージェント的能力を備えた AI コーディングツール"
  author: "[[Organization/anysphere]]"
---

Cursor は初回リリース後にエージェント的な能力を獲得した AI コーディングツールである。[[ScholarlyArticle/configuring-agentic-ai-coding-tools]] は、そのリリースを2023年3月、Cursor Agents を2025年6月、Cursor CLI を2025年8月と記録している。同研究のサンプル 2,926 リポジトリのうち 355 に現れ、調査対象の5つのツールのなかで2番目に少なかった。

この研究において Cursor が際立つのは、素の採用率ではなくそのユーザーコミュニティの設定の習慣である。他のツールのユーザーがコンテキストファイルの近辺にとどまるのに対し、Cursor のプロジェクトは Rules と Commands を重視しており、Rules の仕組みはほぼ全面的に Cursor のリポジトリに集中している。著者らはこれを、Cursor が Rules を導入した最初期のツールの一つであったことに帰している。

## 概要

Cursor を採用しているリポジトリは、研究において2つのメタデータの次元で際立っている。サンプル中で最も若く、年齢の中央値は 5.5 年（全体では 6.7 年）である。またソースコードのサイズでは最大で、中央値 75k KB（全体では 40k KB）である。コントリビュータ数の中央値（54）とコミット数の中央値（2,780）も、サンプル全体よりやや高い。

### 検索: grep と並ぶ意味的検索

[[Organization/anysphere]] 自身の研究記事は、コードベースからの取得をエージェントの品質を左右するてこの一つとして扱っている。[[BlogPosting/improving-agent-with-semantic-search]] は、Cursor のエージェントが grep のようなツールによる正規表現ベースの検索に加えて、自然言語のクエリに合致するコード断片を取得する [[DefinedTerm/semantic-search]] を用いており、同社が自ら訓練した埋め込みモデルと自社のインデックス作成のパイプラインがそれを支えていると報告している。自社の [[Dataset/cursor-context-bench]] と自社のユーザートラフィック上で測定された効果として主張されているのは、質問への回答精度が平均で 12.5% 高くなることと、コード残存率のささやかな向上であり、後者は 1,000 ファイル以上のコードベースで最も大きい。述べられている結論は、エージェントは「意味的検索と同様に grep も大いに活用しており、この2つの組み合わせが最良の結果につながる」というものである。

## 機能

研究の表1は、カタログ化された各メカニズムについて Cursor の成果物を挙げている。

- [[DefinedTerm/context-files]] — [[DefinedTerm/agents-md]]、および非推奨の `.cursorrules`
- Settings — `.cursor/cli.json`
- [[DefinedTerm/agent-skills]] — `.cursor/skills/`
- [[DefinedTerm/subagents]] — `.cursor/agents/`
- Commands — `.cursor/commands/`
- Hooks — `.cursor/hooks.json`
- Rules — `.cursor/rules/`
- MCP サーバ — `.cursor/mcp.json`

`.cursor/rules/` に置かれる Cursor Rules は、非推奨のコンテキストファイル `.cursorrules` とは別個の仕組みであり、混同すべきではない。

## 沿革

Cursor は2023年3月にリリースされ、エージェント的な能力は2025年に続いた。

ベンダーについての Wikipedia の記述は、研究の年表に加えて製品の年表を補っている。Cursor のエージェント機能を、コードベース全体を検索し、ファイルを編集し、ターミナルコマンドを実行し、自然言語の指示から複数ステップのプログラミング作業を遂行するものとして記述する。2025年10月の Cursor 2.0 が git worktree またはリモートマシンを用いた複数エージェントの並列実行のサポートを追加したことを記録し、ウェブ、モバイル、コマンドライン、クラウドの各環境向けにさらにエージェントがリリースされたことにも触れている。GitHub のプルリクエストと統合されたコードレビューツール Bugbot は2025年7月に開始され、チーム向けおよびエンタープライズ向けのプランは管理コントロール、利用状況の分析、シングルサインオン、モデルの制御、コンプライアンス機能を提供する。モデルについては、Cursor は自社のコーディングモデルと並んで Anthropic および OpenAI のモデルを含むサードパーティの大規模言語モデルを統合している。2025年7月の月額20ドルの Pro プランの変更——500 リクエストを利用量に応じた上限へ置き換えたもの——は予期せぬ課金についての苦情を招き、その後同社は制限を撤回し返金を約束した。当該の Wikipedia の記事には2026年7月付のメンテナンスバナーが付されており、大規模言語モデル由来のテキスト、したがって検証されていない主張を含んでいる可能性が警告されている。そのため、これらの製品情報は一次資料が得られるまで未確認のものとして扱うべきである——[[Organization/anysphere]] を参照。そのコンテキストファイル `.cursorrules` はこの種の成果物としては最初期に現れたものの一つで、2024年に始まったが、研究がサンプルのなかで見つけたのは 73 件（コンテキストファイルの 1.5%）にとどまった。Cursor はその後このファイルを非推奨とし、現在は代わりに AGENTS.md を使うことを勧めている。[[SoftwareApplication/codex-cli]] とともに、Cursor は研究においてすでに AGENTS.md のネイティブサポートを提供しているツールとして挙げられており、著者らはこれがツールベンダーにとって当然の前提になっていくかもしれないと示唆している。
