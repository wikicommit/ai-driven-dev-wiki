---
title: "Berkeley Function Calling Leaderboard（BFCL）"
type: "schema:Dataset"
lang: ja
tags: [エージェント, ツール利用]
translated_from: ".wikicommit/entity/en/Dataset/berkeley-function-calling-leaderboard.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "大規模言語モデルを関数呼び出し（ツール呼び出し）タスクで評価するためのベンチマークデータセット。入力として自然言語のクエリと望ましい関数仕様を、期待される出力として正しい関数、パラメータ、値を示す構造化された JSON オブジェクトを組にしている。"
  variableMeasured: ["natural language query", "function specification", "correct function name", "correct parameters", "correct values"]
---

Berkeley Function Calling Leaderboard（BFCL）は、Yan ら（2024）によって導入された、大規模言語モデルが関数呼び出し（ツール呼び出し）タスクをどれほどうまくこなすかを評価するためのベンチマークデータセットである。[[ScholarlyArticle/testing-rest-apis-as-llm-tools]] は、自然言語によるテストケース生成モデルをファインチューニングするための訓練データの一部として、BFCL の V3 リリースを用いている。

## 内容

BFCL の各事例は、入力として自然言語のユーザークエリと望ましい関数仕様（構造的には API 仕様に相当する）を、期待される出力として正しい関数、そのパラメータ、およびその値を示す構造化された JSON オブジェクトを組にしている。

## 出自

BFCL は、大規模言語モデルにおける関数呼び出しのベンチマークとして Yan ら（2024）によって導入された。[[ScholarlyArticle/testing-rest-apis-as-llm-tools]] は、特にその V3 リリースを利用している。

## 利用

[[ScholarlyArticle/testing-rest-apis-as-llm-tools]] は、BFCL のより単純な API 事例 400 件（それぞれパラメータは最大 10 個）を、独自に人手で精選したドメイン固有の API 事例 120 件と組み合わせ、その統合プールの 70% を用いて（検証用とテスト用にそれぞれ 15% ずつを取り分けたうえで）、自然言語のテストケース発話を生成するように Granite-3B-Code-Base モデルを（LoRA により）ファインチューニングしている。
