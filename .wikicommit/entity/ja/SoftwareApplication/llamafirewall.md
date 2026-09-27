---
title: "LlamaFirewall"
type: "schema:SoftwareApplication"
lang: ja
tags: [セキュリティ, プロンプトインジェクション, ガードレール, エージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/llamafirewall.md"
source_commit: "90f235c19401779128f2c36166ba9e641fa1393d"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Meta による、LLM で動作するエージェントのためのオープンソースのシステムレベルのガードレールフレームワーク。ジェイルブレイク分類器、思考の連鎖（chain-of-thought）のアラインメント監査器、生成コードの静的解析器を 1 つのポリシーエンジンに統合している。"
  applicationCategory: "LLM エージェント向けのセキュリティガードレールフレームワーク"
  featureList: "PromptGuard 2 によるジェイルブレイク検出（86M および 22M モデル）、目標の乗っ取りと間接プロンプトインジェクションを対象とする AlignmentCheck による思考の連鎖の監査（実験的）、Semgrep と正規表現ルールを用いた CodeShield による生成コードの静的解析、カスタムの正規表現スキャナーと LLM プロンプトスキャナー、カスタムパイプラインと条件付きの是正措置"
---

LlamaFirewall は、[[DefinedTerm/prompt-injection]]、エージェントのミスアラインメント、安全でないコードなど、AI エージェントに関連するセキュリティリスクに対する最後の防御層として機能するよう設計された、セキュリティに特化したオープンソースのガードレールフレームワークである。[[ScholarlyArticle/llamafirewall-an-open-source-guardrail-system-for-building-secure-ai-agents]] で紹介されており、同論文はこれが Meta で本番運用されていると述べ、他者が利用・拡張できるようオープンソースソフトウェアとして公開している。コードは Meta の PurpleLlama リポジトリ <https://github.com/meta-llama/PurpleLlama/tree/main/LlamaFirewall> で公開されている。

## 機能

LlamaFirewall は複数のスキャナーを統一的なポリシーエンジンにまとめており、開発者はその中でカスタムパイプラインを構築し、条件付きの是正戦略を定義し、新しい検出器を組み込むことができる。同梱されているガードレールは 3 つである。

- **PromptGuard 2** は DeBERTa モデルをベースにした軽量な分類器で、ユーザーのプロンプトや信頼できないデータに含まれる、指示の上書きやトークンインジェクションといった明示的な [[DefinedTerm/jailbreaking]] の手法を検出する。mDeBERTa-base をベースとする 8,600 万パラメータ版と、より低レイテンシの 2,200 万パラメータ版があり、CPU または GPU 上でローカルに実行できる。
- **AlignmentCheck** は実験的な監査器で、高性能な LLM と few-shot プロンプトを用いて、エージェントが選択したアクションとそれまでの推論をユーザーの元々の目標と比較し、[[DefinedTerm/indirect-prompt-injection]] やその他の目標の乗っ取りを示唆するアクションにフラグを立てる。
- **CodeShield** は LLM が生成したコードのためのオンライン静的解析エンジンで、Semgrep と正規表現ベースのルールをサポートし、高速なパターンマッチングの層を用い、そこでフラグが立った入力はより深い解析へとエスカレーションする。50 を超える CWE（Common Weakness Enumeration）をカバーする。以前は Llama 3 のローンチの一環としてリリースされていた。

このフレームワークには、正規表現または LLM プロンプトを書ける開発者なら誰でもエージェントのガードレールを更新できる、カスタマイズ可能なスキャナーも含まれている。論文のシナリオでは、PromptGuard が注入された Web コンテンツをエージェントのコンテキストに入る前に破棄し、AlignmentCheck がエージェントの振る舞いがユーザーのタスクから逸脱したときに実行を停止し、CodeShield が安全でない SQL クエリを含むパッチを、エージェントが安全なパターンを採用するまで拒否する。

## 採用とエコシステム

論文は LlamaFirewall を Meta で本番運用されているものとして説明し、従来のセキュリティにおいて Snort、Zeek、Sigma が使われているのと同じように、ポリシーや検出器を共有するための協働の基盤として位置づけている。論文はこのフレームワークを [[SoftwareApplication/nemo-guardrails]]、[[SoftwareApplication/guardrails-ai]]、Invariant Labs のフレームワークと比較し、[[Dataset/agentdojo]] で評価している。著者らは、マルチモーダルエージェントへの拡張、AlignmentCheck のレイテンシ削減、そして悪意あるコードの実行や安全でないツール利用といった振る舞いへの脅威カバレッジの拡大を計画している。これは、エージェントのための [[DefinedTerm/guardrails]] というより広い実践の実装の 1 つである。
