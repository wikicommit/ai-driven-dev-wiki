---
title: "Cursor Context Bench"
type: "schema:Dataset"
lang: ja
tags: [エージェンティックコーディング, ベンチマーク, 評価]
review_status: pending
translated_from: ".wikicommit/entity/en/Dataset/cursor-context-bench.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Anysphere が保守する社内評価用データセット。正解が既知であるコードベースからの情報取得に焦点を当てている。Cursor は自社製品で最もよく使われるモデル群に対してこれを実行し、取得ツールが回答精度へ及ぼす効果を測定している。"
  creator: "[[Organization/anysphere]]"
  measurementTechnique: "既知の正解に対する、コードベースを対象とした質問応答"
---

Cursor Context Bench は [[Organization/anysphere]] が保守していると述べる評価用データセットであり、「正解が既知であるコードベースからの情報取得に焦点を当てた」ものである。本 wiki には [[BlogPosting/improving-agent-with-semantic-search]] を通じてのみ登場し、そこでは [[DefinedTerm/semantic-search]] に関する同記事の主張を支えるオフライン測定として用いられている。

## 構成

出典はこのデータセットの規模も、タスクの種類も、その事例がどのように収集・検証されたのかも記述していない。述べられているのはタスクの形——コードベースからの情報取得であり、正解はあらかじめ既知である——と、この評価が [[SoftwareApplication/cursor]] で最もよく使われるモデルのすべて、同社自身の Composer を含めて実行されているということである。

## 評価における利用

このベンチマークは、同一のモデルに対する2つのツール構成——セマンティック検索が利用可能なツールに含まれている場合と、含まれていない場合——を比較するために用いられている。Cursor は、あらゆる構成においてセマンティック検索が結果を有意に改善したと報告しており、これらのオフライン評価から導かれた見出しの数字は、質問への回答精度が平均で 12.5% 高くなり、モデルによって 6.5%〜23.5% の幅があるというものである。

明白な限界は手法ではなく出所にある。このベンチマークは、結果を報告し、かつ評価対象の機能を販売しているのと同じ企業によって保守されており、出典にはそれが公開されているとも、他の誰かがそれに対して実行したとも示されていない。同じ記事における実ユーザトラフィックを用いたオンライン A/B テストは、これらのオフラインの数字よりもかなり小さな効果を示している。
