# timelogger-web

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

## Links

- Project board/Issues: GitHub Issues/Projects
- Storybook (Chromatic): https://main--63d52217f1430a5ad69846cd.chromatic.com

## License

This project is licensed under the terms of the MIT License. See `LICENSE` for details.
