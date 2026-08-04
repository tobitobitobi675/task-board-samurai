# CLAUDE.md

このファイルは、このリポジトリで作業する Claude Code (claude.ai/code) 向けのガイダンスです。

## プロジェクト概要

task-board-samurai プロジェクト。

(プロジェクトの詳細が固まり次第、目的・技術スタック・ディレクトリ構成などをここに追記してください。)

## Git 運用ルール

- **コードを変更するたびに、コミットしてGitHubにプッシュすること。** 変更を溜め込まず、意味のある単位（1機能・1修正など）ごとにコミット・プッシュを行う。
- コミットメッセージは変更内容が分かるように簡潔に書く（例: `fix: ログイン時のバリデーションエラーを修正`）。
- プッシュ先ブランチや force push など、破壊的・共有状態に影響する操作を行う場合は事前にユーザーに確認する。
- pre-commit / CI などのフックは `--no-verify` で無視せず、失敗した場合は原因を修正してから再度コミットする。
- シークレットや `.env` などの機密情報を含むファイルは絶対にコミットしない。

## デプロイ先

- 本番環境: GitHub Pages — https://tobitobitobi675.github.io/task-board-samurai/
- `main` ブランチに push すると、GitHub Actions (`.github/workflows/deploy.yml`) が自動的にビルド・デプロイを実行する。
- デプロイ状況は `gh run list --repo tobitobitobi675/task-board-samurai` で確認できる。
- リポジトリは GitHub Pages 利用のため Public 設定にしている。

## 技術スタック

- ビルドツール: Vite
- フレームワーク: React 19 (JSX、`react`/`react-dom`)
- 言語: JavaScript（TypeScript は未導入）
- Lint: oxlint
- 状態管理: React の `useState` / `useEffect` のみ（外部の状態管理ライブラリは使用しない）
- データ永続化: ブラウザの `localStorage`（`JSON.stringify` / `JSON.parse` で保存・復元）
- CI/CD: GitHub Actions（`.github/workflows/deploy.yml`）

## コンポーネントの命名規約

- コンポーネントファイル・関数名は `PascalCase`（例: `App.jsx` の `function App()`）。
- イベントハンドラ・ロジック関数は `動詞 + 名詞` の `camelCase`（例: `addTask`, `toggleTask`, `deleteTask`）。
- CSS クラス名は `kebab-case`（例: `task-form`, `task-list`, `task.done`）。状態を表すクラスは `done` のように単純な形容詞/状態名を追加する形にする。
- 1 コンポーネント = 1 ファイル（`ComponentName.jsx` + 必要に応じて `ComponentName.css`）とし、コンポーネントが増えてきたら `src/components/` 配下に切り出す。

## 開発コマンド

- `npm install`: 依存パッケージのインストール
- `npm run dev`: 開発サーバーの起動（Vite）
- `npm run build`: 本番ビルド
- `npm run lint`: Lint 実行（oxlint）
- `npm run preview`: ビルド成果物のプレビュー

## アーキテクチャ

- Vite + React (JSX) 構成。
- `src/App.jsx`: タスクボードのメインコンポーネント（タスクの追加・完了切り替え・削除）。
- `src/App.css`: タスクボードのスタイル。
- `src/main.jsx`: エントリーポイント。
