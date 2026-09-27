---
title: "Conductor"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール]
translated_from: ".wikicommit/entity/en/SoftwareApplication/conductor.md"
source_commit: "c044ecf40b811dd9fe94970a2c89786a7a0bda4f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Melty Labs が提供するオーケストレーションツール。開発者自身のマシン上で複数の Claude Code エージェントを並列にデプロイ・管理し、各エージェントに専用の独立した Git ワークツリーを割り当て、それらすべてを 1 つのダッシュボードに表示する。"
  applicationCategory: "マルチエージェント・オーケストレーションツール"
  author: "Melty Labs"
---

Conductor は Melty Labs が提供するオーケストレーションツールで、開発者が自身のマシン上で複数の [[SoftwareApplication/claude-code]] エージェントを並列にデプロイし、管理できるようにする。その狙いは、コーディングエージェントの小さな群れを、1 つのエージェントと同じくらい簡単に実行できるようにすることだと説明されている。この名前は直感に反するものだと指摘されている。Conductor（指揮者）と名付けられているにもかかわらず、このツールは [[DefinedTerm/conductor-and-orchestrator-modes]] の区別において、指揮者側ではなくオーケストレーター側に属するからである。

## 機能

各エージェントはそれぞれ独立した Git ワークツリーの中で動作し、これによって同時に作業するエージェント同士の衝突が回避される。ダッシュボードには実行中のすべてのエージェントが表示され（「誰が何に取り組んでいるか」が見えると説明されている）、開発者は最後になってからではなく、作業の進行に合わせてそのコードをレビューできる。

## 採用とエコシステム

[[BlogPosting/future-of-agentic-coding-conductors-to-orchestrators]] は、Conductor を複数のエージェントを同時にオーケストレーションするための新興のプラットフォームやオープンソースプロジェクトの 1 つとして紹介し、[[SoftwareApplication/claude-squad]] と同じグループに分類している。記事は LinkedIn のスタッフソフトウェアエンジニアである Juriy Zaytsev という 1 人のユーザーの言葉を引用している。彼はこのツールを自分にとって最も理にかなった選択肢だと述べ、「エージェントと対話することと、その隣のペインで自分の変更を見ることの完璧なバランス」と表現した。また GitHub との連携がシームレスだと評価し、プルリクエストがマージされた直後にタスクが「Merged」と表示され、「Archive」ボタンが提示されたことを挙げている。これは記事が伝える 1 人のユーザーの体験談であり、一般的な評価ではない。
