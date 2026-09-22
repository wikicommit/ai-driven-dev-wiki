---
title: "Completion 攻撃"
type: "schema:DefinedTerm"
lang: ja
tags: [LLM, セキュリティ, プロンプトインジェクション, エージェントの安全性]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/completion-attack.md"
source_commit: "6b5a8ac7a493c71300dccb7564cd1bdadb65f53c"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "偽の応答をプロンプトに付け足してアプリケーションのタスクがすでに完了したとモデルに思い込ませ、その上で適切な区切り記号の後ろに新たな指示を注入する、プロンプトインジェクション攻撃の一群。"
---

Completion 攻撃とは、まず偽の応答をプロンプトに付け足してアプリケーションのタスクが完了したと LLM に誤認させ、
続いて新たな指示を注入する——そしてモデルはそれに従う傾向がある——プロンプトインジェクションの技法である。
注入されたテキストが正当なクエリの形式に一致するよう、適切な区切り記号が挿入される。この名称と分類は
[[ScholarlyArticle/struq]] によるもので、その著者らは自らの Completion 攻撃が Simon Willison の先行研究に着想を得た
ものだと述べ、同論文において Completion 攻撃の重要性を強調したと述べている。

## 用法

同論文はこの一群を、攻撃者が用いる区切り記号によって分類している。**Completion-Real** 攻撃は正当なクエリと
まったく同じ区切り記号を用いるもので、最も効果的な戦略とされる。**Completion-Close** 攻撃はそのわずかな変種を用い、
論文の例では "###response:" の代わりに "#Response" が挙げられている。そして **Completion-Other** 攻撃は正当なものとは
まったく無関係な区切り記号を用い、論文の評価では手作業で設計された数百通りの代替から選ばれている。
さらに 2 つの複合形も定義されている。**Completion-RealCmb** と **Completion-OtherCmb** であり、それぞれ Ignore 技法と
Escape-Separation 技法を対応する Completion 攻撃に組み込んだものである。

防御のないモデルに対して測定すると、この一群は同論文の手作りの攻撃のうち最も強力である。Completion-Real は Llama と
Mistral の両ベースラインで 96% の攻撃成功率に達し、Completion-Close の最高得点の変種も同じく両方で 96% に達する。
Completion-Other は Llama で 29%、Mistral で 71% である。注入する指示を中国語やスペイン語に翻訳しても
Completion-Real は防御のないモデルに対して有効なままだが（Llama で 66% と 50%、Mistral で 96% と 92%）、注入全体を
base64 でエンコードすると両方で 0% にまで落ちる。

同論文の防御はこの一群に 2 つの異なる箇所で対処しており、それがこの攻撃を単なる一覧中の一項目ではなく設計上の
標的として扱う理由である。本物の区切り記号を用いる攻撃は、モデルがユーザーデータを見る前に予約された区切りトークンを
除去するフロントエンドの再帰的フィルタによって阻止される。ごく近い区切り記号を用いる攻撃は
[[DefinedTerm/structured-instruction-tuning]] によって阻止される。本物の区切り記号は予約トークンにトークナイズされる
のに対し、ごく近いものは通常のテキストとしてトークナイズされるからである。著者らは、StruQ が自分たちに設計できた
Completion 攻撃をすべて阻止すると述べている。表に残る残余の数値は最大で 2%、防御された Mistral モデルに対する
Completion-RealCmb のものである。また、フィルタがなければ本物の区切り記号を用いる Completion 攻撃は依然として
有効だろうとも注記している。

## 関連用語

[[DefinedTerm/prompt-injection]]、[[DefinedTerm/structured-query]]、
[[DefinedTerm/structured-instruction-tuning]]
