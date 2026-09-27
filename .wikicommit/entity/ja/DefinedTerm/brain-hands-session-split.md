---
title: "Brain/Hands/Session 分割"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/brain-hands-session-split.md"
source_commit: "f948f309cb907fd940528e22bdf1a82e1e673130"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントを、それぞれ独立に交換可能な 3 つのコンポーネントに分離するアーキテクチャパターン。3 つとは、Brain（モデルと、それを呼び出すハーネスのループ）、Hands（行動を実行するサンドボックスとツール）、Session（セッションのイベントを記録する追記専用のログ）である。"
---

Brain/Hands/Session 分割は、Anthropic が [[BlogPosting/scaling-managed-agents-decoupling-the-brain-from-the-hands]] で示したパターンで、長時間稼働する AI エージェントを、それぞれが独立に故障したり交換されたりしうる 3 つのコンポーネントに分けて構築するものである。Brain は Claude とそのハーネス、すなわちモデルを呼び出してそのツール呼び出しを振り分けるループである。Hands は行動を実行するサンドボックスとツールである。Session は、起きたことすべてを記録する追記専用のログである。それぞれが、他のコンポーネントについてほとんど仮定を置かないインターフェースになる。

## 用法

このパターンは [[SoftwareApplication/claude-managed-agents]] のアーキテクチャである。Anthropic はこれをオペレーティングシステムとのアナロジーで説明している。オペレーティングシステムはハードウェアを、プロセスやファイルといった、その下のハードウェアよりも長く生き残る抽象へと仮想化した。このパターンは「これらのインターフェースの形については明確な立場をとるが、その背後で何が動くかについては立場をとらない（opinionated about the shape of these interfaces, not about what runs behind them）」ことを目指している。ハーネスは Claude が単独ではできないことについての仮定を組み込んでおり、それらの仮定はモデルが改善するにつれて古びていくからである。その例として挙げられているのは、あるモデルの [[DefinedTerm/context-anxiety]] に対処するためにコンテキストのリセットを追加したハーネスで、後のモデルではその振る舞いが消えてしまい、リセットは無用の重荷として残った。

Anthropic は、当初は 3 つのコンポーネントすべてを単一のコンテナで動かしていたと述べている。そのためそのコンテナは、ペットと家畜（pets versus cattle）の比喩でいう「ペット」になっていた。コンテナが故障すればセッションは失われ、デバッグにはユーザーデータを保持していることの多いコンテナでシェルを開く必要があり、ハーネスはあらゆるリソースが自分のすぐ隣にあると仮定していた。分離後は、ハーネスはサンドボックスを他のツールと同じように呼び出す（`execute(name, input) → string`）ため、故障したコンテナはツール呼び出しのエラーとなり、新しいコンテナをプロビジョニングできる。また、セッションログはハーネスの外にあるため、故障したハーネスは `wake(sessionId)` で再起動し、`getSession(id)` でログを取得して、最後のイベントから再開できる。Anthropic は、必要なときにだけコンテナをプロビジョニングするようにしたことで、最初のトークンまでの時間が p50 でおよそ 60%、p95 で 90% 以上短縮されたと報告しており、同じ分離によって、1 つの Brain が多数の Hands と連携したり、多数のステートレスな Brain を同時に起動したりできるようになったとしている。

Session は、長いコンテキストの扱い方も変える。Anthropic はこれを Claude のコンテキストウィンドウと区別している。[[DefinedTerm/compaction]] やコンテキストのトリミングのように何を残すかについて不可逆な判断を下すのではなく、Session はすべてのイベントを永続的に保存し、ハーネスにその一部を選び出させる。一方、イベントがモデルに届く前の変換はすべてハーネスに委ねられる。

Addy Osmani による長時間稼働エージェントの概説は、Google の Gemini Enterprise Agent Platform を、アーキテクチャとしては同じ brain/hands/session 分割であり、チームがゼロから組み立てるのではなく、プラットフォーム規模で製品化され開発キットと一体で提供されたものだと説明している（[[SoftwareApplication/gemini-enterprise-agent-platform]] を参照）。

## 適用される場面

- **条件。** Anthropic はこのパターンを、長期にわたるタスクを担うエージェントをホストするためのものとして提示している。そこでは、ハーネスの外にある永続的なイベントログこそが、コンテナやハーネスの故障後に実行を復旧可能にするものであり、またエージェントが単一のシェルを超えた実行環境に到達する必要が生じうる。
- **前提。** モデルが複数の実行環境について推論し、作業をどこに送るかを判断できることを前提としている。Anthropic は、以前のモデルにはそれができなかったため、当初は単一のコンテナから始めたと述べている。
- **セキュリティ。** サンドボックスをハーネスから分離することは、Claude が生成したコードが動くサンドボックスから認証情報に到達できないようにするための Anthropic の方法であり、プロンプトインジェクションが環境から認証情報を単純に読み取れないようにしている。Git トークンは初期化時にサンドボックスのリモートに組み込まれ、MCP の認証情報はプロキシによってボールトから取得される。
- **確立の度合い。** これは一つのベンダーが自社のホスト型サービスの設計について述べたものであり、性能の数値もそのサービスのものである。Osmani の概説は、この分割を複数のマネージド型エージェントランタイムの根底にあるパターンとして扱っている。

## 関連用語

[[DefinedTerm/long-running-agent]], [[DefinedTerm/meta-harness]], [[DefinedTerm/agent-harness]], [[SoftwareApplication/claude-managed-agents]], [[SoftwareApplication/gemini-enterprise-agent-platform]], [[Organization/anthropic]]
