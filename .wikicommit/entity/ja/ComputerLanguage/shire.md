---
title: "Shire"
type: "schema:ComputerLanguage"
lang: ja
tags: [コーディングエージェント, オーケストレーション, コーディングツール]
translated_from: ".wikicommit/entity/en/ComputerLanguage/shire.md"
source_commit: "19bc48f9255734f269436c88f52086be2c4420a5"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: reviewed

properties:
  description: "大規模言語モデルが統合開発環境と対話してそれを制御し、プログラミングを自動化できるようにする AI コーディングエージェント言語。IDE やリモートエージェントとのやり取りをコードとして定義する。"
reviewed_by: "joyk0117"
---

Shire は、大規模言語モデル（LLM）が統合開発環境（IDE）と自由に対話し、それを制御してプログラミングを自動化
できるようにする、シンプルな AI コーディングエージェント言語であると説明されている。Shire では、IDE から得た
情報をどう扱うか、また IDE がリモートエージェントとどうやり取りするかを、プログラムを書くのと同じように定義する。

[[BlogPosting/integrating-cloud-and-ide-agents]] では、クラウドエージェントと IDE エージェントの協調を実装した
ものとして紹介されている。そこでは、IDE 側のエージェントオーケストレーションシステムが、ローカルのエージェント
だけでなくクラウド上で動作するエージェントも呼び出す。

## 詳細

その記事で示されている例は、メタデータヘッダー — 名前、変数、ストリーミング後のアクション — で始まり、その後に
プロンプト本文が続くファイルである。変数の 1 つは `thread` 関数によって埋められる。この関数は、Dify
プラットフォーム上にデプロイされたリモートエージェントを呼び出すシェルスクリプトを実行し、`jsonpath` で回答を
抽出する。続いてプロンプトが、その要件をユーザーのデータベース情報やテーブルと組み合わせる。モデルが要件を分析
した後、`execute` 関数が、基本的な SQL 規約を保持する 2 つ目のローカルな Shire エージェント（`gen-sql.shire`）を
呼び出し、生成される SQL が企業の標準に従うようにする。さらなる例は GitHub リポジトリ
`shire-lang/shire-spring-java-demo` で公開されている。
