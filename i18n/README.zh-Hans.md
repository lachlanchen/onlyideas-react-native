[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)


# OnlyIdeas 全栈应用

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

**OnlyIdeas** 是一个帮助人们分享并变现想法的全栈应用。它集成了 **AWS Amplify** 用于用户认证、数据存储（AppSync + DynamoDB）和文件托管（S3）。你可以通过 **Expo** 在 **iOS**、**Android** 和 **Web** 上运行该项目。

该项目受 “OnlyFans 风格” 的功能启发，也计划集成 AI 工具，用于生成、分析和翻译用户提交的想法、音乐或媒体内容。

本 README 是基于现有 README 内容和当前源码文件整理而成的、扩展版仓库级说明。

## 概览 📌

### 一览技术栈

| 区域 | 技术 |
|---|---|
| 应用框架 | `React Native` + `Expo` |
| 路由 | `expo-router` |
| 认证 + 数据 + 存储 | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| 数据库 | `Amazon DynamoDB`（通过 Amplify GraphQL 模型） |
| 文件存储 | `Amazon S3` |
| 目标平台 | iOS, Android, Web |

OnlyIdeas 使用了：

- `expo-router` 进行路由管理和基于路由的页面。
- `aws-amplify` + `@aws-amplify/ui-react-native` 处理认证、API、DataStore 和存储。
- Amplify 后端能力：**Auth (Cognito)**、**API (AppSync GraphQL)** 与 **Storage (S3)**。

当前用户流程：

1. 通过 Amplify Authenticator 登录。
2. 首页动态流显示创作者列表（`User` 记录）。
3. 打开创作者主页，查看内容与付费墙状态。
4. 创建新帖子，可选上传图片到 S3。

## 功能 ✨

- 创作者列表与个人主页。
- 使用 Amplify UI Authenticator 登录/登出。
- 集成图片选择器的新帖发布。
- S3 图片上传与图片读取。
- 基于 GraphQL 的 `User` 和 `Post` 模型持久化。
- 单一 Expo 项目同时支持 iOS、Android 与 Web。

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

## 先决条件 ✅

- 建议使用 Node.js 18+。
- npm（锁文件为 `package-lock.json`）。
- Expo 兼容工具：
  - iOS 模拟器 + Xcode（用于本地 iOS 调试）。
  - Android Studio + SDK/模拟器（用于本地 Android 调试）。
- 用于配置 Amplify 的 AWS 账号访问权限。
- 用于后端搭建的 Amplify CLI。

## 安装 🚀

### 1. 克隆仓库

按你的工作流选择任一远端方式：

| 命令 | 说明 |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | 历史/归档参考 |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | 当前仓库（推荐） |

然后进入项目目录：

```bash
cd onlyideas-react-native
```

该仓库专门面向 **OnlyIdeas** 平台，聚焦于创意分享与变现。

### 2. 安装依赖

在项目根目录执行：

```bash
npm install
```

该命令会安装必要的 Node 模块，包括 **Expo**、**React Native** 和 **aws-amplify**。

## 配置并初始化 AWS Amplify ☁️

1. **安装 Amplify CLI**（如果尚未安装）：

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. 使用你的 AWS 凭据**配置 Amplify**：

   ```bash
   amplify configure
   ```

   - 登录 AWS 控制台，创建或使用现有 IAM 用户。
   - 提供 `accessKeyId` 与 `secretAccessKey`。
   - 命名新配置文件（例如：`onlyideas`）。

3. 在该项目中**初始化 Amplify**：

   ```bash
   amplify init
   ```

   推荐参数：

   - 环境名称：`dev`（或你自己的名称）
   - 默认编辑器：按你偏好选择
   - 身份验证方式：`AWS profile`
   - 配置文件：选择刚刚配置好的 profile

4. **推送 Amplify 后端**：

   ```bash
   amplify push
   ```

此步骤会为 OnlyIdeas 创建 AWS 后端资源（Cognito、AppSync、S3 等）。

## 运行应用 ▶️

通过 **Expo** 在不同平台启动应用：

```bash
npx expo start
```

或使用以下脚本：

| 脚本 | 命令 | 用途 |
|---|---|---|
| `npm start` | `expo start` | 启动 Expo 开发服务器 |
| `npm run ios` | `expo start --ios` | 打开 iOS 模拟器 |
| `npm run android` | `expo start --android` | 打开 Android 模拟器 |
| `npm run web` | `expo start --web` | 运行 Web 目标 |

- 按 `i` 打开 iOS 模拟器（需要 macOS + Xcode）。
- 按 `a` 打开 Android 模拟器（需要 Android Studio 与 SDK）。
- 按 `w` 在浏览器中打开 Web 版本。

### 在 Web 上运行

由于本项目使用了部分只适用于 **React Native** 的库（如 `@aws-amplify/ui-react-native`），如果 Web 打包时出现错误，你可能需要按需处理对应导入。多数情况下，**Web** 可直接运行；若遇到问题，请：

- 移除或替换纯原生导入；
- 或跳过 Web 构建，先继续使用原生平台。

## 配置说明 ⚙️

### 必需的生成文件：`src/aws-exports.js`

`app/_layout.js` 会引用 `../src/aws-exports`，但该文件由 Amplify 生成且未纳入仓库提交。执行 `amplify init` + `amplify push` 后会生成它。

### Amplify 后端结构

在 `amplify/backend/backend-config.json` 中，本项目包含：

- `auth/OnlyFansCloneApp`（Cognito）
- `api/OnlyFansCloneApp`（AppSync GraphQL）
- `storage/s3onlyfanscloneappstorageb3e1fac4`（S3）

补充的仓库级鉴权信息：

- AppSync 默认鉴权目前是 `API_KEY`，并额外支持 AWS IAM。

### GraphQL 数据模型

在 `amplify/backend/api/OnlyFansCloneApp/schema.graphql` 中定义：

- `User` 模型的字段包括 `name`、`handle`、`bio`、`avatar`、`coverImage`、`subscriptionPrice`
- `Post` 模型的字段包括 `text`、可选的 `image`、`likes` 与 `userID` 索引（`byUser`）

### Expo/Babel 配置

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
4. 可选：从图库选择图片。
5. 点击 `Post` 上传图片并保存 `Post` 记录。

### 本地后端工作流（常见）

```bash
amplify status
amplify pull
amplify push
```

如修改了 schema/models，请按你的环境使用 Amplify CLI 命令重新生成相关产物。

## 开发说明 🛠️

- 通过 `expo-router` 在 `app/` 下进行文件化路由。
- 当前应用混合了 `DataStore` 与直接 `API.graphql` 的 mutation 用法。
- 在用户 `signIn` 时，`_layout.js` 通过 `Hub` 监听并尝试创建匹配的 `User` 记录。
- 当前 `package.json` 中未定义专门的 `test` 或 `lint` 脚本。
- `i18n/` 目录已存在；本仓库计划添加多语言 README 文件（在当前草稿中尚未完全收录）。
- README 顶部会固定保留一行语言选项。

## 故障排查 🧯

### `Cannot find module '../src/aws-exports'`

执行：

```bash
amplify init
amplify push
```

确保本地已生成 `src/aws-exports.js`。

### 认证成功但首页内容为空

- 确认 `Hub` 登录监听已执行且用户创建 mutation 成功。
- 检查 AppSync 鉴权模式与权限配置。
- 在 DynamoDB/AppSync 控制台确认 `User` 数据是否存在。

### 新建帖子时图片上传失败

- 确认 Amplify 后端中存在 S3 存储资源。
- 确认已登录用户拥有上传权限。
- 检查网络访问后重试。

### Web 打包出现原生导入报错

可按条件导入仅原生模块，或者在兼容性不稳定时先专注于 iOS/Android 开发。

## 路线图 / 后续计划 🧭

- **AI 集成**：新增端点或第三方 API 调用（例如 OpenAI），支持自动内容生成、音乐和弦分析或翻译。
- **变现功能**：增加订阅或支付能力（如 Stripe），以复刻带有付费能力的内容模式。
- **部署**：使用 [EAS Build](https://docs.expo.dev/eas/) 或同类方案，生成独立的 iOS 与 Android 应用。
- 在 `i18n/` 下按本文件顶部语言选项继续补充多语言 README。

## 致谢 🙌

- 原始项目作者：[GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app)。
- 已改编并重命名为 **OnlyIdeas**，聚焦于帮助人们分享并变现想法，并规划了面向音乐、语言翻译与研究协作的 AI 功能。

查看原始仓库的 README 可获取更多代码库与功能细节。

## 参与贡献 🤝

欢迎贡献。直到补充完整的 `CONTRIBUTING.md` 前，请按以下轻量流程：

1. Fork 该仓库。
2. 创建 feature 分支。
3. 保持改动聚焦，并至少在一个目标平台上验证。
4. 在 PR 中提供清晰的环境与复现说明。

如果你在修改 Amplify 资源，请在 PR 描述中补充对应的 `amplify/` 更新与迁移说明。

## 许可证 📄

当前仓库暂未包含 `LICENSE` 文件。

除非维护者补充明确许可证，否则默认保留所有权利。

---

希望你在构建 **OnlyIdeas** 时玩得愉快，也欢迎根据需求定制该平台，结合 AI 助力保护并盈利你的用户创意。


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
