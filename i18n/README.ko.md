[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# OnlyIdeas 풀스택 앱

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

**OnlyIdeas**는 사람들이 자신의 아이디어를 공유하고 수익화할 수 있도록 도와주는 풀스택 애플리케이션입니다. 사용자 인증, 데이터 저장(AppSync 및 DynamoDB), 파일 호스팅(S3)을 위해 **AWS Amplify**와 연동되며, **Expo**를 통해 **iOS**, **Android**, **Web**에서 실행할 수 있습니다.

“OnlyFans 스타일” 기능에서 영감을 받아, OnlyIdeas는 또한 사용자가 기여한 아이디어, 음악, 미디어를 생성·분석·번역하는 AI 도구 통합도 목표로 하고 있습니다.

이 README는 기존 README 내용과 현재 소스 파일을 기반으로 확장한, 저장소 기준의 초안입니다.

## 개요 📌

### 한눈에 보는 스택

| 영역 | 기술 |
|---|---|
| 앱 프레임워크 | `React Native` + `Expo` |
| 내비게이션 | `expo-router` |
| 인증 + 데이터 + 저장소 | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| 데이터베이스 | `Amazon DynamoDB` (Amplify GraphQL 모델 경유) |
| 파일 저장소 | `Amazon S3` |
| 대상 플랫폼 | iOS, Android, Web |

OnlyIdeas는 다음을 사용합니다:

- 내비게이션과 라우트 기반 화면에 `expo-router` 사용
- 인증, API, DataStore, 저장소에 `aws-amplify` + `@aws-amplify/ui-react-native` 사용
- Amplify 백엔드 카테고리: **Auth (Cognito)**, **API (AppSync GraphQL)**, **Storage (S3)**

현재 사용자 흐름:

1. Amplify Authenticator를 통해 로그인합니다.
2. 홈 피드에 크리에이터 목록(`User` 레코드)이 표시됩니다.
3. 크리에이터 프로필을 열어 게시물/페이월 상태를 확인합니다.
4. 새 게시물을 작성하고, 필요 시 S3에 이미지를 업로드합니다.

## 기능 ✨

- 크리에이터 목록 및 프로필 페이지.
- Amplify UI Authenticator를 통한 로그인/로그아웃.
- 이미지 선택기 통합으로 새 게시물 작성.
- S3 이미지 업로드 및 이미지 조회.
- GraphQL 기반 `User`, `Post` 모델 영속성.
- 하나의 Expo 프로젝트로 iOS, Android, Web 실행 대상 지원.

## 프로젝트 구조 🗂️

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
├── i18n/                    # 번역 README 폴더(현재 비어 있음)
├── app.json
├── babel.config.js
├── index.js
└── package.json
```

## 사전 요구사항 ✅

- Node.js 18+ 권장.
- npm(`package-lock.json` lockfile 사용).
- Expo 호환 도구:
  - iOS Simulator + Xcode (iOS 로컬 시뮬레이션)
  - Android Studio + SDK/에뮬레이터 (Android 로컬 시뮬레이션)
- Amplify 프로비저닝을 위한 AWS 계정 접근.
- 백엔드 설정을 위한 Amplify CLI.

## 설치 🚀

### 1. 저장소 클론

작업 방식에 맞는 원격 저장소를 선택하세요:

| 명령 | 비고 |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | 과거/아카이브 참조 |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | 현재 저장소(권장) |

그다음 해당 프로젝트 디렉터리를 여십시오:

```bash
cd onlyideas-react-native
```

이 저장소는 창의성과 수익화에 초점을 둔 **OnlyIdeas** 플랫폼 전용으로 구성되어 있습니다.

### 2. 의존성 설치

프로젝트 루트에서 실행하세요:

```bash
npm install
```

필요한 Node 모듈(예: **Expo**, **React Native**, **aws-amplify**)이 설치됩니다.

## AWS Amplify 구성 및 초기화 ☁️

1. **Amplify CLI 설치** (아직 설치하지 않은 경우):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. AWS 자격 증명으로 **Amplify 구성**:

   ```bash
   amplify configure
   ```

   - AWS 콘솔에 로그인하고 기존 IAM 사용자 사용 또는 새 사용자 생성
   - `accessKeyId` 및 `secretAccessKey` 입력
   - 새 프로필 이름 지정(예: `onlyideas`)

3. 이 프로젝트에서 **Amplify 초기화**:

   ```bash
   amplify init
   ```

   권장 값:

   - 환경 이름: `dev`(또는 원하는 값)
   - 기본 편집기: 사용자 선택
   - 인증 방식: `AWS profile`
   - 프로필: 방금 만든 항목 선택

4. **Amplify 백엔드 배포**:

   ```bash
   amplify push
   ```

이 단계로 OnlyIdeas용 AWS 백엔드(Cognito, AppSync, S3 등)가 프로비저닝됩니다.

## 앱 실행 ▶️

**Expo**로 서로 다른 플랫폼에서 앱을 실행합니다:

```bash
npx expo start
```

또는 package script를 사용합니다:

| 스크립트 | 명령 | 용도 |
|---|---|---|
| `npm start` | `expo start` | Expo 개발 서버 시작 |
| `npm run ios` | `expo start --ios` | iOS 시뮬레이터 실행 |
| `npm run android` | `expo start --android` | Android 에뮬레이터 실행 |
| `npm run web` | `expo start --web` | Web 대상 실행 |

- `i`를 눌러 iOS Simulator 열기 (macOS + Xcode 필요).
- `a`를 눌러 Android 에뮬레이터 열기 (Android Studio 및 SDK 필요).
- `w`를 눌러 웹 빌드를 브라우저에서 열기.

### 웹에서 실행

이 프로젝트에는 일부 **React Native** 전용 라이브러리(`@aws-amplify/ui-react-native` 등)가 있으므로, 웹 번들링 시 오류가 발생하면 해당 import를 조건부로 처리해야 할 수 있습니다. 대부분의 경우 **web**은 바로 동작합니다. 문제가 생기면 다음 중 하나를 시도하세요.

- 네이티브 전용 import를 제거하거나 교체
- 웹 빌드를 건너뛰고 네이티브 플랫폼으로 개발 계속

## 구성 노트 ⚙️

### 필수 생성 파일: `src/aws-exports.js`

`app/_layout.js`에서 `../src/aws-exports`를 import합니다. 이 파일은 Amplify가 생성하므로 저장소에 커밋되어 있지 않습니다. `amplify init` + `amplify push` 실행 시 생성됩니다.

### Amplify 백엔드 구성

`amplify/backend/backend-config.json`에서 이 프로젝트는 다음을 포함합니다:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

추가 저장소 기준 인증 세부 정보:

- AppSync 기본 인증은 현재 `API_KEY`, 보조 프로바이더는 AWS IAM입니다.

### GraphQL 데이터 모델

`amplify/backend/api/OnlyFansCloneApp/schema.graphql`에 정의됨:

- 프로필 필드(`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)가 있는 `User` 모델
- `text`, 선택적 `image`, `likes`, `userID` 인덱스(`byUser`)가 있는 `Post` 모델

### Expo/Babel 설정

- `index.js`는 async iterator polyfill과 `expo-router/entry`를 로드합니다.
- `babel.config.js`에는 다음이 포함됩니다:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## 사용 예시 🧪

### 게시물 생성 및 게시

1. 앱을 열고 로그인합니다.
2. 홈 화면에서 `New post`를 탭합니다.
3. 게시물 텍스트를 입력합니다.
4. 필요하면 라이브러리에서 이미지를 선택합니다.
5. `Post`를 눌러 이미지를 업로드하고 `Post` 레코드를 저장합니다.

### 로컬 백엔드 작업 흐름(일반적)

```bash
amplify status
amplify pull
amplify push
```

스키마/모델을 수정할 경우 환경에 맞춰 Amplify CLI 명령으로 산출물을 다시 생성하세요.

## 개발 노트 🛠️

- 라우팅은 `app/` 아래 `expo-router` 기반의 파일 라우팅입니다.
- 현재 앱은 `DataStore`와 직접 `API.graphql` mutation 사용을 병행합니다.
- 인증 `signIn` 시 `_layout.js`가 `Hub`를 통해 리스너를 기다리며, 대응하는 `User` 레코드 생성을 시도합니다.
- 현재 `package.json`에는 전용 `test` 또는 `lint` 스크립트가 정의되어 있지 않습니다.
- `i18n/` 디렉터리가 존재하며, 해당 언어 README 파일은 이 초안 단계에서 아직 추가되지 않았습니다.
- 언어 링크는 이 README 상단에 단일 옵션 라인으로 의도적으로 유지되어 있습니다.

## 문제 해결 🧯

### `Cannot find module '../src/aws-exports'`

다음 명령을 실행하세요:

```bash
amplify init
amplify push
```

로컬에서 `src/aws-exports.js`가 생성되었는지 확인합니다.

### 인증은 성공했지만 사용자 피드가 비어 있음

- `Hub`의 sign-in listener가 실행되고 사용자 생성 mutation이 성공했는지 확인하세요.
- AppSync 인증 모드와 권한을 확인하세요.
- DynamoDB/AppSync 콘솔에서 `User` 레코드 데이터를 점검하세요.

### 새 게시물에서 이미지 업로드 실패

- Amplify 백엔드에 S3 저장소 리소스가 있는지 확인합니다.
- 인증된 사용자가 업로드 권한을 가지고 있는지 확인합니다.
- 네트워크 상태를 확인한 뒤 재인증하고 다시 시도하세요.

### 네이티브 전용 import로 인한 웹 빌드 오류

네이티브 전용 모듈을 조건부로 import하거나, 웹 호환성이 깨지면 iOS/Android 중심으로 개발하세요.

## 로드맵 / 다음 단계 🧭

- **AI 통합**: 자동 콘텐츠 생성, 음악 코드 분석, 번역을 지원하는 OpenAI 같은 엔드포인트/서드파티 API 호출 추가
- **수익화**: 유료형 기능(예: Stripe)을 적용해 구독/결제 기능을 통합
- **배포**: [EAS Build](https://docs.expo.dev/eas/) 또는 유사 툴로 iOS/Android 독립 실행형 앱 생성
- `i18n/` 내 언어 링크를 활용해 언어 README 세트 확장

## 감사 🙌

- 원본 프로젝트: [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- 사람들의 아이디어 공유와 수익화를 지원하고, 음악·번역·연구 협업을 위한 AI 기능을 추가할 수 있도록 **OnlyIdeas**로 전환/리브랜딩되었습니다.

원본 코드베이스와 기능에 대한 추가 정보는 원본 저장소의 README를 확인하세요.

## 기여 🤝

기여를 환영합니다. 전용 `CONTRIBUTING.md`가 추가되기 전에는 아래 가벼운 흐름을 따라주세요:

1. 저장소를 fork합니다.
2. feature 브랜치를 만듭니다.
3. 변경 범위를 집중적으로 유지하고 최소 한 개 타깃 플랫폼에서 테스트합니다.
4. 설정/재현 절차를 명확히 적은 풀 리퀘스트를 열어주세요.

Amplify 리소스를 변경할 경우, 해당 `amplify/` 변경 내용과 마이그레이션 메모를 PR 설명에 포함하세요.

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## License 📄

현재 이 저장소에는 `LICENSE` 파일이 없습니다.

명시적 라이선스가 유지관리자에 의해 추가될 때까지 기본적으로 모든 권리(all rights reserved)가 보유된 것으로 간주됩니다.

---

**OnlyIdeas** 개발을 즐겨 보세요. AI 지원을 활용해 사용자 아이디어를 보호하고 수익화할 수 있도록 플랫폼을 자유롭게 발전시키세요.
