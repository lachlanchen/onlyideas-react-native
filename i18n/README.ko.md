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

**OnlyIdeas**는 사용자가 아이디어를 공유하고 수익화할 수 있도록 돕는 풀스택 애플리케이션입니다. 사용자 인증, 데이터 저장(AppSync & DynamoDB), 파일 호스팅(S3)을 위해 **AWS Amplify**와 통합되어 있습니다. **Expo**를 통해 **iOS**, **Android**, **Web**에서 이 프로젝트를 실행할 수 있습니다.

OnlyIdeas는 “OnlyFans 스타일” 기능에서 영감을 받았으며, 사용자가 기여한 아이디어, 음악, 미디어를 생성·분석·번역하기 위한 AI 도구 통합도 목표로 하고 있습니다.

이 README는 기존 README 내용과 현재 소스 파일을 바탕으로 확장한, 저장소 기준에 맞는 초안입니다.

## 개요 📌

### 한눈에 보는 스택

| 영역 | 기술 |
|---|---|
| 앱 프레임워크 | `React Native` + `Expo` |
| 내비게이션 | `expo-router` |
| 인증 + 데이터 + 스토리지 | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| 데이터베이스 | `Amazon DynamoDB` (Amplify GraphQL 모델 기반) |
| 파일 스토리지 | `Amazon S3` |
| 대상 플랫폼 | iOS, Android, Web |

OnlyIdeas는 다음을 사용합니다:

- 내비게이션 및 라우트 기반 화면 구성을 위한 `expo-router`.
- 인증, API, DataStore, 스토리지를 위한 `aws-amplify` + `@aws-amplify/ui-react-native`.
- **Auth(Cognito)**, **API(AppSync GraphQL)**, **Storage(S3)**를 위한 Amplify 백엔드 카테고리.

현재 사용자 흐름:

1. Amplify Authenticator를 통해 로그인합니다.
2. 홈 피드에 크리에이터 목록(`User` 레코드)이 표시됩니다.
3. 크리에이터 프로필을 열어 게시물 및 페이월 상태를 확인합니다.
4. 새 게시물을 작성하고 필요 시 이미지를 S3에 업로드합니다.

## 기능 ✨

- 크리에이터 목록 및 프로필 페이지.
- Amplify UI Authenticator 기반 로그인/로그아웃.
- 이미지 선택기 연동이 포함된 새 게시물 작성.
- S3 이미지 업로드 및 이미지 조회.
- GraphQL 기반 `User`, `Post` 모델 영속화.
- 하나의 Expo 프로젝트에서 iOS, Android, Web 실행 타깃 지원.

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
├── i18n/                    # Translation README directory (currently empty)
├── app.json
├── babel.config.js
├── index.js
└── package.json
```

## 사전 준비 사항 ✅

- Node.js 18+ 권장.
- npm (`package-lock.json` 사용).
- Expo 호환 도구:
  - iOS Simulator + Xcode(iOS 로컬 시뮬레이션용).
  - Android Studio + SDK/에뮬레이터(Android 로컬 시뮬레이션용).
- Amplify 프로비저닝을 위한 AWS 계정 접근 권한.
- 백엔드 설정을 위한 Amplify CLI.

## 설치 🚀

### 1. 저장소 클론

기존 표준 명령 유지:

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

이 저장소에 현재 설정된 실제 원격 주소:

```bash
git clone git@github.com:lachlanchen/onlyideas-react-native.git
cd onlyideas-react-native
```

이 저장소는 **OnlyIdeas** 플랫폼에 맞춰져 있으며, 창의성과 수익화에 초점을 둡니다.

### 2. 의존성 설치

프로젝트 루트에서 실행:

```bash
npm install
```

이 명령은 **Expo**, **React Native**, **aws-amplify**를 포함한 필요한 Node 모듈을 설치합니다.

## AWS Amplify 구성 및 초기화 ☁️

1. 아직 설치하지 않았다면 **Amplify CLI 설치**:

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. AWS 자격 증명으로 **Amplify 구성**:

   ```bash
   amplify configure
   ```

   - AWS 콘솔에 로그인하여 IAM 사용자를 새로 만들거나 기존 사용자를 사용합니다.
   - `accessKeyId`, `secretAccessKey`를 입력합니다.
   - 새 프로필 이름을 지정합니다(예: `onlyideas`).

3. 이 프로젝트에서 **Amplify 초기화**:

   ```bash
   amplify init
   ```

   권장 프롬프트:

   - Environment name: `dev` (또는 원하는 이름)
   - Default editor: 자유 선택
   - Authentication method: `AWS profile`
   - Profile: 방금 구성한 프로필 선택

4. **Amplify 백엔드 푸시**:

   ```bash
   amplify push
   ```

이 과정으로 OnlyIdeas용 AWS 백엔드(Cognito, AppSync, S3 등)가 프로비저닝됩니다.

## 앱 실행 ▶️

**Expo**를 사용해 다양한 플랫폼에서 앱을 실행합니다:

```bash
npx expo start
```

또는 package script 사용:

| 스크립트 | 명령어 | 용도 |
|---|---|---|
| `npm start` | `expo start` | Expo 개발 서버 시작 |
| `npm run ios` | `expo start --ios` | iOS 시뮬레이터 실행 |
| `npm run android` | `expo start --android` | Android 에뮬레이터 실행 |
| `npm run web` | `expo start --web` | 웹 타깃 실행 |

- `i`를 누르면 iOS Simulator가 열립니다(macOS + Xcode 필요).
- `a`를 누르면 Android 에뮬레이터가 열립니다(Android Studio & SDK 필요).
- `w`를 누르면 브라우저에서 웹 빌드가 열립니다.

### 웹에서 실행

이 프로젝트는 일부 **React Native** 전용 라이브러리(예: `@aws-amplify/ui-react-native`)를 사용하므로, 웹 번들링 중 오류가 발생하면 해당 import를 조건부 처리해야 할 수 있습니다. 많은 경우 **web**도 바로 동작합니다. 문제가 발생하면 다음 중 하나를 선택하세요.

- 네이티브 전용 import를 제거하거나 대체하거나,
- 웹 빌드를 건너뛰고 네이티브 플랫폼 중심으로 개발을 진행합니다.

## 설정 참고 사항 ⚙️

### 필수 생성 파일: `src/aws-exports.js`

`app/_layout.js`는 `../src/aws-exports`를 import하지만, 이 파일은 Amplify가 생성하며 이 저장소에는 커밋되어 있지 않습니다. `amplify init` + `amplify push`를 실행하면 생성됩니다.

### Amplify 백엔드 구성

`amplify/backend/backend-config.json` 기준, 이 프로젝트에는 다음이 포함됩니다:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

추가 저장소 기준 인증 정보:

- AppSync 기본 인증은 현재 `API_KEY`이며, 추가 제공자로 AWS IAM이 설정되어 있습니다.

### GraphQL 데이터 모델

`amplify/backend/api/OnlyFansCloneApp/schema.graphql`에 정의됨:

- 프로필 필드(`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)를 가진 `User` 모델
- `text`, 선택적 `image`, `likes`, `userID` 인덱스(`byUser`)를 가진 `Post` 모델

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
4. 필요 시 라이브러리에서 이미지를 선택합니다.
5. `Post`를 탭해 이미지를 업로드하고 `Post` 레코드를 저장합니다.

### 로컬 백엔드 워크플로(일반적)

```bash
amplify status
amplify pull
amplify push
```

스키마/모델을 수정한 경우, 환경에 맞는 Amplify CLI 명령으로 필요한 산출물을 다시 생성하세요.

## 개발 노트 🛠️

- 라우팅은 `app/` 아래 `expo-router` 기반 파일 라우팅을 사용합니다.
- 현재 앱은 `DataStore`와 직접 `API.graphql` mutation 사용을 혼합하고 있습니다.
- 인증 `signIn` 시 `_layout.js`는 `Hub`를 통해 이벤트를 수신하고, 대응되는 `User` 레코드 생성을 시도합니다.
- 현재 `package.json`에는 전용 `test` 또는 `lint` 스크립트가 정의되어 있지 않습니다.
- `i18n/` 디렉터리는 존재하며, 이 초안 단계에서는 언어별 README 파일이 아직 추가되지 않았습니다.
- 언어 링크는 이 README 상단에 단일 옵션 줄로 의도적으로 유지됩니다.

## 문제 해결 🧯

### `Cannot find module '../src/aws-exports'`

다음을 실행하세요:

```bash
amplify init
amplify push
```

로컬에 `src/aws-exports.js`가 생성되어 있는지 확인하세요.

### 인증은 성공하지만 사용자 피드가 비어 있음

- `Hub`의 sign-in 리스너가 실행되었고 사용자 생성 mutation이 성공했는지 확인합니다.
- AppSync 인증 모드와 권한을 확인합니다.
- DynamoDB/AppSync 콘솔에서 `User` 레코드 데이터를 확인합니다.

### 새 게시물에서 이미지 업로드 실패

- Amplify 백엔드에 S3 스토리지 리소스가 존재하는지 확인합니다.
- 인증된 사용자에게 업로드 권한이 있는지 확인합니다.
- 네트워크 접근 상태를 확인하고 재인증 후 다시 시도합니다.

### 네이티브 전용 import로 인한 웹 빌드 오류

네이티브 전용 모듈을 조건부 import 처리하거나, 웹 호환성 이슈가 있는 경우 iOS/Android 중심으로 개발하세요.

## 로드맵 / 다음 단계 🧭

- **AI 통합**: 자동 콘텐츠 생성, 음악 코드 분석, 번역을 지원하기 위해 엔드포인트 또는 서드파티 API 호출(예: OpenAI)을 추가합니다.
- **수익화**: 수익화 기능을 재현하려면 구독/결제 기능(예: Stripe)을 통합합니다.
- **배포**: [EAS Build](https://docs.expo.dev/eas/) 등을 사용해 iOS/Android용 standalone 앱을 생성합니다.
- 이 파일 상단의 언어 링크를 활용하여 `i18n/` 아래 언어별 README 세트를 확장합니다.

## 감사의 말 🙌

- 원본 프로젝트: [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- 아이디어 공유 및 수익화에 초점을 맞춘 **OnlyIdeas**로 재구성 및 리브랜딩되었으며, 음악·언어 번역·리서치 협업을 위한 AI 기능이 계획되어 있습니다.

원본 코드베이스와 기능에 대한 추가 정보는 원본 저장소의 README를 확인하세요.

## 기여 🤝

기여를 환영합니다. 전용 `CONTRIBUTING.md`가 추가되기 전까지는 아래 간단한 흐름을 따라주세요:

1. 저장소를 포크합니다.
2. 기능 브랜치를 생성합니다.
3. 변경 범위를 집중적으로 유지하고 최소 한 개 타깃 플랫폼에서 테스트합니다.
4. 설정/재현 절차를 명확히 적어 Pull Request를 엽니다.

Amplify 리소스를 변경하는 경우, 해당 `amplify/` 업데이트와 마이그레이션 노트를 PR 설명에 포함하세요.

## 라이선스 📄

현재 이 저장소에는 `LICENSE` 파일이 없습니다.

가정: 유지관리자가 명시적 라이선스를 추가하기 전까지 기본적으로 모든 권리는 보유됩니다.

---

**OnlyIdeas**를 즐겁게 개발해 보세요. AI 지원을 통해 사용자 아이디어를 보호하고 수익화할 수 있도록 플랫폼을 자유롭게 확장해 보시기 바랍니다.
