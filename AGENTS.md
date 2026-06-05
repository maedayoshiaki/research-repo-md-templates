# AGENTS.md — AI Agent Guide

AI コーディングエージェント（Claude Code / Codex 等）向けの作業ルール。
人間向けの概要は `README.md`、Git ルールは `CONTRIBUTING.md` を参照する。

## Purpose

このテンプレートは、研究・実装・学習・Git 操作を小さく再開しやすく保つためのもの。
説明は短くし、必要な要点と例を残す。

## Read first

作業前に、必要な範囲だけ読む。

1. `README.md` — プロジェクト概要と Markdown の役割
2. `STATUS.md` — 現在の状態
3. `PLANS.md` — これから行う作業
4. `MEMORY.md` — 確定した前提・決定・落とし穴
5. `docs/AI_OUTPUT_EXAMPLES.md` — AI の回答例、Human Coding Slots、設計案比較の例
6. 関連する `docs/*` — 理論、実験、設計、用語

すべての Markdown を毎回読む必要はない。

## Core rules

- 変更は小さく、レビューしやすくする。
- 複数ファイルにまたがる変更では、先に短い方針を示す。
- 既存の命名、構成、文体を尊重する。
- 賢い実装より、読みやすい実装を優先する。
- 挙動、理論、使い方、設計が変わったら関連 Markdown を更新する。
- API キー、認証情報、個人情報、未公開データを Markdown やコードに書かない。

## Repository Human Involvement Profile

このリポジトリでは、AI コーディングエージェントにどこまで実装を委任し、人間がどこまで設計・実装・レビューに関与するかを最初に 1 つ選ぶ。

- **Selected Profile:** `{{L0 / L1 / L2 / L3 / L4}}`
- **Default Collaboration Mode:** `{{AI Delegate / AI Draft → Human Rewrite / Pair Programming / Human Driver}}`
- **Human Coding Requirement:** `{{none / review only / selective slots / core implementation / main implementation}}`
- **Reason:** {{このリポジトリでこの介入度を選ぶ理由}}

テンプレート使用開始時に 1 つだけ選ぶ。
選ばなかった Profile の詳細説明は削除してよい。
削除後、この節には選択した Profile だけを残す。

### Profile overview

| Profile | 目的 | 人間の実装量 | AI への委任 | 既定の協働モード |
|---|---|---:|---:|---|
| `L0 Speed First` | 最速で動かす | なし | 最大 | `AI Delegate` |
| `L1 Review Gate` | AI 実装を人間が読む | 少 | 大 | `AI Delegate` / `AI Draft → Human Rewrite` |
| `L2 Selective Human Slots` | 速度と学習の両立 | 中 | 中 | `Pair Programming` |
| `L3 Learning First` | 学習重視 | 多 | 補助 | `Pair Programming` / `Human Driver` |
| `L4 Human Driver` | 人間が主担当 | 最大 | 最小 | `Human Driver` |

迷ったら `L2 Selective Human Slots` を選ぶ。

### L0 — Speed First

#### Intent

最速で動くものを作る。
人間がコードを書くことは必須ではない。
研究アイデアの短期検証、単発スクリプト、使い捨ての解析、定型処理に向く。

#### Human responsibilities

人間は次を担当する。

- 目的、入力、出力、制約を決める
- 受け入れ条件を確認する
- 最終 diff と実行結果を確認する
- 研究上の前提、数式、実験条件に関わる変更だけレビューする

#### AI responsibilities

AI は次を担当してよい。

- 実装の大部分
- テスト雛形
- CLI、ログ、設定、ファイル I/O
- リファクタ
- ドキュメントの最低限の更新

#### AI may provide complete code

AI は完成実装を出してよい。
ただし、研究上の仮定、評価指標、数式の意味を勝手に確定してはいけない。

#### Human Coding Slots

原則不要。
AI は Human Coding Slots を提案しなくてよい。
人間が学習したいと明示した場合のみ、1 個だけ提案する。

#### Design alternatives

軽微な実装では不要。
非自明な設計判断、依存ライブラリ追加、公開 API 変更、破壊的変更では 2〜3 案を出す。

#### Explain-back

不要。
ただし、人間が求めた場合は、主要関数の入出力と変更方法を短く説明する。

#### Documentation

`docs/LEARNING.md` の更新は不要。
`STATUS.md` と `MEMORY.md` は、今後も参照する決定がある場合のみ更新する。

#### Done criteria

- 実装が動く
- 受け入れ条件を満たす
- 実行方法が分かる
- docs only / test skipped などの省略理由が PR に書かれている

### L1 — Review Gate

#### Intent

AI に実装を委任しつつ、人間がレビューで主導権を持つ。
人間がコードを書くことは必須ではないが、主要な変更点を読んで説明できる状態にする。

#### Human responsibilities

人間は次を担当する。

- 仕様と受け入れ条件を決める
- 主要 diff を読む
- 実行結果、テスト結果、失敗時の挙動を確認する
- 設計判断、依存追加、公開 API 変更を承認する

#### AI responsibilities

AI は次を担当してよい。

- 実装
- テスト
- リファクタ
- 設計案の比較
- PR 説明の下書き
- 変更点の要約

#### AI may provide complete code

AI は完成実装を出してよい。
ただし、主要な責務、入出力、変更方法を説明する。

#### Human Coding Slots

原則不要。
ただし、次の場合は AI が任意で 1〜2 個提案する。

- 人間が新しい API を学ぶ価値がある
- 研究コードの中核処理が含まれる
- 後で人間が修正する可能性が高い

提案しても、人間が実装する義務はない。
レビューだけでよい。

#### Design alternatives

非自明な設計では 2〜5 案を出す。
人間は採用案を確認し、過剰設計でないかを見る。

#### Explain-back

PR 前に、AI は次を短く提示する。

- 何を変更したか
- 主要な入出力
- テスト方法
- 人間が見るべき diff
- 変更しやすい箇所

#### Documentation

`docs/LEARNING.md` は任意。
再利用する知識、落とし穴、設計判断がある場合のみ更新する。

### L2 — Selective Human Slots

#### Intent

AI による高速化と、人間のコーディング経験の獲得を両立する。
人間はすべてを書かない。
学習価値が高い部分だけ、実装・修正・説明に関与する。

#### Human responsibilities

人間は次を担当する。

- 設計案の採否
- 研究アルゴリズム、評価指標、前処理、主要 API の確認
- AI が提案した Human Coding Slots のうち、必要なものの実装・修正・説明
- 完成後の explain-back

#### AI responsibilities

AI は次を担当してよい。

- 周辺実装
- 定型処理
- テスト雛形
- CLI、ログ、設定
- 型、docstring、軽いリファクタ
- 人間が書いたコードのレビュー
- Human Coding Slots の分割とヒント提示

#### Human Coding Slots

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

#### AI may provide complete code

Human Coding Slot に指定された中核部分では、AI はいきなり完成実装を出さない。
先に、疑似コード、入出力例、テスト観点、境界条件を出す。

Human Coding Slot ではない部分では、AI は完成実装を出してよい。

#### Design alternatives

非自明な設計判断では 2〜5 案を出す。
人間が採用案を選ぶ。
AI は、各案について次を説明する。

- 概要
- 長所
- 短所
- 学習価値
- 過剰設計の可能性
- より単純な代替案

#### Explain-back

人間は、少なくとも Human Coding Slot に関して次を説明できる状態にする。

- 入出力
- 責務
- なぜこの設計にしたか
- どこを変えれば拡張できるか
- どのテストで正しさを確認するか

#### Documentation

Human Coding Slot で扱った学習事項は、必要に応じて `docs/LEARNING.md` に短く残す。
設計判断は `PLANS.md`、`MEMORY.md`、または ADR に残す。

### L3 — Learning First

#### Intent

速度より学習を優先する。
AI は実装者ではなく、設計レビュー、ヒント提示、テスト設計、コードレビューの相手として振る舞う。

#### Human responsibilities

人間は次を担当する。

- 主要設計の選択
- 主要関数、主要クラス、研究アルゴリズムの実装
- デザインパターンや実装スタイルの採否判断
- 実装後の explain-back
- 学習事項の記録

#### AI responsibilities

AI は次を担当する。

- 設計案の比較
- 最小例
- 疑似コード
- 境界条件の整理
- テスト案
- コードレビュー
- バグ原因の説明
- リファクタ案

#### Human Coding Slots

AI は原則として 2〜4 個の Human Coding Slots を提案する。
少なくとも 1 個は人間が実装または書き直す。

Slot は、学習価値の高い単位にする。
大きすぎる場合は、関数単位、責務単位、テスト単位に分割する。

#### AI may provide complete code

中核部分の完成実装は、原則として先に出さない。
人間が実装した後に、レビュー、修正版、代替案を出す。

ただし、次は AI が完成実装してよい。

- CLI
- ログ
- 設定
- テストの boilerplate
- 型定義の補助
- 既存コードに合わせた単純な変換

#### Design alternatives

設計判断では、原則 3〜5 案を出す。
AI は推奨案を示してよいが、最終決定は人間が行う。

#### Explain-back

必須。
人間は PR 前に次を説明できる状態にする。

- 実装した中核処理
- 採用した設計
- 採用しなかった案
- テストの意味
- 次に自力で修正できる範囲

#### Documentation

`docs/LEARNING.md` を原則更新する。
必要に応じて `Code Reproduction` に、AI なしで再実装できる範囲を残す。

### L4 — Human Driver

#### Intent

人間のコーディング力を鍛える。
AI は完成コード生成者ではなく、教師、レビュー担当、設計相談相手として振る舞う。

#### Human responsibilities

人間は次を担当する。

- 設計
- 主要実装
- テストの中核
- デバッグ方針
- リファクタ判断
- 学習ログの記録

#### AI responsibilities

AI は次を担当する。

- 問題の分解
- 参考になる最小例
- 疑似コード
- API の説明
- テストケースの提案
- コードレビュー
- バグ原因の推定
- よりよい設計へのコメント

#### Human Coding Slots

全中核処理が Human Coding Slot の候補になる。
AI は最初に、実装対象を 3〜5 個の小さい Slot に分割する。

各 Slot では、AI は次に留める。

- 入出力仕様
- 期待される挙動
- 疑似コード
- テスト観点
- よくあるミス
- ヒント

#### AI may provide complete code

中核実装の完成コードは、人間が求めない限り出さない。
人間が一度実装した後であれば、AI は修正版や改善案を出してよい。

#### Design alternatives

必須。
設計判断では、AI は複数案を出し、人間が選ぶ。
人間は採用理由を説明する。

#### Explain-back

必須。
PR 前に、人間は次を説明する。

- なぜその実装にしたか
- どの設計案を捨てたか
- どこが拡張点か
- テストが何を保証するか
- 次回 AI なしで書けそうな範囲

#### Documentation

`docs/LEARNING.md` を更新する。
学習目的が強い場合は `Code Reproduction` も更新する。

## Human review required

次の変更は、人間の確認なしに確定しない。

- 数式、理論、研究上の前提
- 実験プロトコル、評価指標、データ形式
- アーキテクチャ、公開 API、ディレクトリ構成
- 新規依存ライブラリの追加
- 破壊的変更
- `MEMORY.md` に書かれた重要な前提の変更
- Git ルールや Markdown の役割分担の変更

## Task Collaboration Modes

タスク開始時に、`PLANS.md` で協働モードを選ぶ。
Task Collaboration Mode は、Repository Human Involvement Profile の範囲内でタスクごとに選ぶ。

| Mode | 人間の役割 | AI の役割 | 適する作業 |
|------|------------|-----------|------------|
| `Human Driver` | 設計・実装の主担当 | ヒント、レビュー、テスト案 | 学びたい文法、PyTorch 基本、研究アルゴリズム |
| `Pair Programming` | 方針決定と主要実装 | 小さい実装案、レビュー、代替案 | 通常の研究コード開発 |
| `AI Draft → Human Rewrite` | 読解、修正、採否判断 | たたき台作成 | 定型処理、CLI、設定、ログ、テスト雛形 |
| `AI Delegate` | 仕様と検証の確認 | 実装の大部分 | GPU 高速化、CI、互換性対応、退屈なリファクタ |

Profile ごとの目安：

- `L0`: 通常は `AI Delegate`
- `L1`: 通常は `AI Delegate` または `AI Draft → Human Rewrite`
- `L2`: 通常は `Pair Programming`
- `L3`: 通常は `Pair Programming` または `Human Driver`
- `L4`: 通常は `Human Driver`

リポジトリ既定より人間の介入度を上げるのは常に許可する。
下げる場合は `PLANS.md` または PR に理由を書く。

## Delegation and subagents

コーディングエージェントが subagent / task agent / specialist agent を使える場合は、必要に応じて使ってよい。

使ってよい例：

- 大きいコードベースの局所調査
- テスト失敗の原因調査
- 既存 API の利用箇所検索
- ドキュメント整合性チェック
- lint / format / 型エラーの機械的修正
- 設計案の追加調査

ただし、subagent の利用は Repository Human Involvement Profile を迂回する理由にならない。
次は main agent が責任を持つ。

- 最終方針の統合
- 人間レビューが必要な判断の提示
- Human Coding Slots の維持
- 数式、研究上の前提、評価指標の確認
- PR での説明と検証結果の報告

`L3` / `L4` では、subagent に中核実装を丸投げしない。
調査、レビュー、テスト案、局所的な補助に留める。

## Design alternatives

非自明な設計判断では、AI は実装前に代替案を出す。

- 原則として 2〜5 案を提示する。
- 重い設計、構造変更、デザインパターン採用では最大 5 案まで出す。
- 軽い判断では 2〜3 案でよい。
- 各案には、概要、長所、短所、学習価値を 1〜3 行で添える。
- 最終決定は人間が行い、採用理由を `PLANS.md`、`MEMORY.md`、または ADR に残す。

### Implementation style / pattern selection

実装スタイルや設計パターンの候補は固定リストに限定しない。
AI はタスクに合う有名な設計パターン、アーキテクチャパターン、実装スタイルを選び、必要に応じて比較する。

候補の例：

- Basic styles: procedural, functional, object-oriented, data-oriented
- GoF design patterns: Factory Method, Abstract Factory, Builder, Adapter, Facade, Decorator, Strategy, Command, Observer, State, Template Method, Visitor
- Architectural styles: Layered architecture, Pipeline, MVC, Hexagonal Architecture / Ports and Adapters, Clean Architecture
- Enterprise patterns: Repository, Unit of Work, Service Layer, Data Mapper
- Research-code styles: config-driven experiment, registry-based metric/loss selection, plugin-style method extension, script-first prototype

AI は、パターン名を出すだけで終わらない。次を説明する。

- そのスタイルやパターンを使う理由
- 今回の規模に対して過剰設計ではないか
- 人間が学べる設計上のポイント
- より単純な実装で十分な可能性
- 将来の拡張で有利になる条件

小さい実験コード、単発スクリプト、読み捨ての解析コードでは、simple procedural や functional pipeline を優先してよい。
有名なパターン名を無理に当てはめない。

## Planning

軽微な修正なら `PLANS.md` は不要。
次の場合は、着手前に `PLANS.md` に短い計画を書く。

- 複数ファイルにまたがる
- 新機能を追加する
- 大きめのリファクタを行う
- 数式やアルゴリズムを実装する
- 実験条件を変更する
- 人間が学びたい実装概念を含む
- Repository Human Involvement Profile から外れる進め方をする

計画は長くしない。目的、Profile、協働モード、手順、確認方法が分かればよい。

## Coding and learning

このリポジトリでは、実装とコーディング学習を同時に扱う。

- 非自明なコードには、選択理由を 1〜3 文で添える。
- コメントは「何をしているか」ではなく「なぜそうするか」を書く。
- 学習に有用な概念が出たら、Profile に応じて `docs/LEARNING.md` に短く残す。
- `docs/LEARNING.md` には、長い引用ではなく、自分の言葉で要点と小さなコード例を書く。
- AI が生成した主要コードは、人間が入出力、責務、変更方法を説明できる状態にする。

### Human Coding Slots

Human Coding Slots の扱いは Repository Human Involvement Profile に従う。

- `L0`: 原則不要
- `L1`: 任意。レビュー対象だけでもよい
- `L2`: 学習価値がある場合に 1〜3 個提案
- `L3`: 原則 2〜4 個提案し、少なくとも 1 個は人間が実装または書き直す
- `L4`: 中核処理を Human Coding Slots に分割し、人間が主導する

AI は、次のような場合には `Human Coding Slots` を積極的に提案する。

- 新しい言語機能、ライブラリ、API を学ぶとき
- 関数分割、クラス設計、責務分離を学ぶとき
- デザインパターンや実装スタイルを比較・採用するとき
- 研究アルゴリズム、loss、評価指標、前処理などの中核処理を書くとき
- 人間が今後も自力で修正・拡張できるようにしたい箇所があるとき

AI は次を提示する：

- **Human-written parts:** 人間が書くことを推奨する関数、クラス、処理
- **Reason:** なぜそこを人間が書くと学習効果が高いか
- **Hints only:** AI が出してよいヒント、疑似コード、入出力例、テスト観点
- **AI-assisted parts:** AI が書いてよい定型処理、周辺処理、補助コード
- **Explain-back target:** 実装後に人間が説明できるべき内容

`L2` 以上では、学習対象の中核部分について、AI はいきなり完成コードを出さない。
まず人間が書く範囲を提案し、人間が実装しやすい粒度に分割する。

例：

```md
### Human Coding Slots

| Slot | 人間が書く部分 | 学習価値 | AI が出してよい支援 | 完了条件 |
|------|----------------|----------|----------------------|----------|
| 1 | `Dataset.__getitem__` | shape / dtype / 前処理の理解 | 疑似コード、入出力例、テスト案 | 小さいテストが通る |
| 2 | loss の中核計算 | 数式とコードの対応理解 | 式の説明、境界条件 | 既知入力で期待値と一致 |
```

## Response examples for learning tasks

学習要素を含む実装タスクでは、必要に応じて次の形式で返答する。
特に、設計判断、デザインパターン、実装スタイル、研究アルゴリズム、評価指標、前処理、テスト設計を含む場合は、この形式を優先する。

1. **Task understanding:** 何を実装するか、変更が必要そうなファイル
2. **Repository profile:** 選択済み Profile と、このタスクでの上げ下げの有無
3. **Design alternatives:** 2〜5 案と、それぞれの長所・短所・学習価値
4. **Recommended Human Coding Slots:** Profile に応じて、人間が書くとよい箇所、理由、AI が出してよいヒントの範囲
5. **AI-assisted work:** AI が担当してよい補助実装、テスト、型、リファクタ、ドキュメント更新
6. **Checkpoints:** 人間が実装後に説明すべきこと、確認すべきテスト

軽微な修正や学習目的でない作業では、この形式を短縮または省略してよい。
具体的な回答例は `docs/AI_OUTPUT_EXAMPLES.md` を参照する。

### Learning-first areas

次の領域では、選択した Repository Human Involvement Profile に従って、人間の関与度を上げる。
`L0` / `L1` では AI が完成実装を出してよいが、設計・数式・評価指標の意味は説明する。
`L2` 以上では、必要に応じて Human Coding Slots を提案する。
`L3` / `L4` では、中核部分の完成実装を先に出さない。

- PyTorch の `Dataset`, `DataLoader`, `nn.Module`, training loop
- Python の基本設計、型、例外、ファイル I/O
- 研究アルゴリズムの中核処理
- データ構造の選定
- 評価指標、loss、前処理の設計
- デザインパターンや実装スタイルの採否判断

AI が出してよいもの：

- 最小例
- 疑似コード
- テスト案
- レビューコメント
- 代替設計案
- バグの原因説明

AI が避けるもの：

- Profile を無視していきなり全実装を完成させる
- 人間が理解していない抽象化を導入する
- 「一般的にはこう」として設計を確定する
- subagent の出力を未検証のまま統合する

例：

````md
### 2026-05-31: pathlib

`Path` を使うと、OS に依存しにくいパス操作ができる。

```python
from pathlib import Path

file_path = Path("data") / "input.csv"
```
````

## Markdown update rules

- `STATUS.md` は現在の状態を書く。
- `PLANS.md` は未来の作業を書く。
- `MEMORY.md` は今後も参照する確定情報を書く。
- `docs/LEARNING.md` は学習した実装概念を書く。
- `docs/THEORY.md` は数式、理論、アルゴリズムを書く。
- `docs/EXPERIMENTS.md` は実験条件、結果、考察を書く。
- `docs/ARCHITECTURE.md` はモジュール構成と依存関係を書く。

迷ったら、`README.md` の Documentation Map に従う。

## Git workflow

Git の詳細ルールは `CONTRIBUTING.md` に集約する。

基本手順：

1. `main` から作業ブランチを作る。
2. 小さく変更する。
3. 必要な検証を行う。
4. 関連 Markdown を更新する。
5. 小さく焦点を絞ったコミットを作る。
6. PR を開く。

## Verification

完了報告前に、可能な範囲で確認する。

```bash
{{make format}}
{{make lint}}
{{make typecheck}}
{{make test}}
```

ドキュメントのみの変更では、上記を省略してよい。
その場合は、PR に「docs only」と書く。

## Done criteria

作業完了の条件：

- 変更の目的が達成されている
- 変更範囲が小さく保たれている
- 必要な検証を行っている
- 関連 Markdown を更新している
- Repository Human Involvement Profile と担当範囲が分かる
- 残課題があれば `STATUS.md` または PR に書いている

## Project structure example

```text
.
├── AGENTS.md            # AI 向け作業ルール
├── CLAUDE.md            # Claude Code 用。AGENTS.md を参照
├── README.md            # 人間向け入口
├── CONTRIBUTING.md      # Git、ブランチ、コミット、PR のルール
├── PLANS.md             # これから行う作業計画
├── STATUS.md            # 現在の状態
├── MEMORY.md            # 確定した前提・決定・落とし穴
├── docs/
│   ├── AI_OUTPUT_EXAMPLES.md # AI の回答例
│   ├── LEARNING.md      # コーディング学習ログ
│   ├── ARCHITECTURE.md  # 実装構成・依存関係
│   ├── THEORY.md        # 数式・理論
│   ├── GLOSSARY.md      # 用語集
│   ├── EXPERIMENTS.md   # 実験ログ
│   └── adr/             # 重要な設計判断
├── src/{{package}}/
├── experiments/
└── tests/
```
