---
title: "Brain/Hands/Session の分離"
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
  description: "AI エージェントを、互いに独立して置き換え可能な 3 つのコンポーネントに切り離すアーキテクチャパターン。Brain（モデルと、それを呼び出すハーネスのループ）、Hands（アクションを実行するサンドボックスとツール）、Session（セッションのイベントを記録する追記専用のログ）の 3 つから成る。"
---

Brain/Hands/Session の分離とは、Anthropic が
[[BlogPosting/scaling-managed-agents-decoupling-the-brain-from-the-hands]] で示した、長時間稼働する
AI エージェントを構築するためのパターンであり、エージェントを、それぞれが独立して障害を起こしたり置き換えられたりできる 3 つのコンポーネントに分ける。
Brain は Claude とそのハーネス、すなわちモデルを呼び出してそのツール呼び出しを振り分けるループである。Hands はアクションを実行するサンドボックスとツールである。Session は起きたことすべてを記録する追記専用のログである。
それぞれが、他のコンポーネントについてほとんど前提を置かないインターフェースとなる。

## 用法

このパターンは [[SoftwareApplication/claude-managed-agents]] のアーキテクチャである。Anthropic はこれをオペレーティングシステムとの類比で説明している。オペレーティングシステムはハードウェアを、プロセスやファイルのように、その下にあるハードウェアよりも長く生き残る抽象へと仮想化した。同様にこのパターンは「これらのインターフェースの形については意見を持つが、その背後で何が動くかについては意見を持たない」ことを目指している。ハーネスには Claude が自力ではできないことについての前提が組み込まれており、その前提はモデルの向上とともに古くなっていくからである。Anthropic が挙げる例は、あるモデルの [[DefinedTerm/context-anxiety]] に対処するためにコンテキストリセットを追加したハーネスであり、後のモデルではその振る舞いが消えてしまい、リセットは無用の重荷として残った。

Anthropic は、当初 3 つのコンポーネントすべてを単一のコンテナで動かしていたと述べている。これにより、そのコンテナは「ペットとキャトル（pets versus cattle）」の意味での「ペット」になってしまった。コンテナが障害を起こせばセッションは失われ、デバッグにはしばしばユーザーデータを抱えたコンテナ内でシェルを開く必要があり、ハーネスはあらゆるリソースが自分の隣にあることを前提としていた。分離後は、ハーネスはサンドボックスを他のツールと同じように呼び出す（`execute(name, input) →
string`）。そのため、コンテナの障害はツール呼び出しのエラーとなり、新しいコンテナをプロビジョニングできる。また、セッションログがハーネスの外にあるため、障害を起こしたハーネスは `wake(sessionId)` で再起動し、`getSession(id)` でログを取得して最後のイベントから再開できる。Anthropic によれば、必要なときにだけコンテナをプロビジョニングするようにしたことで、最初のトークンまでの時間（time-to-first-token）が p50 で約 60%、p95 で 90% 超短縮された。また、同じ分離によって、1 つの Brain が多数の Hands と連携したり、多数のステートレスな Brain を同時に起動したりできるようになったという。

Session は長いコンテキストの扱い方も変える。Anthropic はこれを Claude のコンテキストウィンドウと区別している。[[DefinedTerm/compaction]] やコンテキストのトリミングのように何を残すかについて不可逆な判断を下すのではなく、Session はすべてのイベントを永続的に保存し、ハーネスがその一部を選び出せるようにする。イベントがモデルに届く前のあらゆる変換はハーネスに委ねられる。

Addy Osmani による長時間稼働エージェントの概説は、Google の Gemini Enterprise Agent Platform を、アーキテクチャとしては同じ brain/hands/session の分離であり、それがプラットフォーム規模で製品化され、チームがゼロから組み立てるのではなく開発キットと一緒に提供されているものだと説明している（[[SoftwareApplication/gemini-enterprise-agent-platform]] を参照）。

## 適用される場面

- **条件。** Anthropic はこのパターンを長期にわたるエージェントをホストするためのものとして示している。そこでは、ハーネスの外にある永続的なイベントログこそが、コンテナやハーネスの障害後に実行を回復可能にするものであり、またエージェントが単一のシェルを超えた実行環境に到達する必要が生じうる。
- **前提。** モデルが複数の実行環境について推論し、どこに作業を送るかを判断できることを前提としている。Anthropic は、以前のモデルにはそれができなかったため、当初は単一のコンテナから始めたと述べている。
- **セキュリティ。** サンドボックスをハーネスから分離することは、Anthropic が、Claude の生成したコードが実行されるサンドボックスから認証情報に到達できないようにするための方法であり、これによってプロンプトインジェクションが環境から認証情報を単純に読み取ることを防いでいる。Git トークンは初期化時にサンドボックスのリモートに組み込まれ、MCP の認証情報はプロキシによってボールトから取得される。
- **確立の度合い。** これは、あるベンダーが自社のホスト型サービスの設計について述べたものであり、性能の数値もそのサービスから得られたものである。Osmani の概説は、この分離を複数のマネージドなエージェントランタイムの根底にあるパターンとして扱っている。

## 関連用語

[[DefinedTerm/long-running-agent]], [[DefinedTerm/meta-harness]], [[DefinedTerm/agent-harness]],
[[SoftwareApplication/claude-managed-agents]], [[SoftwareApplication/gemini-enterprise-agent-platform]],
[[Organization/anthropic]]
