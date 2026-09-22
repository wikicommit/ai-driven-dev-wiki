---
title: "Colang"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント安全性, ガードレール, 対話モデリング]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/colang.md"
source_commit: "a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "柔軟でありながら制御可能な対話フローを設計するために NVIDIA NeMo Guardrails が導入したモデリング言語。Python に似た構文を持ち、ユーザーの意図・ボットの応答・それらをつなぐフローを例示によって宣言する。このツールキットの dialog rails が書かれる言語である。"
---

Colang は、柔軟でありながら制御可能な対話フローを設計するために特別に作られたモデリング言語である。これは
[[SoftwareApplication/nemo-guardrails]] によって、そのツールキットのさまざまな種類のガードレールを設定し実装する手段として
導入されており、その README は構文を Python に似たものと述べ、とりわけ開発者にとってシンプルで直観的であるよう設計されている
としている。定義は guardrails の設定フォルダ内の `.co` ファイルに置かれ、そこでとりわけ dialog rails を供給する。

1.0 と 2.0 の 2 つのバージョンがサポートされており、既定は 1.0 である。

## 用法

この言語の単位はプログラムされるのではなく宣言される。`define user` ブロックは意図に名前を与え、それを表す発話の例を列挙する
——挨拶のブロックは "Hello!" と "Good afternoon!" を挙げる——したがって意図はパターンによってではなく例示によって指定される。
`define bot` ブロックは応答に名前を与え、その文言を示す。次に `define flow` ブロックがそれらをつなぎ、順序を列挙する。
ユーザーが挨拶を表し、続いてボットが挨拶を表して手助けを申し出る、という具合である。

同じ 3 つの構文は、礼儀と同じ手軽さで制約も表現する。README の 2 つめの例は、"You are stupid" を発話例とする侮辱を表す
ユーザーの意図を定義し、それを、落ち着いて手助けする意思を表すボットの応答と組み合わせるフローを定義している——ある入力の
クラスに対する返答をモデルに委ねるのではなく固定する dialog rail である。

これらの定義が生み出す正規形のメッセージこそが、あるアクションを実行すべきか、次のステップでモデルを呼び出すべきか、あるいは
代わりにあらかじめ定義された応答を使うべきかを判断するときに、このツールキットの dialog rails が働きかける対象である。

## 関連用語

- [[SoftwareApplication/nemo-guardrails]] — この言語を導入し使用しているツールキット
- [[DefinedTerm/guardrails]] — この言語がその一種を表現する、より広い制御の一族
- [[DefinedTerm/prompt-engineering]] — そうした制約をプロンプト自体の中の散文で述べる代替的なアプローチ
