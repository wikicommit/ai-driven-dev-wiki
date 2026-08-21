---
title: "SWE-bench"
type: "schema:Dataset"
lang: ja
tags: [エージェンティックコーディング, ベンチマーク, 評価]
review_status: pending
translated_from: ".wikicommit/entity/en/Dataset/swe-bench.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "実世界の GitHub Issue からなるベンチマークであり、言語モデルとコーディングエージェントがそれらを解決できるかを評価するために使われる。ソフトウェアエンジニアリングにおける Foundation Model の能力についての事実上のベンチマークと記述されている。その後、人手で検証された版と長期タスクの後継版へ改訂されている。"
  creator: "Carlos E. Jimenez and colleagues"
  datePublished: "2024"
  measurementTechnique: "生成されたパッチによる、実世界の GitHub Issue の自律的な解決"
---

SWE-bench は実世界の GitHub Issue から構築されたベンチマークであり、言語モデルがそれらを自律的に解決できるかを試すために導入された。[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] はこれを、ソフトウェアエンジニアリングにおける Foundation Model の能力を評価するための事実上のベンチマークと記述し、[[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] は、自律的な Issue 解決というタスクを定義し、単一エージェント、マルチエージェント、ワークフローに基づくアプローチにまたがる研究のフロンティアを触発した功績を認めている。

## 構成

元のベンチマークはそのタスクを実際のリポジトリの Issue から取っていた。情報源には2つの改訂版が記述されている。

- **SWE-bench Verified** は、SWE-bench のタスクのいくつかが曖昧あるいは仕様不足であるという懸念に対処するために導入された。[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] によれば、OpenAI は SWE-bench の著者らと協働して、これを人手で検証された 500 タスクの部分集合として公開した。
- **SWE-bench Pro** は同じ論文で、SWE-bench Verified がデータ汚染にますますさらされるようになったと警告したうえで OpenAI が推奨した、後続のより信頼できる評価として記述されている。

OpenDev のレポートはこれらを、より広い変種と後継の一族——多言語版、マルチモーダル版、フリーランスのタスク版を含む——のなかに位置づける。それは、関数レベル・クラスレベルの生成から、リポジトリレベルの Issue 解決を経て、環境に接地された相互作用のタスクへと、段階的に広がってきた評価のエコシステムのなかにある。

## 評価における利用

情報源は Verified の部分集合における急速な測定上の進展を報告している。[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] は、2024年8月のローンチ時に GPT-4o がタスクの 33% を解いた一方で、2025年半ばまでに主要なエージェンティックな解が 70% を超えたと述べている。[[ScholarlyArticle/agentic-ai-in-the-software-development-lifecycle]] はその軌跡を両端へさらに伸ばし、2023年10月から2026年4月のあいだに SWE-bench Verified で 1.96% から 78.4% への上昇を報告し、それをエージェンティックなシステムについての実証的な証拠の統合における見出しの性能指標として用いている。

両論文はまた、このベンチマークを能力の確定した尺度としてではなく、注意を要する対象としても扱っている。エージェンティック SE のロードマップは、テストに通ることだけではもはや十分でないと論じ、SWE-bench の結果をより深く検討した研究群を、今日の Foundation Model が生成するコードがプロの製品コードベースにとってマージ可能な水準からなお遠いことを示すものとして要約する。その文献からの知見としては、「もっともらしい」修正の 29.6% が振る舞いの退行を持ち込んでいたか、厳密な再テストで誤りだったこと、エージェントが人間の開発者とは違ってしばしば単一ファイルに限られた表層的なパッチを生み出したこと、そしてユニットテストに通ったパッチの多くが、スタイル上の問題や隠れた退行のためにより広い CI のチェックで落ちたことなどが報告されている。同論文は、SWE-bench から SWE-bench Verified へ、そして SWE-bench Pro へという進行を、この分野の急速な進歩と、エージェントの能力について汚染されていない尺度を保つことの難しさの双方を例示するものと特徴づけている。

Verified の部分集合についてのベンダーの報告にも、それ自身の但し書きが付く。[[Organization/openai]] の [[BlogPosting/introducing-codex]] は、`codex-1` について公表した数値から「われわれの社内インフラでは実行できなかった」SWE-Bench Verified の23サンプルが除外されたこと、そしてモデルが最大コンテキスト長 192k トークンと中程度の「推論の労力」——投稿によればローンチ時に製品で利用可能だった設定——でテストされたことを述べている。同じ投稿は、「OpenAI における実世界の社内 SWE タスクを厳選した集合」と記述する別のベンチマークと並べて結果を報告している。

OpenDev のレポートは、ベンチマークのスコアが評価のハーネスそのものにも敏感であることを指摘する。Meta Context Engineering についての研究を、固定された評価のハーネスがエージェントのベンチマークへ系統的なバイアスを持ち込むことを見出したものとして要約する。ハーネスは、ある戦略を他より有利にしうるしかたでコンテキストを形づくるからである。

ベンチマークは信号の1つにすぎないため、両論文は補完的な証拠を指し示す。エージェンティック SE のロードマップは、エージェントが著したプルリクエストについての大規模な GitHub の研究に依拠し、OpenDev のレポートは、リポジトリレベルの Issue 解決が示唆するよりも、長期にわたるコマンドラインのタスクにおける合格率が実質的に低いことを報告する端末操作のベンチマークを際立たせている。
