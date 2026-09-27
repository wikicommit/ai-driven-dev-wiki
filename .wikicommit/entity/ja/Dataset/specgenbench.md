---
title: "SpecGenBench"
type: "schema:Dataset"
lang: ja
tags: [形式仕様, プログラム検証, ベンチマーク]
translated_from: ".wikicommit/entity/en/Dataset/specgenbench.md"
source_commit: "5bacbd79c76dd8cc2c996065acd6063b17df868b"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "手書きの検証可能な JML 仕様を備えた 120 の Java プログラムからなるデータセット。SV-COMP の Java ベンチマークよりも幅広い制御フロー構造でプログラムの形式仕様生成を評価するために、SpecGen の著者らが作成した。"
---

SpecGenBench は、専門家が記述した正解の形式仕様を備えた 120 の Java プログラムからなるデータセットであり、自動仕様生成を評価するために [[ScholarlyArticle/specgen-automated-generation-of-formal-program-specifications-via-large-language-models]] の著者らによって構築された。著者らはこれを、後続の研究を促進することを意図した貢献として位置づけている。

## 内容

プログラムは多様な制御フロー構造と、配列や文字列といったデータ構造を含み、その仕様には、変数間の線形・非線形の関係を持つ事後条件とループ不変条件が含まれる。プログラムは制御フロー構造によって 5 つのカテゴリに分けられる。Sequential（26 プログラム、分岐もループもなし）、Branched（23、ループはなく分岐あり）、Single-path Loop（24、本体に分岐を持たない 1 層のループ）、Multi-path Loop（26、ループ本体に分岐あり）、Nested Loop（21）である。プログラムの平均はコード 20.77 行、循環的複雑度 6.60 である。

## 来歴

著者らが SpecGenBench を構築したのは、同じく使用した SV-COMP の Java ベンチマークがループを含まないプログラムに偏っており（著者らの分析では 88.7%）、また仕様生成に特化したデータセットがほとんど存在しないためである。20 のプログラムは仕様とともに Nilizadeh らが構築したデータセットから、100 のプログラムは LeetCode から採られている。選ばれたプログラムは、その振る舞いが検証可能な JML 仕様として表現できることが確認されている。LeetCode のプログラムについては、Nilizadeh らの手順に従い、形式検証の専門家 3 名が検証器を通過しなければならない仕様を記述した。あるプログラムについて複数の専門家が検証可能な仕様を作成した場合には、別の専門家がそのうち 1 つを正解として選んだ。

## 用途

SpecGen の論文では、SpecGen は SpecGenBench の 120 プログラムのうち 100 を処理でき、AutoSpec の 91 を上回った。また、ベースラインが処理できなかった 7 つのプログラムを処理できたと報告された唯一の手法であり、そのうち 5 つは Nested Loop カテゴリのものであった。論文はさらに、このデータセットを用いて検証器呼び出しの効率を測定しており、ユーザースタディに用いた 15 のプログラムもこのデータセットから抽出している。
