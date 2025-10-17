# AGENTS.md

## 概要

`GitHub Pages` にデプロイされる静的ファイルのみを管理するモノリポジトリ。
各ディレクトリは専用の個別リポジトリで管理。

## ディレクトリ構成

- `index.html` — ルート (空)
- `docs/` — Markdown ドキュメント
- `markdown-preview/` — Markdown プレビューツール (marked + highlight.js + mermaid + DOMPurify を CDN 経由で読み込む単一 HTML)
- `webadb-tool/` — WebADB ツール (事前ビルド済みの静的アセット)
