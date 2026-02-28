[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# OnlyIdeas 全栈应用

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20Android%20%7C%20Web-2ea44f)
![Expo](https://img.shields.io/badge/Expo-48-000020?logo=expo)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61dafb?logo=react)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-orange?logo=amazon-aws)
![Backend](https://img.shields.io/badge/Backend-AppSync%20%2B%20DynamoDB-ff9900)
![Storage](https://img.shields.io/badge/Storage-S3-569A31)
![Auth](https://img.shields.io/badge/Auth-Cognito-DD344C)
![License](https://img.shields.io/badge/License-Not%20Specified-lightgrey)

**OnlyIdeas** 是一个帮助人们分享并变现创意的全栈应用。它集成了 **AWS Amplify**，用于用户认证、数据存储（AppSync 与 DynamoDB）以及文件托管（S3）。你可以通过 **Expo** 在 **iOS**、**Android** 和 **Web** 上运行本项目。

受 “OnlyFans 风格” 功能启发，OnlyIdeas 也计划集成 AI 工具，用于生成、分析和翻译用户贡献的创意、音乐或媒体内容。

本 README 是基于现有 README 内容与当前源码整理出的扩展版、仓库准确草稿。

## 概览 📌

### 技术栈速览

| 区域 | 技术 |
|---|---|
| 应用框架 | `React Native` + `Expo` |
| 导航 | `expo-router` |
| 认证 + 数据 + 存储 | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| 数据库 | `Amazon DynamoDB`（通过 Amplify GraphQL 模型） |
| 文件存储 | `Amazon S3` |
| 目标平台 | iOS、Android、Web |

OnlyIdeas 使用：

- 使用 `expo-router` 进行导航与基于路由的页面组织。
- 使用 `aws-amplify` + `@aws-amplify/ui-react-native` 实现认证、API、DataStore 与存储。
- 使用 Amplify 后端分类资源：**Auth（Cognito）**、**API（AppSync GraphQL）**、**Storage（S3）**。

当前用户流程：

1. 通过 Amplify Authenticator 登录。
2. 首页信息流展示创作者（`User` 记录）。
3. 打开创作者主页并查看帖子/付费墙状态。
4. 创建新帖子，并可选择上传图片到 S3。

## 功能 ✨

- 创作者列表与个人主页页面。
- 通过 Amplify UI Authenticator 登录/退出。
- 集成图片选择器的新建帖子功能。
- S3 图片上传与图片读取。
- 基于 GraphQL 的 `User` 与 `Post` 模型持久化。
- 一个 Expo 项目覆盖 iOS、Android 与 Web 启动目标。

## 项目结构 🗂️

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

## 前置要求 ✅

- 建议使用 Node.js 18+。
- npm（锁文件为 `package-lock.json`）。
- 与 Expo 兼容的开发工具：
  - iOS Simulator + Xcode（用于 iOS 本地模拟）。
  - Android Studio + SDK/emulator（用于 Android 本地模拟）。
- 具备可用于 Amplify 资源创建的 AWS 账户权限。
- 用于后端初始化的 Amplify CLI。

## 安装 🚀

### 1. 克隆仓库

保留现有规范命令：

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

当前仓库中已配置、与仓库实际一致的远端地址：

```bash
git clone git@github.com:lachlanchen/onlyideas-react-native.git
cd onlyideas-react-native
```

该仓库专门面向 **OnlyIdeas** 平台，聚焦创意分享与变现。

### 2. 安装依赖

在项目根目录运行：

```bash
npm install
```

这会安装所需 Node 模块，包括 **Expo**、**React Native** 与 **aws-amplify**。

## 配置并初始化 AWS Amplify ☁️

1. **安装 Amplify CLI**（若尚未安装）：

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. 使用你的 AWS 凭证 **配置 Amplify**：

   ```bash
   amplify configure
   ```

   - 登录 AWS 控制台，创建或使用已有 IAM 用户。
   - 提供 `accessKeyId` 与 `secretAccessKey`。
   - 为新配置命名（例如 `onlyideas`）。

3. 在本项目中 **初始化 Amplify**：

   ```bash
   amplify init
   ```

   推荐交互选项：

   - Environment name: `dev`（或你的自定义名称）
   - Default editor: 自行选择
   - Authentication method: `AWS profile`
   - Profile: 选择你刚配置的 profile

4. **推送 Amplify 后端**：

   ```bash
   amplify push
   ```

这会为 OnlyIdeas 创建 AWS 后端资源（Cognito、AppSync、S3 等）。

## 运行应用 ▶️

使用 **Expo** 在不同平台启动应用：

```bash
npx expo start
```

或使用 package scripts：

| Script | Command | 作用 |
|---|---|---|
| `npm start` | `expo start` | 启动 Expo 开发服务器 |
| `npm run ios` | `expo start --ios` | 启动 iOS 模拟器 |
| `npm run android` | `expo start --android` | 启动 Android 模拟器 |
| `npm run web` | `expo start --web` | 运行 Web 目标 |

- 按 `i` 打开 iOS Simulator（需要 macOS + Xcode）。
- 按 `a` 打开 Android 模拟器（需要 Android Studio 与 SDK）。
- 按 `w` 在浏览器中打开 Web 版本。

### 在 Web 上运行

由于本项目使用了部分 **React Native** 专用库（例如 `@aws-amplify/ui-react-native`），如果你在 Web 打包时遇到错误，可能需要对相关导入进行条件处理。很多情况下 **web** 可以直接运行。若遇到问题，可选择：

- 移除或替换仅适用于原生平台的导入，或
- 跳过 Web 构建，继续使用原生平台开发。

## 配置说明 ⚙️

### 必需的生成文件：`src/aws-exports.js`

`app/_layout.js` 会导入 `../src/aws-exports`，但该文件由 Amplify 生成，未提交到此仓库。运行 `amplify init` + `amplify push` 后应会生成该文件。

### Amplify 后端结构

根据 `amplify/backend/backend-config.json`，本项目包含：

- `auth/OnlyFansCloneApp`（Cognito）
- `api/OnlyFansCloneApp`（AppSync GraphQL）
- `storage/s3onlyfanscloneappstorageb3e1fac4`（S3）

补充的仓库实际认证细节：

- AppSync 默认认证当前为 `API_KEY`，并额外启用了 AWS IAM 作为提供方。

### GraphQL 数据模型

定义于 `amplify/backend/api/OnlyFansCloneApp/schema.graphql`：

- `User` 模型包含个人资料字段（`name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice`）
- `Post` 模型包含 `text`、可选 `image`、`likes`，以及 `userID` 索引（`byUser`）

### Expo/Babel 设置

- `index.js` 加载异步迭代器 polyfill 与 `expo-router/entry`。
- `babel.config.js` 包含：
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## 使用示例 🧪

### 创建并发布帖子

1. 打开应用并登录。
2. 在首页点击 `New post`。
3. 输入帖子文本。
4. 可选：从相册选择一张图片。
5. 点击 `Post` 上传图片并保存 `Post` 记录。

### 本地后端工作流（常见）

```bash
amplify status
amplify pull
amplify push
```

如果你修改了 schema/models，请按你的环境需要使用 Amplify CLI 命令重新生成相关产物。

## 开发说明 🛠️

- 路由采用 `expo-router` 的文件路由方式，目录位于 `app/`。
- 当前应用同时混用了 `DataStore` 与直接 `API.graphql` mutation 调用。
- 在认证 `signIn` 后，`_layout.js` 会通过 `Hub` 监听并尝试创建对应的 `User` 记录。
- `package.json` 当前未定义专门的 `test` 或 `lint` 脚本。
- `i18n/` 目录已存在；在此草稿阶段，多语言 README 文件计划补充但尚未添加。
- 语言链接刻意保持为 README 顶部的一行选项。

## 故障排查 🧯

### `Cannot find module '../src/aws-exports'`

运行：

```bash
amplify init
amplify push
```

确保本地已生成 `src/aws-exports.js`。

### 认证成功但用户信息流为空

- 确认 `Hub` 的登录监听已执行，且创建用户的 mutation 成功。
- 检查 AppSync 的认证模式与权限配置。
- 在 DynamoDB/AppSync 控制台核验是否存在 `User` 记录。

### 新建帖子时图片上传失败

- 确认 Amplify 后端中存在 S3 存储资源。
- 验证已认证用户具备上传权限。
- 检查网络连接，并在重新认证后重试。

### Web 构建因仅原生导入报错

对仅原生模块做条件导入；如果 Web 兼容性中断，可优先专注 iOS/Android 开发。

## 路线图 / 下一步 🧭

- **AI Integration**：新增端点或第三方 API 调用（例如 OpenAI），以支持自动内容生成、音乐和弦分析或翻译。
- **Monetization**：如果希望复现变现能力，可加入订阅或支付能力（例如 Stripe）。
- **Deployment**：使用 [EAS Build](https://docs.expo.dev/eas/) 或类似方案生成 iOS 与 Android 独立应用。
- 依据本文件顶部的语言链接，在 `i18n/` 下扩展 README 多语言版本。

## 致谢 🙌

- 原始项目作者：[GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app)。
- 本项目已适配并重塑为 **OnlyIdeas**，重点是帮助用户分享并变现创意，并计划加入面向音乐、语言翻译与研究协作的 AI 功能。

如需了解原始代码库与功能细节，请查看原仓库中的 README。

## 贡献 🤝

欢迎贡献。正式 `CONTRIBUTING.md` 尚未添加前，请先遵循以下轻量流程：

1. Fork 仓库。
2. 创建功能分支。
3. 保持改动聚焦，并至少在一个目标平台测试。
4. 提交 Pull Request，并附上清晰的环境配置/复现说明。

如果你修改了 Amplify 资源，请在 PR 描述中包含对应的 `amplify/` 更新与迁移说明。

## 许可证 📄

当前仓库中尚不存在 `LICENSE` 文件。

假设：在维护者添加明确许可证之前，默认保留所有权利。

---

祝你构建 **OnlyIdeas** 顺利，也欢迎你在 AI 辅助下持续定制平台，更好地保护并变现用户创意。
