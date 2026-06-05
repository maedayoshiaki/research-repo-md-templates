# PLANS.md — タスクの計画（ExecPlan）

**未来**を扱うファイル。「これから何をするか」の設計図。
完了したプランは要点を `MEMORY.md` へ昇格させ、ここからは削除/アーカイブする。
進行中のプランが複数になったら `plans/NNN-slug.md`（例: `plans/001-add-sampler.md`）に分割してもよい。

## When To Write A Plan（いつ計画するか）

次のいずれかなら、着手前にプランを書く：

- 複数ファイルにまたがる
- 新機能・大きなリファクタ
- 1 時間以上かかりそう
- 数式・アルゴリズムの新規実装
- 人間が学びたい実装概念を含む
- Repository Human Involvement Profile から外れる進め方をする

軽微な修正（タイポ、1 関数の小修正）はプラン不要。

## How To Use（運用ルール）

- 作業中、`Living Sections` を**こまめに更新**する（後でまとめて書こうとしない）。
- スコープが変わったらプランを**書き直す**。
- 設計判断は `Approach` に**最大 5 案まで**併記し、選んだ理由を残す。
- タスクでは、まず `Repository Profile` を確認し、その範囲内で `Collaboration Mode` を選ぶ。
- 学習したい作業では、Profile に応じて `Human Coding Slots`、`Explain-back` を積極的に使う。
- ただし、`L0` / `L1` や軽微な修正・定型作業では `Human Coding Slots` を省略してよい。
- デザインパターン、実装スタイル、研究アルゴリズム、評価指標、前処理などを学ぶ場合は、できるだけ `Human Coding Slots` を使う。
- コーディングエージェントが subagent を使える場合は、調査・レビュー・テスト案・機械的修正に使ってよい。ただし Profile や人間レビューを迂回しない。
- 完了したら `Outcomes & Retrospective` を埋め、要点を `MEMORY.md` へ。

## Repository Human Involvement Profiles（リポジトリ全体の介入度）

| Profile | 目的 | Human Coding Slots | AI が完成実装を出せる範囲 |
|---|---|---|---|
| `L0 Speed First` | 最速で動かす | 原則不要 | ほぼ全体。研究前提・数式・評価指標は確認する |
| `L1 Review Gate` | AI 実装を人間が読む | 任意。レビュー対象だけでもよい | 全体。ただし主要 diff と設計意図を説明する |
| `L2 Selective Human Slots` | 速度と学習の両立 | 学習価値がある場合に 1〜3 個 | Slot 以外の周辺実装 |
| `L3 Learning First` | 学習重視 | 原則 2〜4 個。少なくとも 1 個は人間が実装または書き直す | 周辺実装、テスト雛形、機械的処理 |
| `L4 Human Driver` | 人間が主担当 | 中核処理を小さい Slot に分割 | 原則として中核実装は出さない |

## Collaboration Modes（AI との協働方法）

Task Collaboration Mode は、Repository Human Involvement Profile の範囲内でタスクごとに選ぶ。

| Mode | 人間の役割 | AI の役割 | 適する作業 |
|------|------------|-----------|------------|
| `Human Driver` | 設計・実装の主担当 | ヒント、レビュー、テスト案 | 学びたい文法、PyTorch 基本、研究アルゴリズム |
| `Pair Programming` | 方針決定と主要実装 | 小さい実装案、レビュー、代替案 | 通常の研究コード開発 |
| `AI Draft → Human Rewrite` | 読解、修正、採否判断 | たたき台作成 | 定型処理、CLI、設定、ログ、テスト雛形 |
| `AI Delegate` | 仕様と検証の確認 | 実装の大部分 | GPU 高速化、CI、互換性対応、退屈なリファクタ |

目安：

- `L0`: 通常は `AI Delegate`
- `L1`: 通常は `AI Delegate` または `AI Draft → Human Rewrite`
- `L2`: 通常は `Pair Programming`
- `L3`: 通常は `Pair Programming` または `Human Driver`
- `L4`: 通常は `Human Driver`

## Task Categories（必要に応じて分ける）

計画が混ざる場合は、タスクを次の3種類に分ける。

- **Research tasks:** 理論、仮説、実験設計、評価
- **Implementation tasks:** 実装、テスト、リファクタ
- **Learning tasks:** Git、言語仕様、ライブラリ、設計パターンの学習

例：

```md
### Milestones / Steps

#### Research tasks
- [ ] 評価指標を決める

#### Implementation tasks
- [ ] データ読み込み処理を実装する
- [ ] テストを追加する

#### Learning tasks
- [ ] pytest fixture の使い方を理解する
```

---

<!-- ▼▼ ここから 1 プランのテンプレート。コピーして使う ▼▼ -->

## Plan: {{プランの短いタイトル}}

- **Status:** `Draft` / `Active` / `Blocked` / `Done`
- **Owner:** {{担当（人間 / AI / Pair）}}
- **Repository Profile:** `L0 Speed First` / `L1 Review Gate` / `L2 Selective Human Slots` / `L3 Learning First` / `L4 Human Driver`
- **Collaboration Mode:** `Human Driver` / `Pair Programming` / `AI Draft → Human Rewrite` / `AI Delegate`
- **Profile Override:** `none` / `stricter` / `looser`
- **Override Reason:** {{既定より人間の介入度を上げる/下げる理由。なければ none}}
- **Created / Updated:** {{YYYY-MM-DD}} / {{YYYY-MM-DD}}
- **Related:** {{issue #, docs/THEORY.md の式番号, docs/ARCHITECTURE.md の節 など}}

### Goal & Non-Goals

- **Goal:** {{このプランで達成すること（1〜3 文）}}
- **Non-Goals:** {{今回はやらないこと（スコープを狭めるために明記）}}

### Context & Constraints

{{背景・前提・制約。理論的背景は docs/THEORY.md、設計制約は docs/ARCHITECTURE.md を参照}}

### Learning Objectives

このタスクで人間が理解すること：

- [ ] {{関連する文法・API}}
- [ ] {{設計判断}}
- [ ] {{テスト方法}}
- [ ] {{性能・メモリ・数値安定性の注意点}}

### Human Coding Slots

Human Coding Slots の扱いは Repository Profile に従う。

- `L0`: 原則不要
- `L1`: 任意。レビュー対象だけでもよい
- `L2`: 学習価値がある場合に 1〜3 個提案
- `L3`: 原則 2〜4 個提案し、少なくとも 1 個は人間が実装または書き直す
- `L4`: 中核処理を Human Coding Slots に分割し、人間が主導する

`L2` 以上では、中核部分の完成コードを先に出さず、ヒント、疑似コード、入出力例、テスト観点に留める。

| Slot | 人間が書く部分 | 学習価値 | AI が出してよい支援 | 完了条件 |
|------|----------------|----------|----------------------|----------|
| 1 | {{例: Dataset.__getitem__ の実装}} | {{shape / dtype / 前処理の理解}} | {{疑似コード、入出力例、テスト案}} | {{小さいテストが通る}} |
| 2 | {{例: loss 関数の中核計算}} | {{数式とコードの対応理解}} | {{式の説明、境界条件}} | {{既知入力で期待値と一致}} |
| 3 | {{必要なら}} | {{...}} | {{...}} | {{...}} |

AI が実装してよい部分：

- {{例: CLI 引数、ログ出力、テスト雛形、設定ファイル、単純なリファクタ}}

AI が完成実装を先に出すべきでない部分（主に `L2` 以上）：

- {{例: 研究アルゴリズムの核、モデル forward、評価指標の本体、設計パターンの採否判断}}

### Subagent Use（任意）

コーディングエージェントが subagent を使える場合のみ記入する。

| 用途 | Subagent に任せる範囲 | Main agent / Human が確認すること |
|---|---|---|
| {{例: 既存 API 調査}} | {{検索、候補列挙}} | {{採用判断、設計への統合}} |
| {{例: テスト失敗調査}} | {{ログ分析、原因候補}} | {{修正方針、実装責任}} |

Subagent の出力は未確認情報として扱い、main agent が統合してから人間に提示する。

### Approach（検討した案 — 最大 5 案）

> 非自明な設計はここで案を並べ、**人間が選ぶ**。重い設計では最大 5 案、軽い判断では 2〜3 案でよい。自明なら 1 案でよい。
> 実装スタイルや設計パターンは固定リストに限定しない。GoF patterns、architecture patterns、enterprise application patterns、research-code patterns、functional / procedural / object-oriented styles などから、タスクに合うものを選ぶ。

| 案 | 実装スタイル / パターン | 参照元・分類 | 概要 | 長所 | 短所 | 学習価値 | 採用判断 |
|----|--------------------------|--------------|------|------|------|----------|----------|
| A | {{例: Simple procedural}} | {{Basic style}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |
| B | {{例: Strategy pattern}} | {{GoF / Behavioral}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |
| C | {{例: Repository pattern}} | {{Enterprise application pattern}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |
| D | {{例: Pipeline architecture}} | {{Architecture pattern}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |
| E | {{必要なら追加}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

- **採用案:** {{A / B / C / D / E}}
- **理由:** {{なぜこれを選んだか。より単純な実装では不十分か、過剰設計でないかも書く}}

### Milestones / Steps

- [ ] {{ステップ 1}}
- [ ] {{ステップ 2}}
- [ ] {{ステップ 3}}
- [ ] テスト追加・検証スタック通過
- [ ] STATUS / MEMORY 更新
- [ ] 必要なら `docs/LEARNING.md` 更新

### Explain-back（理解確認）

人間が自分の言葉で説明する：

- この実装は何をするか：{{...}}
- 主な入出力は何か：{{...}}
- なぜこの設計にしたか：{{...}}
- どこを変更すれば拡張できるか：{{...}}
- どのテストで正しさを確認するか：{{...}}

### Risks & Compatibility

- {{破壊的変更の有無（あれば人間確認: AGENTS.md）}}
- {{依存追加・パフォーマンス・数値安定性などのリスク}}

---

### Living Sections（作業中に更新する。見出しは英語のまま固定）

#### Progress

{{今どこまで進んだか。日付つきで追記}}

#### Surprises & Discoveries

{{想定外だったこと・気づき。MEMORY の落とし穴に昇格する候補}}

#### Decision Log

{{作業中に下した判断と理由。例: 「2024-xx-xx 〇〇は△△の理由で採用しない」}}

#### Outcomes & Retrospective

{{完了後に記入。結果・残課題・次にやるなら何を変えるか}}

<!-- ▲▲ テンプレートここまで ▲▲ -->
