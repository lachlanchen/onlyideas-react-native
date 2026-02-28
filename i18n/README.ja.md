[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# OnlyIdeas Full Stack App

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20Android%20%7C%20Web-2ea44f)
![Expo](https://img.shields.io/badge/Expo-48-000020?logo=expo)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61dafb?logo=react)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-orange?logo=amazon-aws)
![Backend](https://img.shields.io/badge/Backend-AppSync%20%2B%20DynamoDB-ff9900)
![Storage](https://img.shields.io/badge/Storage-S3-569A31)
![Auth](https://img.shields.io/badge/Auth-Cognito-DD344C)
![License](https://img.shields.io/badge/License-Not%20Specified-lightgrey)

**OnlyIdeas** は、人々がアイデアを共有し収益化できるようにするフルスタックアプリケーションです。**AWS Amplify** と連携し、ユーザー認証、データ保存（AppSync & DynamoDB）、ファイルホスティング（S3）を提供します。**Expo** 経由で **iOS**、**Android**、**Web** で実行できます。

「OnlyFans 風」の機能に着想を得つつ、OnlyIdeas はユーザー投稿のアイデア、音楽、メディアを生成・分析・翻訳する AI ツールの統合も目指しています。

この README は、既存の README 内容と現在のソースファイルに基づいて拡張した、リポジトリ準拠のドラフトです。

## 概要 📌

### スタック一覧

| 領域 | 技術 |
|---|---|
| App framework | `React Native` + `Expo` |
| Navigation | `expo-router` |
| Auth + Data + Storage | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Database | `Amazon DynamoDB` (via Amplify GraphQL models) |
| File storage | `Amazon S3` |
| Targets | iOS, Android, Web |

OnlyIdeas では次を利用しています。

- 画面遷移とルートベース画面管理に `expo-router`。
- 認証、API、DataStore、ストレージに `aws-amplify` + `@aws-amplify/ui-react-native`。
- Amplify バックエンドカテゴリとして **Auth (Cognito)**、**API (AppSync GraphQL)**、**Storage (S3)**。

現在のユーザーフロー:

1. Amplify Authenticator でサインイン。
2. ホームフィードでクリエイター一覧（`User` レコード）を表示。
3. クリエイタープロフィールを開き、投稿とペイウォール状態を表示。
4. 必要に応じて画像を S3 にアップロードしつつ新規投稿を作成。

## 機能 ✨

- クリエイター一覧とプロフィールページ。
- Amplify UI Authenticator によるサインイン / サインアウト。
- 画像ピッカー連携付きの新規投稿作成。
- S3 への画像アップロードと画像取得。
- GraphQL ベースの `User` / `Post` モデル永続化。
- 1 つの Expo プロジェクトから iOS・Android・Web を起動可能。

## プロジェクト構成 🗂️

```text
.
├── app/
│   ├── _layout.js           # Amplify config + Authenticator wrapper
│   ├── index.js             # Home feed (users list)
│   ├── newPost.js           # Create post + optional image upload
│   └── user/[id].js         # Creator profile + posts
├── src/
│   ├── components/
│   │   ├── UserCard.js
│   │   ├── UserProfileHeader.js
│   │   └── Post.js
│   ├── graphql/             # Generated operations/schema artifacts
│   └── models/              # Amplify modelgen outputs
├── amplify/
│   └── backend/             # Amplify backend resources (auth/api/storage)
├── i18n/                    # Translation README directory (currently empty)
├── app.json
├── babel.config.js
├── index.js
└── package.json
```

## 前提条件 ✅

- Node.js 18+ 推奨。
- npm（lockfile は `package-lock.json`）。
- Expo 互換ツール環境:
  - iOS Simulator + Xcode（iOS ローカルシミュレーション用）。
  - Android Studio + SDK/emulator（Android ローカルシミュレーション用）。
- Amplify プロビジョニング用の AWS アカウント権限。
- バックエンドセットアップ用の Amplify CLI。

## インストール 🚀

### 1. リポジトリをクローン

既存の正規コマンドを保持:

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

このリポジトリで現在設定されている、リポジトリ準拠のリモート:

```bash
git clone git@github.com:lachlanchen/onlyideas-react-native.git
cd onlyideas-react-native
```

このリポジトリは **OnlyIdeas** プラットフォーム向けに特化されており、創造性と収益化に焦点を当てています。

### 2. 依存関係をインストール

プロジェクトルートで次を実行:

```bash
npm install
```

これにより、**Expo**、**React Native**、**aws-amplify** を含む必要な Node モジュールがインストールされます。

## AWS Amplify の設定と初期化 ☁️

1. **Amplify CLI をインストール**（未導入の場合）:

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. AWS 資格情報で **Amplify を設定**:

   ```bash
   amplify configure
   ```

   - AWS コンソールにサインインし、新規または既存の IAM ユーザーを使用。
   - `accessKeyId` と `secretAccessKey` を入力。
   - 新しいプロファイル名を設定（例: `onlyideas`）。

3. このプロジェクトで **Amplify を初期化**:

   ```bash
   amplify init
   ```

   推奨プロンプト:

   - Environment name: `dev`（または任意）
   - Default editor: 任意
   - Authentication method: `AWS profile`
   - Profile: 先ほど設定したものを選択

4. **Amplify バックエンドを push**:

   ```bash
   amplify push
   ```

これにより、OnlyIdeas 用の AWS バックエンド（Cognito、AppSync、S3 など）がプロビジョニングされます。

## アプリの実行 ▶️

**Expo** を使って各プラットフォームでアプリを起動します:

```bash
npx expo start
```

または package scripts:

| Script | Command | Purpose |
|---|---|---|
| `npm start` | `expo start` | Start Expo dev server |
| `npm run ios` | `expo start --ios` | Launch iOS simulator |
| `npm run android` | `expo start --android` | Launch Android emulator |
| `npm run web` | `expo start --web` | Run web target |

- `i` キーで iOS Simulator を開く（macOS + Xcode 必須）。
- `a` キーで Android エミュレーターを開く（Android Studio & SDK が必要）。
- `w` キーでブラウザで Web ビルドを開く。

### Web での実行

このプロジェクトでは **React Native** 専用ライブラリ（例: `@aws-amplify/ui-react-native`）を一部使用しているため、Web 向けバンドル時にエラーが出る場合はインポートを条件分岐で処理する必要があります。多くの場合 **web** はそのまま動作しますが、問題が起きた場合は次のいずれかを検討してください。

- ネイティブ専用のインポートを削除または置換する。
- Web ビルドをスキップし、ネイティブプラットフォームで開発を継続する。

## 設定メモ ⚙️

### 必須の生成ファイル: `src/aws-exports.js`

`app/_layout.js` は `../src/aws-exports` をインポートしますが、このファイルは Amplify により生成されるため、このリポジトリにはコミットされていません。`amplify init` + `amplify push` を実行すると生成されるはずです。

### Amplify バックエンド構成

`amplify/backend/backend-config.json` より、このプロジェクトには以下が含まれます。

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

追加のリポジトリ準拠な認証情報:

- AppSync のデフォルト認証は現在 `API_KEY` で、追加プロバイダーとして AWS IAM が設定されています。

### GraphQL データモデル

`amplify/backend/api/OnlyFansCloneApp/schema.graphql` で定義:

- `User` モデル: プロフィール項目（`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`）
- `Post` モデル: `text`、任意の `image`、`likes`、`userID` インデックス（`byUser`）

### Expo/Babel 設定

- `index.js` で async iterator polyfill と `expo-router/entry` を読み込み。
- `babel.config.js` には次を含む:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## 使用例 🧪

### 投稿の作成と公開

1. アプリを開いてサインイン。
2. ホーム画面で `New post` をタップ。
3. 投稿テキストを入力。
4. 必要に応じてライブラリから画像を選択。
5. `Post` をタップして画像をアップロードし、`Post` レコードを保存。

### ローカルバックエンド運用（一般的）

```bash
amplify status
amplify pull
amplify push
```

スキーマ/モデルを変更した場合は、環境に応じて Amplify CLI コマンドで必要なアーティファクトを再生成してください。

## 開発メモ 🛠️

- ルーティングは `app/` 配下の `expo-router` によるファイルベース方式。
- 現在のアプリは `DataStore` と直接 `API.graphql` mutation の両方を併用。
- 認証 `signIn` 時、`_layout.js` は `Hub` でイベントを監視し、対応する `User` レコード作成を試行。
- 現時点で `package.json` に専用の `test` / `lint` スクリプトは未定義。
- `i18n/` ディレクトリは存在し、言語別 README は今後追加予定（このドラフト時点）。
- 言語リンクは、この README 上部の単一オプション行として意図的に維持。

## トラブルシューティング 🧯

### `Cannot find module '../src/aws-exports'`

次を実行:

```bash
amplify init
amplify push
```

`src/aws-exports.js` がローカルで生成されていることを確認してください。

### 認証は成功するがユーザーフィードが空

- `Hub` の sign-in リスナーが実行され、ユーザー作成 mutation が成功したか確認。
- AppSync の認証モードと権限を確認。
- DynamoDB/AppSync コンソールで `User` レコードのデータを確認。

### 新規投稿で画像アップロードに失敗する

- Amplify バックエンドに S3 ストレージリソースが存在することを確認。
- 認証済みユーザーにアップロード権限があることを確認。
- ネットワーク接続を確認し、再認証後に再試行。

### Web ビルドでネイティブ専用インポートのエラーが出る

ネイティブ専用モジュールを条件付きでインポートするか、Web 互換性で問題が出る場合は iOS/Android 中心で開発してください。

## ロードマップ / 次のステップ 🧭

- **AI Integration**: 自動コンテンツ生成、音楽コード分析、翻訳をサポートするために、エンドポイントやサードパーティ API 呼び出し（例: OpenAI）を追加。
- **Monetization**: 収益化機能を再現したい場合は、サブスクリプションや決済機能（例: Stripe）を組み込み。
- **Deployment**: iOS / Android 向けスタンドアロンアプリ生成に [EAS Build](https://docs.expo.dev/eas/) などを利用。
- このファイル上部の言語リンクを使って `i18n/` 配下の README セットを拡張。

## 謝辞 🙌

- 元プロジェクト: [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app)。
- **OnlyIdeas** として再構成・リブランディングし、人々がアイデアを共有・収益化できるようにしつつ、音楽、言語翻訳、研究コラボレーション向け AI 機能の導入を計画。

元コードベースと機能の詳細は、元リポジトリの README を確認してください。

## コントリビュート 🤝

コントリビューション歓迎です。専用の `CONTRIBUTING.md` が追加されるまでは、次の軽量フローに従ってください。

1. リポジトリを fork。
2. 機能ブランチを作成。
3. 変更を小さく保ち、少なくとも 1 つの対象プラットフォームで検証。
4. セットアップ手順/再現手順を明記して Pull Request を作成。

Amplify リソースを変更する場合は、対応する `amplify/` の更新とマイグレーションノートを PR 説明に含めてください。

## ライセンス 📄

このリポジトリには現在 `LICENSE` ファイルが存在しません。

前提: メンテナーが明示的なライセンスを追加するまでは、デフォルトで all rights reserved です。

---

**OnlyIdeas** の開発を楽しみながら、AI 支援でユーザーのアイデアを保護し、価値化できるプラットフォームに仕上げてください。
