[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# OnlyIdeas 全端應用程式

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20Android%20%7C%20Web-2ea44f)
![Expo](https://img.shields.io/badge/Expo-48-000020?logo=expo)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61dafb?logo=react)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-orange?logo=amazon-aws)
![Backend](https://img.shields.io/badge/Backend-AppSync%20%2B%20DynamoDB-ff9900)
![Storage](https://img.shields.io/badge/Storage-S3-569A31)
![Auth](https://img.shields.io/badge/Auth-Cognito-DD344C)
![License](https://img.shields.io/badge/License-Not%20Specified-lightgrey)

**OnlyIdeas** 是一個協助人們分享並將想法變現的全端應用程式。它整合 **AWS Amplify** 以處理使用者驗證、資料儲存（AppSync 與 DynamoDB）以及檔案託管（S3）。你可以透過 **Expo** 在 **iOS**、**Android** 與 **Web** 上執行此專案。

受到「OnlyFans 風格」功能啟發，OnlyIdeas 也計畫整合 AI 工具，用於產生、分析與翻譯使用者投稿的想法、音樂或媒體內容。

本 README 是根據既有 README 內容與目前原始檔建立的擴充版、且與儲存庫現況一致的草稿。

## 總覽 📌

### 技術棧速覽

| 區塊 | 技術 |
|---|---|
| App 框架 | `React Native` + `Expo` |
| 導航 | `expo-router` |
| Auth + Data + Storage | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| 資料庫 | `Amazon DynamoDB`（透過 Amplify GraphQL 模型） |
| 檔案儲存 | `Amazon S3` |
| 目標平台 | iOS、Android、Web |

OnlyIdeas 使用：

- 以 `expo-router` 進行導航與路由式畫面管理。
- 以 `aws-amplify` + `@aws-amplify/ui-react-native` 處理 auth、API、DataStore 與 storage。
- 使用 Amplify 後端分類來提供 **Auth (Cognito)**、**API (AppSync GraphQL)** 與 **Storage (S3)**。

目前使用者流程：

1. 透過 Amplify Authenticator 登入。
2. 首頁動態牆列出創作者（`User` 紀錄）。
3. 開啟創作者個人頁並查看貼文與付費牆狀態。
4. 建立新貼文，並可選擇上傳圖片至 S3。

## 功能 ✨

- 創作者列表與個人檔案頁面。
- 使用 Amplify UI Authenticator 進行登入／登出。
- 新貼文建立，整合圖片選取器。
- S3 圖片上傳與圖片讀取。
- 以 GraphQL 為基礎的 `User` 與 `Post` 模型持久化。
- 單一 Expo 專案同時支援 iOS、Android 與 Web 啟動目標。

## 專案結構 🗂️

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

## 先決條件 ✅

- 建議 Node.js 18+。
- npm（lockfile 為 `package-lock.json`）。
- 與 Expo 相容的工具鏈：
  - iOS Simulator + Xcode（用於 iOS 本機模擬）。
  - Android Studio + SDK/emulator（用於 Android 本機模擬）。
- 具備可供 Amplify 佈建的 AWS 帳號存取權。
- 用於後端設定的 Amplify CLI。

## 安裝 🚀

### 1. Clone 儲存庫

保留既有標準指令：

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

此儲存庫目前設定且與實際狀態一致的遠端：

```bash
git clone git@github.com:lachlanchen/onlyideas-react-native.git
cd onlyideas-react-native
```

這個儲存庫專為 **OnlyIdeas** 平台打造，重點放在創意與變現。

### 2. 安裝相依套件

在專案根目錄執行：

```bash
npm install
```

這會安裝必要的 Node 模組，包含 **Expo**、**React Native** 與 **aws-amplify**。

## 設定與初始化 AWS Amplify ☁️

1. **安裝 Amplify CLI**（若尚未安裝）：

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. 使用你的 AWS 憑證**設定 Amplify**：

   ```bash
   amplify configure
   ```

   - 登入 AWS 主控台，建立或使用既有 IAM 使用者。
   - 提供 `accessKeyId` 與 `secretAccessKey`。
   - 命名新 profile（例如 `onlyideas`）。

3. 在此專案中**初始化 Amplify**：

   ```bash
   amplify init
   ```

   建議提示選項：

   - Environment name: `dev`（或自訂）
   - Default editor: 自行選擇
   - Authentication method: `AWS profile`
   - Profile: 選擇你剛設定的 profile

4. **推送 Amplify 後端**：

   ```bash
   amplify push
   ```

這會為 OnlyIdeas 佈建 AWS 後端（Cognito、AppSync、S3 等）。

## 執行應用程式 ▶️

使用 **Expo** 在不同平台啟動你的 app：

```bash
npx expo start
```

或透過 package scripts：

| Script | Command | 用途 |
|---|---|---|
| `npm start` | `expo start` | 啟動 Expo 開發伺服器 |
| `npm run ios` | `expo start --ios` | 啟動 iOS 模擬器 |
| `npm run android` | `expo start --android` | 啟動 Android 模擬器 |
| `npm run web` | `expo start --web` | 執行 Web 目標 |

- 按 `i` 開啟 iOS Simulator（需要 macOS + Xcode）。
- 按 `a` 開啟 Android 模擬器（需要 Android Studio 與 SDK）。
- 按 `w` 在瀏覽器中開啟 web 版本。

### 在 Web 上執行

由於此專案使用了部分 **React Native** 專用函式庫（例如 `@aws-amplify/ui-react-native`），若你在 web 打包時遇到錯誤，可能需要條件式處理這些 import。在很多情況下，**web** 可直接運作。若發生問題，可以：

- 移除或替換純原生（native-only）的 imports，或
- 跳過 web build，改在原生平台繼續開發。

## 設定備註 ⚙️

### 必要產生檔案：`src/aws-exports.js`

`app/_layout.js` 會 import `../src/aws-exports`，但這個檔案由 Amplify 產生，未提交至此儲存庫。執行 `amplify init` + `amplify push` 後應會產生。

### Amplify 後端形狀

根據 `amplify/backend/backend-config.json`，此專案包含：

- `auth/OnlyFansCloneApp`（Cognito）
- `api/OnlyFansCloneApp`（AppSync GraphQL）
- `storage/s3onlyfanscloneappstorageb3e1fac4`（S3）

額外、且與儲存庫現況一致的 auth 細節：

- AppSync 預設驗證目前為 `API_KEY`，並以 AWS IAM 作為額外 provider。

### GraphQL 資料模型

定義於 `amplify/backend/api/OnlyFansCloneApp/schema.graphql`：

- `User` 模型，含個人資料欄位（`name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice`）
- `Post` 模型，含 `text`、可選 `image`、`likes`，以及 `userID` 索引（`byUser`）

### Expo/Babel 設定

- `index.js` 載入 async iterator polyfill 與 `expo-router/entry`。
- `babel.config.js` 包含：
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## 使用範例 🧪

### 建立並發佈貼文

1. 開啟 app 並登入。
2. 在首頁點選 `New post`。
3. 輸入貼文文字。
4. 可選擇從相簿挑選圖片。
5. 點選 `Post` 以上傳圖片並儲存 `Post` 紀錄。

### 本機後端工作流程（常見）

```bash
amplify status
amplify pull
amplify push
```

若你修改了 schema/models，請在你的環境中視需要使用 Amplify CLI 指令重新產生相關產物。

## 開發備註 🛠️

- 路由採用 `expo-router`，以 `app/` 下檔案為基礎。
- 目前 app 同時使用 `DataStore` 與直接 `API.graphql` mutation 的方式。
- 在 auth `signIn` 後，`_layout.js` 會透過 `Hub` 監聽並嘗試建立對應的 `User` 紀錄。
- `package.json` 目前未定義專用 `test` 或 `lint` scripts。
- `i18n/` 目錄已存在；此草稿步驟中規劃新增語言版 README 檔。
- README 頂端的語言連結刻意維持為單一選項列。

## 疑難排解 🧯

### `Cannot find module '../src/aws-exports'`

執行：

```bash
amplify init
amplify push
```

確認本機已產生 `src/aws-exports.js`。

### 驗證成功但使用者動態牆為空

- 確認 `Hub` 的 sign-in 監聽器有執行，且使用者建立 mutation 成功。
- 檢查 AppSync auth mode 與權限。
- 在 DynamoDB/AppSync 主控台確認是否有 `User` 紀錄。

### 新貼文圖片上傳失敗

- 確認 Amplify 後端存在 S3 storage 資源。
- 確認已驗證使用者具備上傳權限。
- 檢查網路連線，重新驗證後再試一次。

### Web build 因 native-only imports 報錯

請對 native-only modules 做條件式匯入，或在 web 相容性中斷時先以 iOS/Android 作為主要開發目標。

## 路線圖 / 下一步 🧭

- **AI 整合**：新增端點或第三方 API 呼叫（例如 OpenAI），支援自動內容生成、音樂和弦分析或翻譯。
- **變現機制**：若你希望重現可變現功能，可整合訂閱或付款能力（例如 Stripe）。
- **部署**：使用 [EAS Build](https://docs.expo.dev/eas/) 或類似方案產生 iOS 與 Android 的獨立 App。
- 依據本檔頂端語言連結，在 `i18n/` 下擴充 README 語言版本。

## 致謝 🙌

- 原始專案由 [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app) 建立。
- 已調整並重新品牌化為 **OnlyIdeas**，專注於協助人們分享並將想法變現，並規劃 AI 功能以支援音樂、語言翻譯與研究協作。

如需原始程式碼與功能的更多細節，請查看原始儲存庫中的 README。

## 貢獻 🤝

歡迎貢獻。在新增專用 `CONTRIBUTING.md` 前，請先遵循以下輕量流程：

1. Fork 此儲存庫。
2. 建立功能分支。
3. 讓變更聚焦，並至少在一個目標平台上測試。
4. 開啟 pull request，並附上清楚的設定／重現說明。

若你有修改 Amplify 資源，請在 PR 說明中附上對應的 `amplify/` 更新與遷移備註。

## 授權 📄

此儲存庫目前不存在 `LICENSE` 檔案。

推定：除非／直到維護者新增明確授權，否則預設為保留所有權利。

---

祝你打造 **OnlyIdeas** 順利，並可自由調整平台，以 AI 協作保護並放大使用者想法的價值。
