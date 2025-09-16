# timelogger-web

[![ci](https://github.com/commew/timelogger-web/actions/workflows/ci.yml/badge.svg)](https://github.com/commew/timelogger-web/actions/workflows/ci.yml)
[![chromatic](https://github.com/commew/timelogger-web/actions/workflows/chromatic.yml/badge.svg)](https://github.com/commew/timelogger-web/actions/workflows/chromatic.yml)

時間管理を行うウェブアプリケーションのフロントエンド用リポジトリになります。

Timelogger frontend built with Next.js and TypeScript. Track tasks and time with an authentication-enabled, Storybook-driven UI and a typed OpenAPI client.

## Features

- タスクの開始/停止/完了などの時間計測機能
- OIDC/NextAuth による認証
- Storybook/Chromatic による UI カタログとビジュアルレビュー
- OpenAPI スキーマからの型生成（`openapi-typescript`）と API モック（Prism, MSW）
- Jest + Testing Library によるユニットテスト

## Tech Stack

- Next.js 13 / React 18 / TypeScript
- UI: Mantine, Emotion
- Auth: NextAuth
- Validation: Zod
- Docs & UI: Storybook, Chromatic
- Testing: Jest, @testing-library/react, MSW
- API: OpenAPI schema, Prism mock server, `openapi-typescript`

## Scripts

```
npm run dev                 # 開発サーバーを起動 (http://localhost:5656)
npm run build               # 本番ビルド
npm run start               # 本番サーバーを起動 (http://localhost:5656)
npm run test                # テスト実行
npm run lint                # Lint 一括実行 (eslint, prettier, next)
npm run format              # Prettier/Eslint 自動整形
npm run storybook           # Storybook 起動 (http://localhost:6006)
npm run build-storybook     # Storybook ビルド
npm run chromatic           # Chromatic へアップロード (要トークン)
npm run api-mock:start      # Prism による API モック (http://localhost:5757)
npm run generate:schema     # OpenAPI から型生成
```

## Getting Started

本リポジトリのコントリビューターは [ローカル開発環境構築手順](https://github.com/commew/timelogger-web/blob/main/docs/setup.md) を参考にローカル PC 上に開発環境の構築をお願いします。

[CONTRIBUTING](https://github.com/commew/timelogger-web/blob/main/.github/CONTRIBUTING.md) の確認もお願いします。

環境構築には https://vercel.com/commew への参加が必要です。

申請に関しては @muchoco-dev までお願いします。

以下の URL から最新の Storybook を確認出来ますので UI の実装はいつでも確認が可能です。（GitHub へのログインが必要になります。）

https://main--63d52217f1430a5ad69846cd.chromatic.com

## Links

- Project board/Issues: GitHub Issues/Projects
- Storybook (Chromatic): https://main--63d52217f1430a5ad69846cd.chromatic.com

## License

This project is licensed under the terms of the MIT License. See `LICENSE` for details.
