---
title: "AgentDojo"
type: "schema:Dataset"
lang: ja
tags: []
translated_from: ".wikicommit/entity/en/Dataset/agentdojo.md"
source_commit: "fed0100a95b9cbca3a6a11c43d68e28bc873bdea"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "ツール呼び出しを行う AI エージェントの有用性とプロンプトインジェクションに対する堅牢性を評価するための拡張可能なベンチマーク環境。4 つのタスクスイート（Workspace、Slack、Travel、Banking）を備え、合計 97 のユーザータスク、27 のインジェクションタスク、629 のセキュリティテストケースを含む。AgentDojo の論文で導入された。"
  creator: ["Edoardo Debenedetti", "Jie Zhang", "Mislav Balunovic", "Luca Beurer-Kellner", "Marc Fischer", "Florian Tramèr"]
  url: "https://agentdojo.spylab.ai"
---

AgentDojo は、[[ScholarlyArticle/agentdojo]] で導入されたベンチマーク環境であり、ツール呼び出しを行う AI エージェントの有用性とプロンプトインジェクションに対する堅牢性を評価するためのものである。固定されたテストスイートではなく、新しい環境、ツール、攻撃、防御を時間とともに追加していける拡張可能なフレームワークとして設計されている。

## 内容

AgentDojo の 4 つの環境（Workspace、Slack、Travel、Banking）はそれぞれ、状態を持つアプリケーションドメインをモデル化しており（たとえば Workspace 環境は、メールの受信箱、カレンダー、クラウドドライブを変更可能な Python オブジェクトとして管理する）、その状態を読み書きするツールの集合を公開している。ユーザータスクは、自然言語による指示と、モデルの出力および環境状態の変化を調べてエージェントが正しく解決したかを判定する有用性関数（utility function）との組であり、正解となるツール呼び出しの系列も伴う。インジェクションタスクは、攻撃者の目的（データの窃取など）を指定し、それ自体のセキュリティチェック関数と正解の関数呼び出し系列を伴う。1 つの環境に対するユーザータスクとインジェクションタスクの集合がタスクスイートを構成し、そのスイートのセキュリティテストケースは、ユーザータスクとインジェクションタスクの直積をとることで形成される。4 つの環境全体で、AgentDojo の最初のバージョンは合計 97 のユーザータスク、27 のインジェクションタスク、629 のセキュリティテストケースを含む。インジェクションを一切含まない状態でユーザータスクを実行することは、無害な有用性テストケースとしても機能する。

## 出自

AgentDojo は ETH チューリッヒと Invariant Labs の研究者によって作成され、agentdojo.spylab.ai で公開されている。Python パッケージとして実装されており、環境、ツール、ユーザータスク、インジェクションタスク、攻撃、エージェント防御パイプラインはそれぞれ、フレームワークのコンポーネントインターフェースに従ったコードとして追加される。そのため、中核の設計を変えることなく、新しい環境、タスク、攻撃、防御でベンチマークを拡張できる。

## 利用

[[ScholarlyArticle/agentdojo]] はこのベンチマークを用いて、クローズドソースおよびオープンソースのさまざまなツール呼び出しエージェント、いくつかのプロンプトインジェクション攻撃の言い回しと 1 つの適応的攻撃、そして 4 つのプロンプトインジェクション防御を評価し、それぞれについて有用性と攻撃成功率の結果を報告している。
