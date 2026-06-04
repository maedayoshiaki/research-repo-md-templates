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

## Learning-first Areas

次は、できるだけ人間が主導して書く。
AI はヒント、最小例、レビュー、テスト案を出す。

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

Explain-back:

- 入出力: {{...}}
- どこで使うか: {{...}}
- よくあるミス: {{...}}
- 次に自分で書けそうな範囲: {{...}}

## Code Reproduction

AI の助けなしで再実装できるかを確認する。
学習目的の PR では、必要に応じてこの欄をコピーして追記する。

### {{YYYY-MM-DD}}: {{再実装した内容}}

- Original task: {{何を実装したか}}
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
