---
title: "Brain/Hands/Session の分離"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/brain-hands-session-split.md"
source_commit: "b0cc6ca63c7e8c23683ba90cc3b5cf0b4690d315"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "AI エージェントを、それぞれ独立に差し替え可能な 3 つの構成要素へと切り離すアーキテクチャパターン。Brain（モデルと、それを呼び出すハーネスのループ）、Hands（ツールが実際に実行される、サンドボックス化された一時的な環境）、そして Session（あらゆる思考・ツール呼び出し・観測を追記のみで記録するイベントログ）である。"
---

Brain/Hands/Session の分離とは、Anthropic が「Scaling Managed Agents: Decoupling the brain from the hands」と題した記事で示した、長時間稼働する AI エージェントを、それぞれ独立に差し替えられる 3 つの構成要素へと分けて構築するためのパターンである。Brain はモデルと、それを呼び出すハーネスのループである。Hands は、ツールが実際に実行される、サンドボックス化された一時的な実行環境である。Session は、あらゆる思考・ツール呼び出し・観測を記録する、追記のみのイベントログである。

## 使われ方

このパターンは [[SoftwareApplication/claude-managed-agents]] の背後にあるアーキテクチャ上の発想である。Anthropic の枠組みでは「ハーネスのあらゆる構成要素は、モデルが自力では何をできないかについての仮定を符号化している」とされる — 3 つの構成要素が結合していると、仮定が古びたとき（たとえば、かつては明示的なプランナーを必要としたモデルが、いまや自力で計画を立てるようになったとき）、システム全体を一度に変更せざるをえなくなる。これらを切り離すことでハーネスは状態を持たなくなり、サンドボックスは「ペットではなく家畜」となり、Brain のクラッシュが実行そのものを失わせることもなくなる。新しいコンテナが `wake(sessionId)` を呼び出し、イベントログから状態を再構成すればよい。Anthropic は、サンドボックスの準備が整う前に推論を開始できるようになったことで、最初のトークンまでの時間が p50 でおよそ 60%、p95 で 90% 超も短縮されたと報告している。

Google の Gemini Enterprise Agent Platform は、アーキテクチャとしてはこれと同じ brain/hands/session の分離であり、ただそれがプラットフォーム規模で製品化され、チームがゼロから組み上げるのではなく開発キットとともに束ねて提供されているものだと説明されている（[[SoftwareApplication/gemini-enterprise-agent-platform]] を参照）。

## 適用される場面

このパターンが当てはまるのは、長時間の稼働が見込まれるエージェントを構築あるいはホストする場合である。状態を持たないハーネスと永続的なイベントログこそが、長い実行を、コンテナ障害に対して脆いものではなく復旧可能なものにするからである。セッションをイベントログとして持つ部分がなければ、コンテナの障害はそのままセッションの失敗であり、デバッグは古いスナップショットに頼らざるをえない。それがあれば、エージェントの記憶は、たまたま動いているプロセスが何であれ、それとは独立に問い合わせ可能な成果物となる。セキュリティ上も重要である。モデルが生成したコードが走るサンドボックスから資格情報に手が届かないようにしておくことは、Anthropic が Managed Agents においてこの分離に帰している利点のひとつである。

## 関連用語

[[DefinedTerm/long-running-agent]], [[SoftwareApplication/claude-managed-agents]], [[SoftwareApplication/gemini-enterprise-agent-platform]], [[Organization/anthropic]]
