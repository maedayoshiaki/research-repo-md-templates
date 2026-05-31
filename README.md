# Research & Dev Repo Template

> **English (summary):** A compact Markdown scaffold for research & development repositories where humans and AI coding agents work together. **`AGENTS.md` is the core** AI operation guide. Use only the files you need, keep each Markdown file short, and make coding, learning, and Git workflow easy to resume.
> <!-- この英語サマリーは配布用の任意項目です。不要なら削除して構いません。 -->

AI コーディングエージェント（Claude Code / Codex 等）と人間が**協働**で研究開発リポジトリをきれいに運用するための雛形。
**中心は `AGENTS.md`**（AI への運用規約）。他のファイルはそれを支える。

> このリポジトリは GitHub の **テンプレートリポジトリ**として配布される想定です。
> 配布する側は Settings → General → **Template repository** を ON にすると「Use this template」ボタンが出ます。

<!-- ▼▼ セットアップが終わったら、ここから区切り線（---）までを削除し、下を自分のプロジェクト README にしてください ▼▼ -->

## How To Use This Template

1. 上部の **「Use this template」→ Create a new repository** で自分のリポを作る。
2. 下記の **プレースホルダ／TODO を埋める**（最重要は `AGENTS.md`）。
3. 仕組みの全体像は [`TEMPLATE_GUIDE.md`](./TEMPLATE_GUIDE.md) を参照（把握後は削除可）。

## Template Policy

このテンプレートは、Markdown ファイルを増やすことではなく、研究・実装・学習・Git 操作を再開しやすくすることを目的とする。
各 Markdown ファイルには明確な役割を持たせ、短い要点と具体例を中心に記述する。

## Filling In TODOs（プレースホルダの埋め方）

プレースホルダは 2 種類：

- **`{{...}}`** … 自分の値に置き換える。例: `{{package}}` → `mylib`
- **`<!-- TODO: ... -->`** … 対応が必要な箇所の目印。HTML コメントなので表示はされない。埋めたら削除する。

置き換えの例（before → after）：

```text
Project Overview: {{時系列データから状態を推定する…}}  →  本プロジェクトは … を推定する。
- セットアップ: {{uv sync}}                              →  - セットアップ: uv sync
| src/{{package}}/ | 本体 |                              →  | src/mylib/ | 本体 |
LICENSE: Copyright (c) 2026 {{YOUR NAME / ORG}}          →  Copyright (c) 2026 Taro Yamada
```

**まずここから（`AGENTS.md` が主体）：**

- `Project Overview` — プロジェクトの 1〜2 文
- `Directory Structure` — 実際の構成に合わせる
- `Commands` — 実コマンド・実スタックに合わせる

**次に（必要なものだけ）：**

- `LICENSE` — `{{YOUR NAME / ORG}}` を自分／組織名に
- `CLAUDE.md` — 基本そのまま（`@AGENTS.md` を参照する）。固有メモがあれば追記
- `docs/ARCHITECTURE.md` — 採用するアーキ様式・Module Map を確定
- `docs/THEORY.md` — 数式を扱うなら記号表・式から
- `docs/LEARNING.md` — コーディング学習を記録するなら残す
- この README 下部の本体（`{{プロジェクト名}}` 等）
- 使わない doc は削除してよい（規模別の取捨は [`TEMPLATE_GUIDE.md`](./TEMPLATE_GUIDE.md)）

> ヒント：全部を一度に埋めない。**`AGENTS.md` だけ埋めて走り出す**のが最小構成。
> 普遍ルールを全リポで効かせたいなら、`AGENTS.md` の Policies を `~/.claude/CLAUDE.md` にも置くとよい。

<!-- ▲▲ ここまで削除 ▲▲ -->

---

# {{プロジェクト名}}

{{1〜2 文の説明。何をするプロジェクトか。}}

> このファイルは**人間向け**の入口。AI コーディングエージェント向けの運用規約は `AGENTS.md`（Claude Code は `CLAUDE.md` 経由で参照）。

## Quickstart

```bash
{{uv sync}}    # セットアップ
{{make run}}   # 実行
{{make test}}  # テスト
```

## Requirements

- {{Python 3.10+ など}}
- {{依存管理ツール}}

## Documentation Map

| ファイル | 役割 | 更新するタイミング |
|------|------|------|
| `README.md` | プロジェクトの概要、始め方、主要ファイルへの入口 | 使い方や入口が変わったとき |
| `AGENTS.md` | AI エージェント向けの作業ルール | AI の作業方針を変えるとき |
| `CONTRIBUTING.md` | Git、ブランチ、コミット、PR のルール | 開発フローを変えるとき |
| `PLANS.md` | これから行う作業計画 | 複数ステップの作業を始めるとき |
| `STATUS.md` | 現在の進捗、未解決事項、次にやること | 作業の開始時と終了時 |
| `MEMORY.md` | 長期的に残す決定事項、前提、重要な知見 | 今後も参照する知見が確定したとき |
| `docs/LEARNING.md` | コーディング学習ログ、理解した概念、復習項目 | 新しい実装概念を学んだとき |
| `docs/THEORY.md` | 数式、理論、アルゴリズムの説明 | 理論や式を追加・修正したとき |
| `docs/EXPERIMENTS.md` | 実験条件、結果、考察 | 実験を行ったとき |
| `docs/ARCHITECTURE.md` | 実装構成、モジュール設計、依存関係 | 構成や責務を変えたとき |
| `docs/GLOSSARY.md` | 用語、略語、表記ゆれの整理 | 重要語を追加したとき |
| `docs/adr/` | 重要な設計判断の記録 | 後から理由を追跡したい判断をしたとき |

## License

[MIT](./LICENSE)
