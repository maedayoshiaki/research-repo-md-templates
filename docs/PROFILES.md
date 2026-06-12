# PROFILES.md — Repository Human Involvement Profiles 詳細

`AGENTS.md` で選ぶ Repository Human Involvement Profile（L0〜L4）の詳細定義。
**Profile 定義の正本はこのファイルに置き、他の Markdown からは参照に留める**（表を複製しない）。
テンプレート使用開始時に Profile を 1 つ選んだら、選ばなかった Profile の節は削除してよい。

| Profile | 目的 | 人間の実装量 | AI への委任 | Human Coding Slots | AI が完成実装を出せる範囲 |
|---|---|---:|---:|---|---|
| `L0 Speed First` | 最速で動かす | なし | 最大 | 原則不要 | ほぼ全体。研究前提・数式・評価指標は確認する |
| `L1 Review Gate` | AI 実装を人間が読む | 少 | 大 | 任意。レビュー対象だけでもよい | 全体。ただし主要 diff と設計意図を説明する |
| `L2 Selective Human Slots` | 速度と学習の両立 | 中 | 中 | 学習価値がある場合に 1〜3 個 | Slot 以外の周辺実装 |
| `L3 Learning First` | 学習重視 | 多 | 補助 | 原則 1〜3 個の `Design Vertical Slice`。少なくとも 1 個は人間が実装または書き直す | 文脈整理、類似実装、周辺実装、テスト雛形、機械的処理 |
| `L4 Human Driver` | 人間が主担当 | 最大 | 最小 | 中核処理を小さい Slot に分割 | 原則として中核実装は出さない |

迷ったら `L2 Selective Human Slots` を選ぶ。

## L0 — Speed First

### Intent

最速で動くものを作る。
人間がコードを書くことは必須ではない。
研究アイデアの短期検証、単発スクリプト、使い捨ての解析、定型処理に向く。

### Human responsibilities

人間は次を担当する。

- 目的、入力、出力、制約を決める
- 受け入れ条件を確認する
- 最終 diff と実行結果を確認する
- 研究上の前提、数式、実験条件に関わる変更だけレビューする

### AI responsibilities

AI は次を担当してよい。

- 実装の大部分
- テスト雛形
- CLI、ログ、設定、ファイル I/O
- リファクタ
- ドキュメントの最低限の更新

### AI may provide complete code

AI は完成実装を出してよい。
ただし、研究上の仮定、評価指標、数式の意味を勝手に確定してはいけない。

### Human Coding Slots

原則不要。
AI は Human Coding Slots を提案しなくてよい。
人間が学習したいと明示した場合のみ、1 個だけ提案する。

### Design alternatives

軽微な実装では不要。
非自明な設計判断、依存ライブラリ追加、公開 API 変更、破壊的変更では 2〜3 案を出す。

### Explain-back

不要。
ただし、人間が求めた場合は、主要関数の入出力と変更方法を短く説明する。

### Documentation

`docs/LEARNING.md` の更新は不要。
`STATUS.md` と `MEMORY.md` は、今後も参照する決定がある場合のみ更新する。

### Done criteria

- 実装が動く
- 受け入れ条件を満たす
- 実行方法が分かる
- docs only / test skipped などの省略理由が PR に書かれている

## L1 — Review Gate

### Intent

AI に実装を委任しつつ、人間がレビューで主導権を持つ。
人間がコードを書くことは必須ではないが、主要な変更点を読んで説明できる状態にする。

### Human responsibilities

人間は次を担当する。

- 仕様と受け入れ条件を決める
- 主要 diff を読む
- 実行結果、テスト結果、失敗時の挙動を確認する
- 設計判断、依存追加、公開 API 変更を承認する

### AI responsibilities

AI は次を担当してよい。

- 実装
- テスト
- リファクタ
- 設計案の比較
- PR 説明の下書き
- 変更点の要約

### AI may provide complete code

AI は完成実装を出してよい。
ただし、主要な責務、入出力、変更方法を説明する。

### Human Coding Slots

原則不要。
ただし、次の場合は AI が任意で 1〜2 個提案する。

- 人間が新しい API を学ぶ価値がある
- 研究コードの中核処理が含まれる
- 後で人間が修正する可能性が高い

提案しても、人間が実装する義務はない。
レビューだけでよい。

### Design alternatives

非自明な設計では 2〜5 案を出す。
人間は採用案を確認し、過剰設計でないかを見る。

### Explain-back

PR 前に、AI は次を短く提示する。

- 何を変更したか
- 主要な入出力
- テスト方法
- 人間が見るべき diff
- 変更しやすい箇所

### Documentation

`docs/LEARNING.md` は任意。
再利用する知識、落とし穴、設計判断がある場合のみ更新する。

## L2 — Selective Human Slots

### Intent

AI による高速化と、人間のコーディング経験の獲得を両立する。
人間はすべてを書かない。
学習価値が高い部分だけ、実装・修正・説明に関与する。

### Human responsibilities

人間は次を担当する。

- 設計案の採否
- 研究アルゴリズム、評価指標、前処理、主要 API の確認
- AI が提案した Human Coding Slots のうち、必要なものの実装・修正・説明
- 完成後の explain-back

### AI responsibilities

AI は次を担当してよい。

- 周辺実装
- 定型処理
- テスト雛形
- CLI、ログ、設定
- 型、docstring、軽いリファクタ
- 人間が書いたコードのレビュー
- Human Coding Slots の分割とヒント提示

### Human Coding Slots

AI は、学習価値がある場合に 1〜3 個の Human Coding Slots を提案する。

各 Slot には次を書く。

- Human-written part
- Reason
- Hints only
- AI-assisted parts
- Explain-back target
- Done condition

人間は、提案された Slot のすべてを実装する必要はない。
タスクの目的、時間、学習優先度に応じて選ぶ。

### AI may provide complete code

Human Coding Slot に指定された中核部分では、AI はいきなり完成実装を出さない。
先に、疑似コード、入出力例、テスト観点、境界条件を出す。

Human Coding Slot ではない部分では、AI は完成実装を出してよい。

### Design alternatives

非自明な設計判断では 2〜5 案を出す。
人間が採用案を選ぶ。
AI は、各案について次を説明する。

- 概要
- 長所
- 短所
- 学習価値
- 過剰設計の可能性
- より単純な代替案

### Explain-back

人間は、少なくとも Human Coding Slot に関して次を説明できる状態にする。

- 入出力
- 責務
- なぜこの設計にしたか
- どこを変えれば拡張できるか
- どのテストで正しさを確認するか

### Documentation

Human Coding Slot で扱った学習事項は、必要に応じて `docs/LEARNING.md` に短く残す。
設計判断は `PLANS.md`、`MEMORY.md`、または ADR に残す。

## L3 — Learning First

### Intent

速度より学習を優先する。
AI は実装者ではなく、設計レビュー、ヒント提示、テスト設計、コードレビューの相手として振る舞う。

### Human responsibilities

人間は次を担当する。

- 主要設計の選択
- 主要関数、主要クラス、研究アルゴリズムの実装
- デザインパターンや実装スタイルの採否判断
- 実装後の explain-back
- 学習事項の記録

### AI responsibilities

AI は次を担当する。

- 設計案の比較
- 最小例
- 疑似コード
- 境界条件の整理
- テスト案
- コードレビュー
- バグ原因の説明
- リファクタ案

### Human Coding Slots

AI は原則として 1〜3 個の Human Coding Slots を `Design Vertical Slice` として提案する
（詳細は [`L3_DESIGN_VERTICAL_SLICE.md`](./L3_DESIGN_VERTICAL_SLICE.md)）。
少なくとも 1 個は人間が実装または書き直す。

Slot は、学習価値の高い単位にする。
大きすぎる場合は、関数単位、責務単位、テスト単位に分割する。

### AI may provide complete code

中核部分の完成実装は、原則として先に出さない。
人間が実装した後に、レビュー、修正版、代替案を出す。

ただし、次は AI が完成実装してよい。

- CLI
- ログ
- 設定
- テストの boilerplate
- 型定義の補助
- 既存コードに合わせた単純な変換

### Design alternatives

設計判断では、原則 3〜5 案を出す。
AI は推奨案を示してよいが、最終決定は人間が行う。

### Explain-back

必須。
人間は PR 前に次を説明できる状態にする。

- 実装した中核処理
- 採用した設計
- 採用しなかった案
- テストの意味
- 次に自力で修正できる範囲

### Documentation

`docs/LEARNING.md` を原則更新する。
必要に応じて `Code Reproduction` に、AI なしで再実装できる範囲を残す。

## L4 — Human Driver

### Intent

人間のコーディング力を鍛える。
AI は完成コード生成者ではなく、教師、レビュー担当、設計相談相手として振る舞う。

### Human responsibilities

人間は次を担当する。

- 設計
- 主要実装
- テストの中核
- デバッグ方針
- リファクタ判断
- 学習ログの記録

### AI responsibilities

AI は次を担当する。

- 問題の分解
- 参考になる最小例
- 疑似コード
- API の説明
- テストケースの提案
- コードレビュー
- バグ原因の推定
- よりよい設計へのコメント

### Human Coding Slots

全中核処理が Human Coding Slot の候補になる。
AI は最初に、実装対象を 3〜5 個の小さい Slot に分割する。

各 Slot では、AI は次に留める。

- 入出力仕様
- 期待される挙動
- 疑似コード
- テスト観点
- よくあるミス
- ヒント

### AI may provide complete code

中核実装の完成コードは、人間が求めない限り出さない。
人間が一度実装した後であれば、AI は修正版や改善案を出してよい。

### Design alternatives

必須。
設計判断では、AI は複数案を出し、人間が選ぶ。
人間は採用理由を説明する。

### Explain-back

必須。
PR 前に、人間は次を説明する。

- なぜその実装にしたか
- どの設計案を捨てたか
- どこが拡張点か
- テストが何を保証するか
- 次回 AI なしで書けそうな範囲

### Documentation

`docs/LEARNING.md` を更新する。
学習目的が強い場合は `Code Reproduction` も更新する。
