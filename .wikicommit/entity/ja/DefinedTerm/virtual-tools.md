---
title: "仮想ツール"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントツーリング, ツール選択, Model Context Protocol]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/virtual-tools.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "機能的に似たツールをひとまとめにし、必要に応じて展開できる単一のツールとしてコーディングエージェントに提示する仕組みを指す GitHub の呼称。個々のツールをすべて見せなくても、何が利用できるかをモデルに把握させられる。"
---

仮想ツール（virtual tools）とは、GitHub が VS Code 上の [[SoftwareApplication/github-copilot]] Chat について説明したところによれば、類似したツールを機能ごとに 1 つの「仮想ツール」の下にまとめ、チャットエージェントが必要に応じて展開できるようにする方法である。GitHub はこれを、関連するツールを収めたディレクトリになぞらえている。モデルには何百ものツール名を浴びせられることなく、何が利用できるかの大まかな感覚が与えられる。また、類似したツールは一緒に使われ、一緒に有効化される傾向があるため、それらをグループ化することで、モデルがツールを個別に探索した場合に想定されるキャッシュミス率も下がると GitHub は述べている。

## 用法

[[BlogPosting/how-were-making-github-copilot-smarter-with-fewer-tools]] で報告されているとおり、GitHub はこの手法を、すべてのツールを公開すること（VS Code のデフォルトのツールセットには約 40 の組み込みツールがあり、[[DefinedTerm/model-context-protocol]] サーバーによって合計が数百に達することもある）と、エージェントにできることを制限するようなかたちでツールセットを絞り込むこととの中間策として導入した。

グループは、GitHub が適応的ツールクラスタリング（adaptive tool clustering）と呼ぶ方法で形成される。以前の試みでは、すべてのツールを LLM に渡してグループ化と要約を依頼していたが、GitHub はこれを断念した。グループ数を制御できず、ときにモデルの上限を超えてしまうこと、処理が遅くトークンのコストがかかること、そしてモデルが一部のツールを分類し損ねることがあったためである。代わりに、GitHub 社内の Copilot 埋め込みモデルで各ツールの埋め込みを生成し、コサイン類似度によってグループ化している。GitHub によれば、これにより正確で安定した再現可能なグループが得られる。各クラスタの要約は依然としてモデル呼び出しで作成されるが、ツールの埋め込みとグループの要約はローカルにキャッシュされるため、再計算のコストは小さい。

同じ考え方は Copilot 自身の組み込みツールにも適用されている。13 個のツールからなるコアセットが最初から提示され、残りの組み込みツールは Jupyter Notebook Tools、Web Interaction Tools、VS Code Workspace Tools、Testing Tools の 4 つの仮想カテゴリーにグループ化され、モデルは必要な場合にのみそれらを展開する。

## 適用される場面

仮想ツールが対処するのは、エージェントが効率的に推論できる以上のツールを抱えている場合である。GitHub は、MCP サーバーが一部のモデルの API 上限を超えるほどのツールを持ち込みうると報告している。ただし、グループ化だけでは失敗モードが残る。モデルが正しいグループを見つけるまでに誤ったグループをいくつも開いてしまう可能性があり、そのたびにキャッシュミス、余分なラウンドトリップ、失敗の機会が生じる。GitHub が仮想ツールを [[DefinedTerm/embedding-guided-tool-routing]] と組み合わせているのはこのためである。この手法とその報告された結果は、単一のベンダーが自社製品について説明したものに由来する。

## 関連用語

- [[DefinedTerm/embedding-guided-tool-routing]]
- [[DefinedTerm/model-context-protocol]]
