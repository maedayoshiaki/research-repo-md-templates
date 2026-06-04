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

軽微な修正（タイポ、1 関数の小修正）はプラン不要。

## How To Use（運用ルール）

- 作業中、`Living Sections` を**こまめに更新**する（後でまとめて書こうとしない）。
- スコープが変わったらプランを**書き直す**。
- 設計判断は `Approach` に**最大 5 案まで**併記し、選んだ理由を残す。
- 学習したい作業では、`Collaboration Mode`、`Human Coding Slots`、`Explain-back` を積極的に使う。
- ただし、軽微な修正や定型作業では `Human Coding Slots` を省略してよい。
- デザインパターン、実装スタイル、研究アルゴリズム、評価指標、前処理などを学ぶ場合は、できるだけ `Human Coding Slots` を使う。
- 完了したら `Outcomes & Retrospective` を埋め、要点を `MEMORY.md` へ。

## Collaboration Modes（AI との協働方法）

| Mode | 人間の役割 | AI の役割 | 適する作業 |
|------|------------|-----------|------------|
| `Human Driver` | 設計・実装の主担当 | ヒント、レビュー、テスト案 | 学びたい文法、PyTorch 基本、研究アルゴリズム |
| `Pair Programming` | 方針決定と主要実装 | 小さい実装案、レビュー、代替案 | 通常の研究コード開発 |
| `AI Draft → Human Rewrite` | 読解、修正、採否判断 | たたき台作成 | 定型処理、CLI、設定、ログ、テスト雛形 |
| `AI Delegate` | 仕様と検証の確認 | 実装の大部分 | GPU 高速化、CI、互換性対応、退屈なリファクタ |

迷ったら `Pair Programming`。
学びたい箇所は `Human Driver` に寄せる。

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
- **Collaboration Mode:** `Human Driver` / `Pair Programming` / `AI Draft → Human Rewrite` / `AI Delegate`
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

AI は実装前に、人間が書くと学習効果が高い部分を 1〜3 個提案する。
ただし、すべての作業で必須ではない。軽微な修正、rename、format、lint、設定の微修正、明らかに定型的な処理では省略してよい。

中核部分は完成コードを先に出さず、ヒント、疑似コード、入出力例、テスト観点に留める。

| Slot | 人間が書く部分 | 学習価値 | AI が出してよい支援 | 完了条件 |
|------|----------------|----------|----------------------|----------|
| 1 | {{例: Dataset.__getitem__ の実装}} | {{shape / dtype / 前処理の理解}} | {{疑似コード、入出力例、テスト案}} | {{小さいテストが通る}} |
| 2 | {{例: loss 関数の中核計算}} | {{数式とコードの対応理解}} | {{式の説明、境界条件}} | {{既知入力で期待値と一致}} |
| 3 | {{必要なら}} | {{...}} | {{...}} | {{...}} |

AI が実装してよい部分：

- {{例: CLI 引数、ログ出力、テスト雛形、設定ファイル、単純なリファクタ}}

AI が完成実装を出してはいけない部分：

- {{例: 研究アルゴリズムの核、モデル forward、評価指標の本体、設計パターンの採否判断}}

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
