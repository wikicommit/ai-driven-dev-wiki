---
title: "埋め込みに基づくツールルーティング"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントツーリング, ツール選択, 埋め込み]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/embedding-guided-tool-routing.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "GitHub が Copilot Chat で用いているツール選択の技法。いずれかのツールグループが展開される前に、クエリの埋め込みをすべてのツールとツールクラスタの埋め込みと比較し、意味的に最も関連の深いツールを事前に選んでモデルから見えるようにする。"
---

埋め込みに基づくツールルーティング（embedding-guided tool routing）とは、VS Code における
[[SoftwareApplication/github-copilot]] Chat のツール選択ステップに GitHub が付けた名前である。このステップでは、
いずれかのツールグループが展開される前に、システムがユーザーのクエリの埋め込みを、すべてのツールとそのクラスタの
ベクトル表現と比較し、グループの奥深くにあるものも含めて意味的に最も関連の深い候補を事前に選び、それらをモデルの
候補集合に直接含める。

## 用法

GitHub は [[BlogPosting/how-were-making-github-copilot-smarter-with-fewer-tools]] において、これを
[[DefinedTerm/virtual-tools]] を補完するものとして説明している。ツールをグループ化した後、モデルはたいてい最終的には
正しいツールを見つけたが、先に誤ったグループを開いてからであることが多かった。GitHub の例は "Fix this bug and merge it
into the dev branch" という依頼で、これに対してモデルはしばしば検索ツール、次にドキュメントのツール、次にローカルの Git
ツールを開いてから、ようやく GitHub MCP ツールグループの中のマージツールが必要だと気づいた。ルーティングを用いると、
システムは最初からマージツールが必要になりそうだと推測し、それを直接提示できる。

GitHub はこの技法を Tool Use Coverage で測定している。これは、モデルが正しいツールを必要とした時点で、そのツールがすでに
モデルから見えている頻度として定義される。GitHub のベンチマークでは、埋め込みに基づく選択は 94.5% のカバレッジに達し、
LLM に基づく選択の 87.5%、デフォルトの静的なツール一覧の 69.0% を上回った。同投稿はこれをオフラインで 27.5% の絶対的な
改善と表現している。オンラインのテストでは、Insiders のツール呼び出しの 72% が埋め込みに基づくマッチングによって事前に
展開されていたのに対し、旧方式のもとでの Stable のツール呼び出しでは 19% だった。埋め込みは GitHub 自身の Copilot
埋め込みモデルから得られている。

## 適用される場面

この技法が当てはまるのは、エージェントのツールが展開可能なグループの背後にまとめられていて、探索的な参照のコスト——誤った
グループを参照するたびに、キャッシュミス、1 回の往復、そして失敗の機会が加わる——を取り除く価値がある場合である。GitHub の
実装では、同投稿が意味的類似度のタスクに最適化されていると説明する GitHub 社内の Copilot 埋め込みモデルと、ローカルに
キャッシュされたツールの埋め込みに依存している。その根拠は、GitHub 自身のオフラインベンチマークと自社製品のオンライン
測定であり、単一の投稿で報告されたものである。GitHub は今後の方向性として、埋め込み、メモリ、強化シグナルをどう組み
合わせられるかを探ることを挙げている。

## 関連用語

- [[DefinedTerm/virtual-tools]]
- [[DefinedTerm/model-context-protocol]]
