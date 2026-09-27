---
title: "Completion 攻撃"
type: "schema:DefinedTerm"
lang: ja
tags: [LLM, セキュリティ, プロンプトインジェクション, エージェント安全性]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/completion-attack.md"
source_commit: "6b5a8ac7a493c71300dccb7564cd1bdadb65f53c"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "プロンプトに偽の応答を付け加えてアプリケーションのタスクがすでに完了したとモデルに思い込ませ、そのうえで適切な区切り記号の後ろに新たな指示を注入する、プロンプトインジェクション攻撃の一系統。"
---

Completion 攻撃とは、まずプロンプトに偽の応答を付け加えて、アプリケーションのタスクが完了したと LLM に誤認させ、
次に新たな指示を注入するプロンプトインジェクションの技法であり、モデルはその指示に従う傾向がある。注入された
テキストが正規のクエリの形式に一致するよう、適切な区切り記号が挿入される。この攻撃は
[[ScholarlyArticle/struq]] において命名・分類されており、その著者らは自らの Completion 攻撃が Simon Willison による
先行研究に着想を得たものだと述べ、同論文で Completion 攻撃の重要性を強調していると述べている。

## 用法

同論文は、攻撃者がどの区切り記号を用いるかによってこの系統を区分している。**Completion-Real** 攻撃は正規のクエリと
まったく同じ区切り記号を用いるもので、同論文はこれを最も効果的な戦略としている。**Completion-Close** 攻撃はそれらを
わずかに変えたものを用いるもので、同論文の例は "###response:" の代わりに "#Response" を使うものである。そして
**Completion-Other** 攻撃は正規のものとはまったく無関係な何らかの区切り記号を用いるもので、同論文の評価では、人手で
設計された数百の代替候補から選ばれている。
さらに二つの組み合わせ形も定義されている。**Completion-RealCmb** と **Completion-OtherCmb** であり、それぞれ Ignore
技法と Escape-Separation 技法を対応する Completion 攻撃に組み込んだものである。

防御されていないモデルに対して測定すると、この系統は同論文の手作りの攻撃の中で最も強力である。Completion-Real は
Llama と Mistral のベースラインの両方で 96% の攻撃成功率に達し、最も高いスコアの Completion-Close の変種も両方で
96% に達する。Completion-Other は Llama で 29%、Mistral で 71% である。注入する指示を中国語やスペイン語に翻訳しても、
Completion-Real は防御されていないモデルに対して有効なままである（Llama で 66% と 50%、Mistral で 96% と 92%）が、
注入全体を base64 でエンコードすると両方で 0% に下がる。

同論文の防御はこの系統に二つの別々の箇所で対処しており、それがこの系統を単に一覧の中の攻撃の一つとしてではなく、
設計上の標的として扱う理由である。本物の区切り記号を用いる攻撃は、モデルがユーザーデータを見る前にそこから予約済みの
区切り記号トークンを取り除く、フロントエンドの再帰的フィルタによって阻止される。紛らわしい似た区切り記号を用いる攻撃は
[[DefinedTerm/structured-instruction-tuning]] によって阻止される。本物の区切り記号は予約済みトークンにトークン化される
のに対し、似た区切り記号は通常のテキストとしてトークン化されるからである。著者らは、StruQ は自分たちが設計できた
すべての Completion 攻撃を阻止すると述べている。表に残る数値は最大 2% で、これは防御された Mistral モデルに対する
Completion-RealCmb のものである。また、フィルタがなければ、本物の区切り記号を用いる Completion 攻撃は依然として
有効だろうとも指摘している。

## 関連用語

[[DefinedTerm/prompt-injection]], [[DefinedTerm/structured-query]],
[[DefinedTerm/structured-instruction-tuning]]
