# Changelog

このテンプレートの変更履歴。GitHub のテンプレートリポジトリは派生先に更新が**自動で伝播しない**ため、
利用者はタグ間の差分（例: `git diff v0.1.0..v0.2.0 -- AGENTS.md`）で変更を確認し、必要な分だけ取り込む。

## [Unreleased]

### Fixed
- 存在しない節番号への参照（`AGENTS.md §1` / `§3` / `§8`）を見出し名による参照に修正
- L3 の Human Coding Slots 数の記述ゆれ（2〜4 個 / 1〜3 個）を「1〜3 個の Design Vertical Slice」に統一

### Changed
- Profile 詳細（L0〜L4）を `docs/PROFILES.md` に分離し、`AGENTS.md` を約半分に軽量化
- `PLANS.md` の Profile / Collaboration Modes の重複表をポインタ化（Single Source of Truth 化）
- `README.md` / `AGENTS.md` / `TEMPLATE_GUIDE.md` のドキュメントマップを実ファイル構成と一致させた
- `docs/AI_OUTPUT_EXAMPLES.md` を「毎回読む」対象から「必要時に読む」対象に変更

### Added
- `docs/PROFILES.md`（Profile 定義の正本）
- CI: markdownlint + lychee による Markdown / リンク検査（`.github/workflows/docs-lint.yml`）
- `CITATION.cff`（GitHub の「Cite this repository」対応）
- `CHANGELOG.md`（このファイル）

## [0.1.0] - 2026-06-12

- 初回タグ。既存テンプレート一式。
