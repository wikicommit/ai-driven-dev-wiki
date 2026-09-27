---
title: "Gemini Cloud Assist"
type: "schema:SoftwareApplication"
lang: ja
tags: [クラウド運用, AI 支援プログラミング]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/gemini-cloud-assist.md"
source_commit: "f98378c1c0274db465979eeb9b19989edbed4da1"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Google Cloud コンソール内の AI アシスタントで、チャットペインとして開く。Google 自身のワークショップでは、プロンプトからアプリケーションのクラウドアーキテクチャを設計し（図と Terraform コードを生成する）、さらにログ分析やパフォーマンス・コストに関する質問を通じてデプロイ済みアプリケーションの運用を支援するために使われている。"
  applicationCategory: "クラウドコンソールの AI アシスタント"
  author: "[[Organization/google]]"
---

Gemini Cloud Assist は [[Organization/google]] の AI アシスタントであり、Google Cloud コンソールに組み込まれていて、コンソール右上の「Cloud Assist Chat」コントロールから開く。ここで参照できる情報源は Google Codelabs のワークショップ「AI Agent End to End」であり、そこではソフトウェア開発ライフサイクルの両端でこのアシスタントが使われている。まずアプリケーションのアイデアをクラウドアーキテクチャに落とし込むために使い、後には稼働中のアプリケーションの運用アシスタントとして使う。

## 機能

ワークショップの設計ステップでは、ユーザーが作りたいアプリケーションをプロンプトで説明する。例では、Python のバックエンドと React のフロントエンドをそれぞれ Cloud Run 上で別々にホストし、WebSocket で通信させ、生成された画像を Cloud Storage バケットに保存し、API キーを保存する手段も用意するという内容であり、これに対して Cloud Assist がアーキテクチャ図を生成する。その後ユーザーは「Edit app design」ビューから対応する Terraform コードをダウンロードでき、ワークショップはこれを同じ計画の機械可読版と説明している。ワークショップはこのコードを、参加者が実行するものではなく参照用の設計図として扱っている。

運用ステップでは、アプリケーションのデプロイ後、ワークショップは稼働中の Cloud Run サービスに対して Cloud Assist を使い、3 種類のタスクのプロンプトを与える。サービスのログに記録された最近のエラーの要約、起動レイテンシが高い原因の調査、そしてサービスとそのストレージバケットのコストを分析して節約の余地を探すことである。有効化の手順は「Get Gemini Assist」ステップとして示されており、Cloud Assist を無料で有効にするオプションがある。

## 採用とエコシステム

ワークショップは Cloud Assist を [[SoftwareApplication/gemini-cli]] と組み合わせている。Gemini CLI は、設計ステップと運用ステップの間でコード、テスト、デプロイスクリプト、CI/CD パイプラインを書くために使われる。また、アプリケーションに含まれるエージェントには [[SoftwareApplication/agent-development-kit]] が使われている。ワークショップの位置づけは、アプリケーションの構築を手伝ったのと同じ AI アシスタントが、本番環境での監視、トラブルシューティング、最適化のパートナーにもなるというものである。これは Google がトレーニング用ワークショップで自社のツールを紹介しているものであり、それらがどのように使われているかについての独立した記述ではない。
