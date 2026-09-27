---
title: "Compound Engineering Plugin"
type: "schema:SoftwareApplication"
lang: ja
tags: [Claude Code プラグイン, マルチエージェント, コードレビュー]
translated_from: ".wikicommit/entity/en/SoftwareApplication/compound-engineering-plugin.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Every が提供する Claude Code プラグイン。専門特化したレビューエージェントと、計画 → 作業 → レビュー → 複利化（compound）のサイクルを追加する。エンジニアリング作業の一単位一単位が、後に続く作業を容易にするべきだという考え方に基づいている。"
  applicationCategory: "Claude Code プラグイン"
  author: "Every"
---

Compound Engineering Plugin は、Every が提供する [[SoftwareApplication/claude-code]] のプラグインである。専門特化したレビューエージェントと、計画 → 作業 → レビュー → 複利化（compound）のサイクルを追加するもので、エンジニアリング作業の一単位一単位が後に続く作業を容易にするべきだという考え方を中心に設計されている。インストールは Claude Code の中から行い、GitHub リポジトリをプラグインマーケットプレイスとして追加したうえで `compound-engineering` をインストールする。

## 機能

- `/workflows:plan` は、機能のアイデアを詳細な実装計画に落とし込む。
- `/workflows:review` は、マージ前にマルチエージェントによるコードレビューを実行する。セキュリティ、パフォーマンス、アーキテクチャ、複雑さのそれぞれに専門のレビュアーが割り当てられる。
- `/workflows:compound` は、得られた学びを文書化し、将来のエージェントが過去の作業の恩恵を受けられるようにする。

## 採用とエコシステム

Addy Osmani は [[BlogPosting/claude-code-swarms]] の中で、[[DefinedTerm/agent-teams]] を中心により構造化されたワークフローを求める人にこのプラグインを勧めている。彼はこのプラグインの思想を「80% が計画とレビュー、20% が実行」と表現し、これが Agent Teams を効果的にする要因と対応していると論じている。すなわち、仕様が優れているほどエージェントの出力は良くなり、学びが体系化されるほど後続のエージェントが迷走することは少なくなる、というものである。同じ記事は、このプラグインが [[SoftwareApplication/opencode]] でも動作し、実験的には Codex でも動作すると述べている。
