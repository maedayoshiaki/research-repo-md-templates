# CONTRIBUTING — Git Rules

人間の開発者向けの Git ルール。
AI 併用時の作業方針は `AGENTS.md` を参照する。

## Setup

```bash
{{uv sync}}
```

## Branch rules

- `main` に直接コミットしない。
- 作業ごとにブランチを作る。
- ブランチ名は次の形式にする。

```text
feature/<short-name>
fix/<short-name>
docs/<short-name>
experiment/<short-name>
```

例：

```text
feature/add-loader
fix/path-bug
docs/update-theory
experiment/baseline-test
```

## Commit rules

コミットメッセージは次の形式にする。

```text
<type>: <summary>
```

使用する `type` は以下に限定する。

| type | 用途 |
|---|---|
| `feat` | 新機能 |
| `fix` | バグ修正 |
| `docs` | ドキュメント修正 |
| `refactor` | 挙動を変えない整理 |
| `test` | テスト追加・修正 |
| `exp` | 実験コード・実験条件の追加 |
| `chore` | その他の作業 |

例：

```text
feat: add csv loader
fix: correct output path
docs: update theory explanation
exp: add baseline experiment
```

## Pull request rules

PR には以下を書く。

- 何を変更したか
- なぜ変更したか
- どう確認したか
- 関連する Issue、実験、またはドキュメント

## Before opening a PR

可能な範囲で検証スタックを通す。

```bash
{{make format}}
{{make lint}}
{{make typecheck}}
{{make test}}
```

ドキュメントのみの変更では、上記を省略してよい。
その場合は PR に `docs only` と書く。

## Working with AI agents

- AI に丸投げせず、開発者が最終判断する。
- 数式、理論、実験条件、アーキテクチャ、公開 API、破壊的変更は人間が確認する。
- AI には、必要に応じて短い理由や代替案を出させる。
- 作業後に `STATUS.md` を更新し、確定事項は `MEMORY.md` に残す。

## Review checklist

- [ ] 変更範囲が小さい
- [ ] 必要な検証を行った
- [ ] 関連 Markdown を更新した
- [ ] 数式・理論・実験条件の変更は人間が確認した
- [ ] コミットとブランチ名がルールに従っている
