---
title: "Terminal-Bench"
type: "schema:Dataset"
lang: ja
tags: [評価, エージェント]
translated_from: ".wikicommit/entity/en/Dataset/terminal-bench.md"
source_commit: "f948f309cb907fd940528e22bdf1a82e1e673130"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "バージョン 4.0 として公開されているベンチマークで、公式サイトは自らを、エージェントの作業のフロンティアを測定し、それとともに進化するものと説明している。結果はタスク全体に対する解決率として、コストやトークン数とあわせて報告される。"
  url: "https://www.tbench.ai/"
---

Terminal-Bench は、公式サイトが一文で「エージェントの作業のフロンティアを測定し、それとともに進化する（to measure and evolve with the frontier of agent work）」ものと説明しているベンチマークである。そのサイトで提示されているバージョンは Terminal-Bench 4.0 である。サイトはこのベンチマークに加えて、リーダーボード、別の場所でホストされているタスク一覧、そして実行方法、ブログ、コミュニティの Discord、コントリビューター向けのページを用意している。

## 内容

ベンチマークの中身はタスクの集合であり、ランディングページとは別の場所、Harbor フレームワークのデータセットハブ上で、ベンチマーク名とバージョン番号を含むパスの下に公開されている。ランディングページが示しているのは、タスクが何を含むかではなく、タスク全体にわたる結果がどのように報告されるかである。リーダーボードは、順位、モデル、実行に用いたエージェント、解決率、コスト、トークン数という構成で並べられている。解決率は Terminal-Bench 4.0 のタスクのうち解決されたものの割合であり、95% 信頼区間を示すひげ（whisker）付きでプロットされる。

ページには、ベンチマークのデータが学習コーパスに決して含まれるべきではないという宣言も掲載されており、その後に Terminal-Bench の GUID が続く。

## 出自

サイトは、このベンチマークのホストとして Stanford、Harbor、Laude Institute を挙げており、タスクは Harbor フレームワークのデータセットハブを通じて公開している。

## 利用

LangChain は、ランディングページに掲載されているものより前のバージョンである Terminal Bench 2.0 を用いて自社のコーディングエージェントへの変更を評価し、その結果を [[BlogPosting/improving-deep-agents-with-harness-engineering]] で報告している。同社はこのバージョンを、エージェント型コーディングを評価するための今や標準的なベンチマークであり、機械学習、デバッグ、生物学などのドメインにわたる 89 のタスクを持つと説明している。実行のオーケストレーションには Harbor を用い、サンドボックスの立ち上げ、エージェントループとのやり取り、検証と採点を行わせた。このベンチマークの厳しいタイムアウトは、LangChain が行ったハーネスの変更 — 時間予算に関する警告や、各段階でどれだけの推論計算を費やすかなど — を方向づけた。

Anthropic も Terminal-Bench 2.0 を Google Kubernetes Engine のクラスタ上で実行し、そこでのスコアがベンチマークのリソース制約の強制方法に依存していたことを [[BlogPosting/quantifying-infrastructure-noise-in-agentic-coding-evals]] で報告している。同記事によれば、Terminal-Bench 2.0 は推奨 CPU と RAM をタスクごとに指定しており、リーダーボードは一時的な過剰割り当てを許容するサンドボックスプロバイダーを使用している。一方、Anthropic 自身の環境は当初、仕様を超えたコンテナをすべて強制終了していた。同じモデル、ハーネス、タスクで 6 通りのリソース構成を試したところ、インフラエラー率は厳格な強制時の 5.8% から上限なしの 0.5% へと低下し、成功率は 6 パーセンテージポイント上昇した — [[DefinedTerm/infrastructure-noise]] を参照。Anthropic は、推奨リソース仕様を公開していることをこのベンチマークの功績として認めたうえで、その強制方法もあわせて規定すれば、同社が見いだした差は解消されるだろうと提案している。
