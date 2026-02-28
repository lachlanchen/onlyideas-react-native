[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# OnlyIdeas Full Stack App

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20Android%20%7C%20Web-2ea44f)
![Expo](https://img.shields.io/badge/Expo-48-000020?logo=expo)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61dafb?logo=react)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-orange?logo=amazon-aws)
![Backend](https://img.shields.io/badge/Backend-AppSync%20%2B%20DynamoDB-ff9900)
![Storage](https://img.shields.io/badge/Storage-S3-569A31)
![Auth](https://img.shields.io/badge/Auth-Cognito-DD344C)
![License](https://img.shields.io/badge/License-Not%20Specified-lightgrey)
![GitHub contributors](https://img.shields.io/github/contributors/lachlanchen/onlyideas-react-native?style=flat-square)
![Open issues](https://img.shields.io/github/issues/lachlanchen/onlyideas-react-native?style=flat-square)

**OnlyIdeas** は人々がアイデアを共有し、収益化できるようにするフルスタックアプリケーションです。**AWS Amplify** と連携し、ユーザー認証、データ保存（AppSync と DynamoDB）、ファイルホスティング（S3）を統合しています。**Expo** 経由で **iOS**、**Android**、**Web** で動作します。

OnlyFans スタイルの機能に着想を得て、OnlyIdeas ではユーザー投稿のアイデア・音楽・メディアを生成、分析、翻訳する AI ツールの統合も目指しています。

この README は、既存の README 内容と現在のソースファイルを基に拡張した、リポジトリ準拠のドラフトです。

## 概要 📌

### スタックを一望

| 領域 | 技術 |
|---|---|
| App framework | `React Native` + `Expo` |
| Navigation | `expo-router` |
| 認証 + データ + ストレージ | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Database | `Amazon DynamoDB` (via Amplify GraphQL models) |
| ファイル保存 | `Amazon S3` |
| ターゲット | iOS, Android, Web |

OnlyIdeas では次を使用します。

- ナビゲーションとルートベース画面に `expo-router`。
- 認証、API、DataStore、ストレージに `aws-amplify` + `@aws-amplify/ui-react-native`。
- Amplify バックエンドカテゴリとして **Auth (Cognito)**、**API (AppSync GraphQL)**、**Storage (S3)**。

現在のユーザーフロー:

1. Amplify Authenticator でサインインします。
2. ホームフィードにクリエイター一覧（`User` レコード）を表示します。
3. クリエイタープロフィールを開き、投稿とペイウォール状態を確認します。
4. 必要に応じて S3 に画像をアップロードし、投稿を作成します。

## 機能 ✨

- クリエイター一覧とプロフィールページ。
- Amplify UI Authenticator を使ったサインイン / サインアウト。
- 画像ピッカーを統合した新規投稿作成。
- S3 への画像アップロードおよび画像取得。
- GraphQL バックエンドの `User` と `Post` モデル永続化。
- 1 つの Expo プロジェクトから iOS、Android、Web の各ターゲットを起動。

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
- Expo 対応ツール:
  - iOS Simulator + Xcode（iOS ローカルシミュレーション用）
  - Android Studio + SDK/emulator（Android ローカルシミュレーション用）
- Amplify プロビジョニング用の AWS アカウント。
- バックエンド構築用の Amplify CLI。

## インストール 🚀

### 1. リポジトリをクローン

ワークフローに合うリモートを選択してください:

| コマンド | 備考 |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | 歴史的/アーカイブ参照 |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | 現行リポジトリ（推奨） |

次に、対象のプロジェクトディレクトリを開きます:

```bash
cd onlyideas-react-native
```

このリポジトリは **OnlyIdeas** プラットフォーム向けに特化され、クリエイティブ性と収益化に焦点を当てています。

### 2. 依存関係をインストール

プロジェクトルートで実行します。

```bash
npm install
```

これで **Expo**、**React Native**、**aws-amplify** を含む必要な Node モジュールがインストールされます。

## AWS Amplify の設定と初期化 ☁️

1. **Amplify CLI** をインストールします（未導入の場合）:

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. AWS 資格情報で **Amplify** を設定します:

   ```bash
   amplify configure
   ```

   - AWS コンソールへサインインし、新規または既存の IAM ユーザーを使用します。
   - `accessKeyId` と `secretAccessKey` を入力します。
   - 新しいプロファイル名を設定します（例: `onlyideas`）。

3. このプロジェクトで **Amplify** を初期化します:

   ```bash
   amplify init
   ```

   推奨プロンプト:

   - Environment name: `dev`（または任意）
   - Default editor: 任意
   - Authentication method: `AWS profile`
   - Profile: 直前に設定したものを選択

4. **Amplify バックエンドを push** します:

   ```bash
   amplify push
   ```

これにより、OnlyIdeas 用の AWS バックエンド（Cognito、AppSync、S3 など）がプロビジョニングされます。

## アプリ起動 ▶️

**Expo** を使って各プラットフォームでアプリを起動します:

```bash
npx expo start
```

または package scripts:

| スクリプト | コマンド | 目的 |
|---|---|---|
| `npm start` | `expo start` | Expo 開発サーバーを起動 |
| `npm run ios` | `expo start --ios` | iOS シミュレーターを起動 |
| `npm run android` | `expo start --android` | Android エミュレーターを起動 |
| `npm run web` | `expo start --web` | Web ターゲットを実行 |

- `i` キーで iOS シミュレーターを開きます（macOS + Xcode が必要）。
- `a` キーで Android エミュレーターを開きます（Android Studio と SDK が必要）。
- `w` キーでブラウザで Web ビルドを開きます。

### Web での実行

このプロジェクトでは一部に **React Native** 固有のライブラリ（例: `@aws-amplify/ui-react-native`）が含まれるため、Web 向けのバンドル時にエラーが発生した場合はインポートを条件付きで処理する必要があります。多くの場合、**web** はそのまま動作しますが、問題がある場合は以下のいずれかを検討してください。

- 純粋にネイティブ向けのインポートを削除または置換する。
- Web ビルドをスキップして、ネイティブプラットフォームで継続的に開発する。

## 設定ノート ⚙️

### 必須の生成ファイル: `src/aws-exports.js`

`app/_layout.js` は `../src/aws-exports` をインポートしますが、このファイルは Amplify が生成するため、このリポジトリにはコミットされていません。`amplify init` + `amplify push` を実行すると生成されます。

### Amplify バックエンド構成

`amplify/backend/backend-config.json` では、このプロジェクトは以下を含みます:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

追加のリポジトリ準拠認証情報:

- AppSync のデフォルト認証は現在 `API_KEY`、AWS IAM が追加プロバイダーとして設定されています。

### GraphQL データモデル

`amplify/backend/api/OnlyFansCloneApp/schema.graphql` で定義:

- `User` モデル（`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice` のプロフィール項目）
- `Post` モデル（`text`, 任意の `image`, `likes`, `userID` インデックス（`byUser`））

### Expo/Babel の設定

- `index.js` で async iterator polyfill と `expo-router/entry` を読み込みます。
- `babel.config.js` には次が含まれます:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## 使用例 🧪

### 投稿の作成と公開

1. アプリを開いてサインインします。
2. ホーム画面で `New post` をタップします。
3. 投稿テキストを入力します。
4. 必要に応じてライブラリから画像を選択します。
5. `Post` をタップして画像をアップロードし、`Post` レコードを保存します。

### ローカルバックエンドの運用（一般的）

```bash
amplify status
amplify pull
amplify push
```

スキーマやモデルを変更した場合は、環境に応じて Amplify CLI コマンドで必要な成果物を再生成してください。

## 開発メモ 🛠️

- ルーティングは、`app/` 配下の `expo-router` によるファイルベース方式。
- 現在のアプリは `DataStore` と直接 `API.graphql` mutation の併用。
- 認証 `signIn` 時、`_layout.js` は `Hub` でイベントを監視し、対応する `User` レコード作成を試行します。
- 現在の `package.json` には専用の `test` / `lint` スクリプトは定義されていません。
- `i18n/` ディレクトリは存在し、このドラフト時点では言語別 README は未追加。
- この README 上部の言語リンクは、単一のオプション行として意図的に保持されています。

## トラブルシューティング 🧯

### `Cannot find module '../src/aws-exports'`

実行:

```bash
amplify init
amplify push
```

`src/aws-exports.js` がローカルで生成されていることを確認してください。

### 認証は成功するがユーザーフィードが空

- `Hub` の sign-in リスナーが実行され、ユーザー作成 mutation が成功したか確認してください。
- AppSync の認証モードと権限を確認してください。
- DynamoDB/AppSync コンソールで `User` レコードのデータを確認してください。

### 新規投稿で画像アップロードが失敗する

- Amplify バックエンドに S3 ストレージリソースが存在することを確認してください。
- 認証済みユーザーがアップロード権限を持っていることを確認してください。
- ネットワーク接続を確認し、再認証後に再試行してください。

### ネイティブ専用インポートによる Web ビルドエラー

ネイティブ専用モジュールを条件付きでインポートするか、Web 互換性が壊れた場合は iOS/Android 中心で開発してください。

## ロードマップ / 次のステップ 🧭

- **AI Integration**: 自動コンテンツ生成、音楽コード分析、翻訳をサポートするために、エンドポイントまたはサードパーティ API 呼び出し（例: OpenAI）を追加します。
- **Monetization**: 収益化機能（例: Stripe）を入れる場合は、サブスクリプションや決済機能を組み込みます。
- **Deployment**: [EAS Build](https://docs.expo.dev/eas/) などを使って、iOS と Android 向けのスタンドアロンアプリを生成します。
- `i18n/` 配下で、上部の言語リンクを使って README セットを拡張します。

## 謝辞 🙌

- 元プロジェクト by [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app)。
- **OnlyIdeas** として改訂・リブランディングされ、人々がアイデアを共有し収益化できることを目的に、音楽・言語翻訳・共同研究向けの AI 機能の導入を計画しています。

元のコードベースと機能の詳細については、元リポジトリの README を確認してください。

## コントリビューション 🤝

コントリビューションは歓迎です。専用の `CONTRIBUTING.md` が追加されるまで、次の軽量なフローに従ってください。

1. リポジトリをフォークします。
2. フィーチャーブランチを作成します。
3. 変更はフォーカスを絞り、少なくとも 1 つのターゲットプラットフォームで検証します。
4. セットアップと再現手順を明記して PR を作成します。

Amplify リソースを変更する場合は、対応する `amplify/` の更新内容と移行ノートを PR 説明に含めてください。

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## License 📄

現在、このリポジトリには `LICENSE` ファイルが存在しません。

明示的なライセンスがメンテナーによって追加されるまで、デフォルトで all rights reserved とみなされます。

---

**OnlyIdeas** の開発をお楽しみください。AI アシストを活用し、ユーザーのアイデアを保護し価値に変換できるプラットフォームを作ってください。
