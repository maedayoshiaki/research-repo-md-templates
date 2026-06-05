# LEARNING.md — Coding Learning Log

コーディング中に学んだことを短く残すファイル。
調べ物の全文保存ではなく、理解した要点、実際に使った小さな例、復習項目だけを書く。

## Purpose

AI に任せきりにせず、人間が理解した設計・文法・ライブラリ・パターンを短く残す。
長い講義ノートではなく、次に同じ実装を読む・直すための学習ログにする。

## Rules

- 調べた内容をそのまま貼らない。
- 自分の言葉で 1〜3 行に要約する。
- 実際に使った小さなコード例を残す。
- 理解が曖昧なものは `Review later` に入れる。
- プロジェクト固有の確定事項は `MEMORY.md` に書く。
- AI 生成コードを採用した場合も、人間が入出力・責務・変更方法を説明できるようにする。
- 学習目的の実装では、必要に応じて、AI の助けなしで再実装できる範囲を `Code Reproduction` に残す。
- 実装スタイルや設計パターンを採用した場合は、名前だけでなく、なぜその抽象化が必要だったかを書く。

## Profile-Based Usage

`docs/LEARNING.md` の更新頻度は Repository Human Involvement Profile に従う。

| Profile | 更新方針 |
|---|---|
| `L0 Speed First` | 原則不要。大きな落とし穴、再利用する知識がある場合のみ書く。 |
| `L1 Review Gate` | レビューで理解した主要 API、設計判断、失敗原因がある場合のみ書く。 |
| `L2 Selective Human Slots` | Human Coding Slot で扱った概念を必要に応じて短く残す。 |
| `L3 Learning First` | 学習目的の PR では原則更新する。 |
| `L4 Human Driver` | 実装後の理解確認、再実装できる範囲、復習項目を記録する。 |

## Learning-first Areas

次は、学習価値が高い領域である。
ただし、人間が主導する度合いは Repository Human Involvement Profile に従う。

- `L0` / `L1`: AI に実装を委任してよい。人間はレビューで主要な入出力、責務、変更方法を確認する。
- `L2`: 必要な部分だけ Human Coding Slots にする。
- `L3` / `L4`: 人間が主導し、AI はヒント、最小例、レビュー、テスト案を出す。

対象例：

- PyTorch の基本構成: `Dataset`, `DataLoader`, `nn.Module`, training loop
- Python の基本設計: 型、例外、ファイル I/O、関数分割
- 研究アルゴリズムの中核処理
- データ構造、loss、評価指標、前処理の設計
- デザインパターンや実装スタイルの採否判断

AI に任せやすいもの：

- GPU 高速化の詳細
- CI、format、lint、型チェックの設定
- 定型的なテスト雛形
- ログ、CLI、設定ファイルの下書き
- 互換性対応、単純なリファクタ

## Implementation Style / Pattern Notes

実装スタイルや設計パターンを学習対象にした場合は、必要に応じてここに短く残す。
候補は固定しない。GoF patterns、architecture patterns、enterprise application patterns、research-code patterns、procedural / functional / object-oriented styles などから、実際に検討したものを書く。

### {{YYYY-MM-DD}}: {{style / pattern name}}

- Category: {{例: GoF / Behavioral, Architecture pattern, Basic style, Research-code style}}
- Used in: `{{src/...}}`
- Repository Profile: `{{L0 / L1 / L2 / L3 / L4}}`
- Human Coding Slot: {{該当する場合。なければ none}}
- Why considered: {{なぜ候補にしたか}}
- Why adopted / rejected: {{採用または不採用の理由}}
- Simpler alternative: {{より単純な実装で十分だったか}}
- What I learned: {{自分の言葉で 1〜3 行}}

Small example:

```{{language}}
{{small_code_example}}
```

## PyTorch Roadmap

PyTorch を使うプロジェクトでは、必要に応じて進捗を残す。

- [ ] Tensor の `shape` / `dtype` / `device`
- [ ] `Dataset` / `DataLoader`
- [ ] `nn.Module` と `forward`
- [ ] loss と metric の違い
- [ ] `autograd`
- [ ] optimizer / scheduler
- [ ] train / eval loop
- [ ] checkpoint 保存と復元
- [ ] GPU / mixed precision
- [ ] profiling / bottleneck analysis

## Learned

### {{YYYY-MM-DD}}: {{学んだ概念}}

{{何を理解したかを 1〜3 行で書く。}}

```{{language}}
{{small_code_example}}
```

- Used in: `{{src/...}}`
- Related: `{{issue / PR / docs/...}}`
- Repository Profile: `{{L0 / L1 / L2 / L3 / L4}}`
- Human Coding Slot: {{該当する場合。なければ none}}

Explain-back:

- 入出力: {{...}}
- どこで使うか: {{...}}
- よくあるミス: {{...}}
- 次に自分で書けそうな範囲: {{...}}

## Code Reproduction

AI の助けなしで再実装できるかを確認する。
主に `L3 Learning First` / `L4 Human Driver` の学習目的 PR で、必要に応じてこの欄をコピーして追記する。

### {{YYYY-MM-DD}}: {{再実装した内容}}

- Original task: {{何を実装したか}}
- Repository Profile: `{{L0 / L1 / L2 / L3 / L4}}`
- Human Coding Slot: {{PLANS.md / PR の該当 slot}}
- Re-implemented from memory: Yes / Partial / No
- Time taken: {{例: 20 min}}
- Checked by: {{例: unit test / small input / review}}

Mistakes:

- {{間違えた点}}

What I can write next time:

- {{次に自力で書けそうな範囲}}

What I still need AI for:

- {{まだ補助が必要な範囲}}

## Review later

- {{復習したい概念}}
