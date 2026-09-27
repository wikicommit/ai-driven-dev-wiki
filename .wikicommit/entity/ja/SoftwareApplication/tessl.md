---
title: "Tessl"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール, 仕様駆動開発]
translated_from: ".wikicommit/entity/en/SoftwareApplication/tessl.md"
source_commit: "4b83a0390f0437f8f63f9399a1db3e12e1ace784"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "仕様が開発者の直接編集する唯一の成果物であり、コードはすべて仕様から生成・再生成される、スペック・アズ・ソースの開発ツール。2 つ目の出典はこれを実験的なものと説明し、逆方向、すなわち既存のコードから仕様を導出する機能についても記録している。"
  applicationCategory: "スペック・アズ・ソースの開発ツール"
  featureList: "仕様を唯一の編集対象の成果物とし、そこからコードを再生成すること、既存のコードから仕様を導出するための文書化されたコマンド、生成されたコードに付く GENERATED FROM SPEC - DO NOT EDIT マーカー、生成を制御する @generate タグと @test タグ"
---

Tessl は、[[DefinedTerm/spec-driven-development]] のスペクトラムにおいて最も急進的な立場、すなわちスペック・アズ・ソースをとる。そこでは仕様が開発者の直接編集する唯一の成果物であり、コードはすべて仕様から生成され、仕様が変わるたびに再生成される。Tessl をこの位置に置いたレポートは、Tessl が、同レポートが仕様を「新しいソースコード」とみなす新たなビジョンと呼ぶものを体現していると述べている。開発者は要求と振る舞いの観点で作業し、機能を変更するということは、生成されたコードを手で編集するのではなく、仕様を変更して再生成することを意味する。

## 機能

Jimmy Song のオンラインハンドブック『智能体构建指南』のある章は、Tessl を実験的なフレームワークとして説明し、3 つの具体的な仕組みを記録している。まず、上記とは逆方向に働き、すでに存在するコードから仕様を導出する `tessl document --code` コマンドを記録している。次に、生成されたコードには `// GENERATED FROM SPEC – DO NOT EDIT` マーカーが付くと述べている。これによって、スペック・アズ・ソースの境界がワークフローの中だけでなく、ソースツリーそのものの中で目に見えるようになる。そして、生成の内容を制御するために使われる `@generate` タグと `@test` タグを挙げている。この記述は Tessl を、スペック・アズ・ソースへの移行の完成形ではなく、その初期の形として位置づけている。

## 採用状況とエコシステム

2026 年の実務者による仕様駆動開発ツールのサーベイ（[[ScholarlyArticle/from-code-to-contract]]）は、[[SoftwareApplication/github-spec-kit]] と [[SoftwareApplication/kiro]] も含む 3 区分のツールキット分類において、Tessl をスペック・アズ・ソースの端に位置づけており、このアプローチが実用的であるためには、成熟し信頼できるコード生成ツールが必要であると指摘している。上記のハンドブックの章は、この実践の代表的な実装 8 つの 1 つとして Tessl を挙げており、そこにもこの 3 つが含まれている。
