---
title: "Gemini Enterprise Agent Platform"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, エージェントプラットフォーム, デプロイ]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/gemini-enterprise-agent-platform.md"
source_commit: "b4fb7581251cd94ab647bba78e4b423acfc06ec0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントを構築・実行するための Google のエンタープライズ向けプラットフォーム。Addy Osmani の報告によれば、Vertex AI を統合し、長時間実行、永続メモリ、サンドボックス化された実行、そしてフリート単位のアイデンティティ・ポリシー・オブザーバビリティのための名前付きサービスからなる単一のスタックにまとめたものである。"
  applicationCategory: "エンタープライズ向けエージェントプラットフォーム"
  featureList: "Agent Runtime、Agent Sessions、Agent Memory Bank、Agent Sandbox、Agent-to-Agent Orchestration、Agent Registry、Agent Identity、Agent Gateway、Agent Observability、Agent Simulation"
  author: "[[Organization/google]]"
---

Gemini Enterprise Agent Platform は、AI エージェントを構築・実行するための Google のエンタープライズ向けプラットフォームである。発表直後に書いた Addy Osmani は、これが Vertex AI をこの単一のプラットフォームに統合し、長時間稼働エージェントを名前付きの SLA を備えた名前付きの製品にしたと報告している。彼はこれを、コードファーストの Agent Development Kit（ADK）およびビジュアルな Agent Studio とバンドルされたものとして位置づけている。

## 機能

Osmani の報告によれば、Agent Runtime は「一度に何日も自律的に実行できる」とうたわれるエージェントをサポートし、コールドスタートは 1 秒未満で、サンドボックスをオンデマンドでプロビジョニングする。彼はユースケースの例として、完了までに 1 週間かかる営業見込み客開拓のシーケンスを紹介している。Agent Sessions は会話とイベントの履歴を永続化し、外部の CRM やデータベースのレコードに対応するカスタムセッション ID に紐付けることができるため、エージェントの状態はそれが関わるビジネス上の状態のすぐそばに置かれる。彼が一般提供（GA）済みと記録している Agent Memory Bank は、プラットフォームの永続的な長期メモリ層である。セッションから記憶を取捨選択してまとめ、それをユーザーのアイデンティティにスコープし、検索 API を公開することで、後のエージェント呼び出しが関連する情報を取り出せるようにする。彼は、Memory Bank を利用した経費申請エージェントによって申請時間が 50% 以上短縮されたという Payhawk の報告を紹介している。Agent Sandbox は堅牢化されたコード実行を担い、彼の評価では Agent-to-Agent Orchestration、Agent Registry、Agent Identity、Agent Gateway、Agent Observability、Agent Simulation が、本番のエージェントフリートを運用するチームがそうでなければ手作業で構築することになる運用上の関心事を基本的にすべてカバーしている。これには、企業が出荷するために必要だと彼が言う暗号学的アイデンティティと監査ログも含まれる。

Google は同じスタックに対するコマンドラインインターフェースも公開している。[[SoftwareApplication/agents-cli]] は、このプラットフォーム、Cloud Run、A2A 連携にまたがるエージェント開発ライフサイクルのための統一されたプログラマティックな基盤として提示されており、スキャフォールディング、評価、インフラのプロビジョニング、Agent Runtime・Cloud Run・GKE へのデプロイ、そして完成したエージェントを配布のために Gemini Enterprise に登録することまでをカバーする。想定される利用者が注目に値する。これは AI コーディングアシスタントが利用することに最適化されている一方で、開発者が同じコマンドを直接実行する Human Mode もサポートしている。この設計の根拠として挙げられているのは、クラウドのコンポーネント群が断片化していると、アシスタントは何かを構築できるようになる前にドキュメントの読み込みに時間とトークンを費やしてしまうという点である。

## 採用とエコシステム

Osmani はこのプラットフォームを、アーキテクチャ的には Anthropic が示した [[DefinedTerm/brain-hands-session-split]] と同じであり、Anthropic と Cursor がそれぞれ別々に説明しているパターンによく似ていると述べている。違いは、チームがゼロから組み立てるよう任されるのではなく、プラットフォームの規模で製品化され、ADK や Agent Studio とバンドルされている点である。彼はこれを、ホスト型のエージェント製品を構築するチームにとっての現実的なマネージドの選択肢の 1 つとして、[[SoftwareApplication/claude-managed-agents]] と並べて挙げている。また、ADK、Memory Bank、Cloud Run、Cloud Scheduler の組み合わせを、状態を蓄積してしきい値に達したときにアラートを出す監視や調査の定期巡回のような、自律的で運用的なエージェントのためのスタックとして、自分が見た中で最もすっきりしたものだと評している。
