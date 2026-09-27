---
title: "GitHub MCP サーバー"
type: "schema:SoftwareApplication"
lang: ja
tags: [ツール利用, エージェントツーリング]
translated_from: ".wikicommit/entity/en/SoftwareApplication/github-mcp-server.md"
source_commit: "ec1aed6cc815a0de19917c1c3fa9646b24090b11"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "GitHub 自身による Model Context Protocol サーバー。ユーザーが OAuth または個人用アクセストークンで付与したアクセス権の範囲内で、AI ツールに GitHub のデータと操作（issue、プルリクエスト、Dependabot アラート）へのアクセスを提供する。"
  applicationCategory: "Model Context Protocol サーバー"
  author: "[[Organization/github]]"
---

GitHub MCP サーバーは、AI ツールを GitHub に接続するために [[Organization/github]] が提供している [[DefinedTerm/model-context-protocol]] サーバーである。これを通じてエージェントは、既存の issue やプルリクエストから情報を取得し、Dependabot アラートを一覧し、issue やプルリクエストを作成・管理できる。いずれもユーザーが与えたアクセス権の範囲内で行われる。

GitHub のあるデベロッパーアドボケイトは、これを MCP サーバーが従うパターンの実例として、また、既存のサーバーがある場合には独自のサーバーを作らない理由として紹介している。独自版を作るのではなく、アップストリームに貢献して皆のためにそれを改善することを勧めている。

## 機能

リモートサーバーとしても、ローカルでの利用向けにも提供されている。アクセス権は、リモートサーバーでは OAuth フローを通じて、ローカルとリモートの両方の形態では個人用アクセストークンを通じて付与される。

リモートサーバーは、一般に npm パッケージや Docker コンテナで行われる MCP サーバーのローカル実行に伴うオーバーヘッドを減らす手段として紹介されており、GitHub の解説によれば、個人用アクセストークンの代わりに OAuth 2.0 で認証できる。AI ツールに、issue、プルリクエスト、コードファイルといった GitHub のライブなコンテキストとツールを提供する。VS Code から使うには、プロジェクトのリポジトリに記載されているとおりに MCP 設定を更新する。同じ解説は、このサーバーがオープンソースであることにも触れている。

## 採用状況とエコシステム

MCP サーバーの構築に関する GitHub のチュートリアルは、自身のワークフローで使うため、あるいは実際の実装を学ぶために、読者にこのサーバーを紹介している（[[BlogPosting/building-your-first-mcp-server]]）。また、別の解説では、issue からプルリクエストに至るワークフローの中で、リモートサーバーを [[SoftwareApplication/github-copilot-coding-agent]] と併用している（[[BlogPosting/from-idea-to-pr]]）。
