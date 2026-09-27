---
title: "Model Armor"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント安全性, ガードレール, プロンプトインジェクション, セキュリティ]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/model-armor.md"
source_commit: "bcf2a6e3499612efcdde4e63a1d4d23bb9dc9e6f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "プロンプトとレスポンスを対象に、プロンプトインジェクション、ジェイルブレイク、悪意のある URL、機密データの漏えいをスクリーニングする Google Cloud のインライン AI ファイアウォール。Gemini Enterprise Agent Platform では、Agent Gateway がエージェントのリクエスト経路上で適用する。"
  applicationCategory: "マネージド AI セキュリティサービス"
  featureList: "イングレスでのプロンプトに対するプロンプトインジェクション・ジェイルブレイク・悪意のある URL のスクリーニング、モデル実行前の該当リクエストのブロック、レスポンス内の機密データを墨消しするエグレスでの Sensitive Data Protection、リージョン単位の設定テンプレート"
  author: "[[Organization/google]]"
---

Model Armor は、Google がインライン AI ファイアウォールと説明する Google Cloud のサービスで、プロンプトとレスポンスを対象に、プロンプトインジェクション、ジェイルブレイク、悪意のある URL、機密データの漏えいをスクリーニングする。[[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] では、[[SoftwareApplication/gemini-enterprise-agent-platform]] 上の 3 つのマネージドなランタイム制御の 1 つとして位置づけられており、Agent Gateway を通じて適用される。Agent Gateway は、ユーザー、エージェント、そのモデルとツールの間のやり取りを傍受するランタイムの強制ポイントである。

同記事は、Model Armor を人手で保守するジェイルブレイク用フレーズのリストに代わるものとして提示している。難読化されたあらゆるジェイルブレイクに対応する正規表現辞書を保守するやり方は、本番環境ではすぐに破綻する、というのが記事の主張である。

## 機能

イングレスでは、Model Armor はエージェントの推論ループが動く前に、境界でペイロードをスクリーニングする。このプラットフォームでは Agent Gateway が Model Armor のテンプレートをリクエスト経路上で直接適用するため、開発者がスクリーニングの呼び出しを書く必要はない。記事では基盤となる API 呼び出しも示されており、ユーザーのプロンプトを指定したテンプレートに照らして送信し、サニタイズ結果を受け取る。フィルターが一致した場合、リクエストはエッジで 403 として破棄される。エージェントのモデルは一切呼び出されないため、トークンは消費されず、コンテキストウィンドウもクリーンに保たれる。記事は、Model Armor のテンプレートがリージョン単位であることにも触れている。

エグレスでは、送出されるレスポンスに対して Sensitive Data Protection を実行し、クレジットカード番号、Stripe のシークレット、従業員 ID などの値を、ゲートウェイの外に出る前に墨消しする。

## 採用とエコシステム

記事の多層的な設計では、Model Armor がペイロードをフィルタリングし、[[SoftwareApplication/semantic-governance-policies]] が提案された各ツール呼び出しの意図を推論し、Agent Anomaly Detection がセッション全体の振る舞いを監視する。記事自身の例は、ペイロードのスクリーニングの限界を示している。丁寧で構文上も問題のないソーシャルエンジニアリングのリクエストにはジェイルブレイクの兆候がないため、Model Armor はそれを通過させ、判断はポリシーエンジンに委ねられる。
