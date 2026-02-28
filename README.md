[English](README.md) · [العربية](i18n/README.ar.md) · [Español](i18n/README.es.md) · [Français](i18n/README.fr.md) · [日本語](i18n/README.ja.md) · [한국어](i18n/README.ko.md) · [Tiếng Việt](i18n/README.vi.md) · [中文 (简体)](i18n/README.zh-Hans.md) · [中文（繁體）](i18n/README.zh-Hant.md) · [Deutsch](i18n/README.de.md) · [Русский](i18n/README.ru.md)


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

**OnlyIdeas** is a full-stack application that helps people share and monetize their ideas. It integrates with **AWS Amplify** for user authentication, data storage (AppSync & DynamoDB), and file hosting (S3). You can run this project on **iOS**, **Android**, and **Web** via **Expo**.

Inspired by “OnlyFans-style” features, OnlyIdeas also aims to integrate AI tools for generating, analyzing, and translating user-contributed ideas, music, or media.

This README is an expanded, repository-accurate draft based on the existing README content and current source files.

## Overview 📌

### Stack at a glance

| Area | Technology |
|---|---|
| App framework | `React Native` + `Expo` |
| Navigation | `expo-router` |
| Auth + Data + Storage | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Database | `Amazon DynamoDB` (via Amplify GraphQL models) |
| File storage | `Amazon S3` |
| Targets | iOS, Android, Web |

OnlyIdeas uses:

- `expo-router` for navigation and route-based screens.
- `aws-amplify` + `@aws-amplify/ui-react-native` for auth, API, DataStore, and storage.
- Amplify backend categories for **Auth (Cognito)**, **API (AppSync GraphQL)**, and **Storage (S3)**.

Current user flow:

1. Sign in through Amplify Authenticator.
2. Home feed lists creators (`User` records).
3. Open a creator profile and view posts/paywall state.
4. Create a new post with optional image upload to S3.

## Features ✨

- Creator listing and profile pages.
- Sign in / sign out with Amplify UI Authenticator.
- New post creation with image picker integration.
- S3 image upload and image retrieval.
- GraphQL-backed `User` and `Post` model persistence.
- iOS, Android, and Web launch targets from one Expo project.

## Project Structure 🗂️

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

## Prerequisites ✅

- Node.js 18+ recommended.
- npm (lockfile is `package-lock.json`).
- Expo-compatible tooling:
  - iOS Simulator + Xcode (for iOS local simulation).
  - Android Studio + SDK/emulator (for Android local simulation).
- AWS account access for Amplify provisioning.
- Amplify CLI for backend setup.

## Installation 🚀

### 1. Clone the Repo

Use whichever remote your workflow prefers:

| Command | Notes |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | Historical/archival reference |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | Current repository (recommended) |

Then open the correct project directory:

```bash
cd onlyideas-react-native
```

This repository is tailored specifically for the **OnlyIdeas** platform, focusing on creativity and monetization.

### 2. Install Dependencies

From the project root, run:

```bash
npm install
```

This installs the necessary Node modules, including **Expo**, **React Native**, and **aws-amplify**.

## Configure & Initialize AWS Amplify ☁️

1. **Install Amplify CLI** (if you haven’t already):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Configure Amplify** with your AWS credentials:

   ```bash
   amplify configure
   ```

   - Sign in to the AWS console, create or use an existing IAM user.
   - Provide the `accessKeyId` and `secretAccessKey`.
   - Name the new profile (e.g., `onlyideas`).

3. **Initialize Amplify** in this project:

   ```bash
   amplify init
   ```

   Recommended prompts:

   - Environment name: `dev` (or your choice)
   - Default editor: your choice
   - Authentication method: `AWS profile`
   - Profile: select the one you just configured

4. **Push Amplify backend**:

   ```bash
   amplify push
   ```

This provisions the AWS backend (Cognito, AppSync, S3, etc.) for OnlyIdeas.

## Running the App ▶️

Use **Expo** to launch your app on different platforms:

```bash
npx expo start
```

Or via package scripts:

| Script | Command | Purpose |
|---|---|---|
| `npm start` | `expo start` | Start Expo dev server |
| `npm run ios` | `expo start --ios` | Launch iOS simulator |
| `npm run android` | `expo start --android` | Launch Android emulator |
| `npm run web` | `expo start --web` | Run web target |

- Press `i` to open the iOS Simulator (macOS + Xcode required).
- Press `a` to open an Android emulator (requires Android Studio & SDK).
- Press `w` to open the web build in your browser.

### Running on Web

Because this project uses some **React Native**-specific libraries (e.g., `@aws-amplify/ui-react-native`), you might need to conditionally handle those imports if you see an error while bundling for web. In many cases, **web** will work out of the box. If you encounter issues, either:

- Remove or replace imports that are purely native, or
- Skip the web build and continue using native platforms.

## Configuration Notes ⚙️

### Required generated file: `src/aws-exports.js`

`app/_layout.js` imports `../src/aws-exports`, but this file is generated by Amplify and is not committed in this repository. Running `amplify init` + `amplify push` should generate it.

### Amplify backend shape

From `amplify/backend/backend-config.json`, this project includes:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Additional repository-accurate auth detail:

- AppSync default authentication is currently `API_KEY` with AWS IAM as an additional provider.

### GraphQL data model

Defined in `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- `User` model with profile fields (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- `Post` model with `text`, optional `image`, `likes`, and `userID` index (`byUser`)

### Expo/Babel setup

- `index.js` loads async iterator polyfill and `expo-router/entry`.
- `babel.config.js` includes:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## Usage Examples 🧪

### Create and publish a post

1. Open app and sign in.
2. Tap `New post` on the home screen.
3. Enter post text.
4. Optionally select an image from library.
5. Tap `Post` to upload image and save `Post` record.

### Local backend workflow (typical)

```bash
amplify status
amplify pull
amplify push
```

If you modify schema/models, regenerate artifacts as needed with Amplify CLI commands in your environment.

## Development Notes 🛠️

- Routing is file-based via `expo-router` under `app/`.
- Current app mixes `DataStore` and direct `API.graphql` mutation usage.
- On auth `signIn`, `_layout.js` listens via `Hub` and attempts to create a matching `User` record.
- No dedicated `test` or `lint` scripts are currently defined in `package.json`.
- `i18n/` directory exists; language README files are planned but not yet added in this draft step.
- Language links are intentionally kept as a single options line at the top of this README.

## Troubleshooting 🧯

### `Cannot find module '../src/aws-exports'`

Run:

```bash
amplify init
amplify push
```

Ensure `src/aws-exports.js` is generated locally.

### Auth succeeds but user feed is empty

- Confirm `Hub` sign-in listener executed and user creation mutation succeeded.
- Check AppSync auth mode and permissions.
- Verify data in DynamoDB/AppSync console for `User` records.

### Image upload fails on new post

- Confirm S3 storage resource exists in Amplify backend.
- Verify authenticated user has permission to upload.
- Check network access and retry after re-auth.

### Web build errors with native-only imports

Conditionally import native-only modules, or focus on iOS/Android for development if web compatibility breaks.

## Roadmap / Next Steps 🧭

- **AI Integration**: Add endpoints or third-party API calls (e.g., OpenAI) to support automated content generation, music chord analysis, or translations.
- **Monetization**: Incorporate subscription or payment features (e.g., Stripe) if you want to replicate monetized features.
- **Deployment**: Use [EAS Build](https://docs.expo.dev/eas/) or similar to generate standalone apps for iOS & Android.
- Expand i18n README set under `i18n/` using the language links at the top of this file.

## Acknowledgments 🙌

- Original project by [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Adapted and rebranded as **OnlyIdeas**, focusing on helping people share and monetize their ideas, with planned AI features for music, language translation, and research collaboration.

For additional details on the original codebase and features, check the README in the original repository.

## Contributing 🤝

Contributions are welcome. Until a dedicated `CONTRIBUTING.md` is added, please follow this lightweight flow:

1. Fork the repo.
2. Create a feature branch.
3. Keep changes focused and test on at least one target platform.
4. Open a pull request with clear setup/reproduction notes.

If you are changing Amplify resources, include the corresponding `amplify/` updates and migration notes in the PR description.

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## License 📄

No `LICENSE` file is currently present in this repository.

Assumption: all rights are reserved by default unless/until an explicit license is added by the maintainers.

---

Enjoy building **OnlyIdeas**, and feel free to tailor the platform to protect and profit from user ideas with AI assistance.
