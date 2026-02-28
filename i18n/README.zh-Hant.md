[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)


# OnlyIdeas 全端應用程式

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

**OnlyIdeas** 是一個幫助人們分享並變現想法的全端應用。它整合了 **AWS Amplify**，用於使用者認證、資料儲存（AppSync + DynamoDB）與檔案託管（S3）。你可以透過 **Expo** 在 **iOS**、**Android** 與 **Web** 上執行本專案。

該專案受「OnlyFans 風格」功能啟發，也計畫整合 AI 工具，用於產生、分析與翻譯使用者提交的想法、音樂或媒體內容。

本 README 是基於現有 README 內容與目前原始碼檔案整理的、擴充版倉庫說明。

## 概覽 📌

### 技術棧一覽

| 領域 | 技術 |
|---|---|
| 應用框架 | `React Native` + `Expo` |
| 路由 | `expo-router` |
| 認證 + 資料 + 儲存 | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| 資料庫 | `Amazon DynamoDB`（透過 Amplify GraphQL 模型） |
| 檔案儲存 | `Amazon S3` |
| 目標平台 | iOS, Android, Web |

OnlyIdeas 使用了：

- `expo-router` 進行路由管理與以路由為基礎的畫面。
- `aws-amplify` + `@aws-amplify/ui-react-native` 處理認證、API、DataStore 與儲存。
- Amplify 後端能力：**Auth (Cognito)**、**API (AppSync GraphQL)** 與 **Storage (S3)**。

目前使用者流程：

1. 透過 Amplify Authenticator 登入。
2. 首頁動態牆顯示創作者（`User` 記錄）。
3. 開啟創作者個人頁並檢視貼文與付費牆狀態。
4. 建立新貼文，並可選擇上傳圖片到 S3。

## 功能 ✨

- 創作者清單與個人頁。
- 使用 Amplify UI Authenticator 登入 / 登出。
- 整合圖片選擇器的新貼文發布。
- S3 圖片上傳與圖片讀取。
- 以 GraphQL 為基礎的 `User` 與 `Post` 模型持久化。
- 單一 Expo 專案同時支援 iOS、Android 與 Web。

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

- 建議使用 Node.js 18+。
- npm（鎖定檔為 `package-lock.json`）。
- Expo 相容工具：
  - iOS 模擬器 + Xcode（用於本機 iOS 測試）。
  - Android Studio + SDK/模擬器（用於本機 Android 測試）。
- 用於配置 Amplify 的 AWS 帳號存取權限。
- 用於後端建立的 Amplify CLI。

## 安裝 🚀

### 1. 複製儲存庫

依你的工作流程選擇任一遠端位址：

| 指令 | 說明 |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | 歷史/封存參考 |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | 目前儲存庫（建議） |

接著開啟正確專案目錄：

```bash
cd onlyideas-react-native
```

此專案專為 **OnlyIdeas** 平台打造，聚焦於創意分享與變現。

### 2. 安裝相依套件

在專案根目錄執行：

```bash
npm install
```

此步驟會安裝必要的 Node 套件，包含 **Expo**、**React Native** 與 **aws-amplify**。

## 配置並初始化 AWS Amplify ☁️

1. **安裝 Amplify CLI**（若尚未安裝）：

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. 使用你的 AWS 憑證**配置 Amplify**：

   ```bash
   amplify configure
   ```

   - 登入 AWS 控制台，建立或使用既有 IAM 使用者。
   - 提供 `accessKeyId` 與 `secretAccessKey`。
   - 命名新的設定檔（例如：`onlyideas`）。

3. 在本專案中**初始化 Amplify**：

   ```bash
   amplify init
   ```

   建議回應：

   - 環境名稱：`dev`（或你偏好的名稱）
   - 預設編輯器：依你的選擇
   - 驗證方式：`AWS profile`
   - Profile：選擇剛剛建立的設定檔

4. **推送 Amplify 後端**：

   ```bash
   amplify push
   ```

此步驟會為 OnlyIdeas 建立 AWS 後端資源（Cognito、AppSync、S3 等）。

## 執行應用 ▶️

使用 **Expo** 在不同平台啟動應用：

```bash
npx expo start
```

或使用專案腳本：

| 腳本 | 指令 | 用途 |
|---|---|---|
| `npm start` | `expo start` | 啟動 Expo 開發伺服器 |
| `npm run ios` | `expo start --ios` | 開啟 iOS 模擬器 |
| `npm run android` | `expo start --android` | 開啟 Android 模擬器 |
| `npm run web` | `expo start --web` | 執行 web 目標 |

- 按 `i` 開啟 iOS 模擬器（需要 macOS + Xcode）。
- 按 `a` 開啟 Android 模擬器（需要 Android Studio 與 SDK）。
- 按 `w` 在瀏覽器開啟網頁版。

### 在 Web 上執行

由於本專案使用部份僅限 **React Native** 的套件（例如 `@aws-amplify/ui-react-native`），若你在 Web 打包時遇到錯誤，可能需要針對匯入進行條件式處理。多數情況下，**web** 可直接運作；若遇到問題可：

- 移除或替換純原生匯入，或
- 暫時跳過 web 建置，先使用原生平台。

## 設定說明 ⚙️

### 必要的產生檔：`src/aws-exports.js`

`app/_layout.js` 會 import `../src/aws-exports`，但該檔案由 Amplify 產生且未納入本儲存庫版本控制。執行 `amplify init` + `amplify push` 應會自動產生。

### Amplify 後端架構

在 `amplify/backend/backend-config.json` 中，本專案包含：

- `auth/OnlyFansCloneApp`（Cognito）
- `api/OnlyFansCloneApp`（AppSync GraphQL）
- `storage/s3onlyfanscloneappstorageb3e1fac4`（S3）

補充的倉庫層級授權資訊：

- AppSync 預設授權目前為 `API_KEY`，並以 AWS IAM 作為額外 provider。

### GraphQL 資料模型

定義於 `amplify/backend/api/OnlyFansCloneApp/schema.graphql`：

- `User` 模型欄位包含 `name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice`
- `Post` 模型包含 `text`、可選的 `image`、`likes` 以及 `userID` 索引（`byUser`）

### Expo/Babel 設定

- `index.js` 載入 async iterator polyfill 與 `expo-router/entry`。
- `babel.config.js` 包含：
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## 使用範例 🧪

### 建立並發布貼文

1. 開啟應用並登入。
2. 在首頁點選 `New post`。
3. 輸入貼文文字。
4. 可選：從圖庫選擇圖片。
5. 按下 `Post` 以上傳圖片並儲存 `Post` 記錄。

### 本機後端工作流程（常見）

```bash
amplify status
amplify pull
amplify push
```

如果你修改了 schema/models，請在本機環境用 Amplify CLI 指令重新產生對應產物。

## 開發說明 🛠️

- 透過 `expo-router` 在 `app/` 下使用檔案式路由。
- 目前應用混合了 `DataStore` 與直接的 `API.graphql` mutation 用法。
- 在使用者 `signIn` 時，`_layout.js` 會透過 `Hub` 監聽並嘗試建立對應的 `User` 記錄。
- 目前 `package.json` 未定義專門的 `test` 或 `lint` 腳本。
- `i18n/` 目錄已存在；README 多語言版本已規劃，這個草稿目前尚未完整補齊。
- 語言連結會固定保留在此 README 的頂端。

## 疑難排解 🧯

### `Cannot find module '../src/aws-exports'`

執行：

```bash
amplify init
amplify push
```

確認本機已生成 `src/aws-exports.js`。

### 驗證成功但首頁內容為空

- 確認 `Hub` 登入監聽有正常執行且使用者建立 mutation 成功。
- 檢查 AppSync 的授權模式與權限設定。
- 在 DynamoDB/AppSync 控制台確認 `User` 資料是否存在。

### 新增貼文時圖片上傳失敗

- 確認 Amplify 後端中存在 S3 儲存資源。
- 確認已登入使用者具備上傳權限。
- 檢查網路連線並重新認證後重試。

### Web 建置出現原生-only 匯入錯誤

請條件式匯入原生-only 模組，若 web 相容性持續不穩，請先集中在 iOS/Android 開發。

## 路線圖 / 後續規劃 🧭

- **AI 整合**：新增端點或第三方 API 呼叫（例如 OpenAI），支援自動內容生成、音樂和弦分析或翻譯。
- **變現功能**：加入訂閱或付費能力（例如 Stripe），以重建可收費內容模式。
- **部署**：使用 [EAS Build](https://docs.expo.dev/eas/) 或類似方案，產生獨立的 iOS 與 Android 應用。
- 依照本檔案頂端語言選項，持續補齊 `i18n/` 下的多語 README。

## 致謝 🙌

- 原始專案作者：[GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app)。
- 已重構並重新命名為 **OnlyIdeas**，著重幫助人們分享並變現想法，並規劃未來加入音樂、語言翻譯與研究協作的 AI 功能。

更多原始碼庫與功能細節，請查看原始儲存庫中的 README。

## 貢獻 🤝

歡迎提交貢獻。直到新增專屬的 `CONTRIBUTING.md` 前，請遵循以下輕量流程：

1. Fork 該儲存庫。
2. 建立 feature 分支。
3. 保持變更聚焦，並至少在一個目標平台上測試。
4. 在 PR 中提供清楚的安裝與重現步驟。

若你正在修改 Amplify 資源，請在 PR 說明中補充對應的 `amplify/` 更新與遷移備註。

## 授權 📄

目前倉庫中尚未包含 `LICENSE` 檔。

除非維護者補充明確授權，否則預設保留所有權利。

---

希望你在打造 **OnlyIdeas** 時一切順利，也歡迎依需求調整平台，運用 AI 幫助保護並變現使用者的創意。


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
