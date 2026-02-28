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

**OnlyIdeas** là ứng dụng full-stack giúp mọi người chia sẻ và kiếm tiền từ ý tưởng của họ. Dự án tích hợp **AWS Amplify** để xác thực người dùng, lưu trữ dữ liệu (AppSync & DynamoDB) và lưu trữ tệp (S3). Bạn có thể chạy dự án này trên **iOS**, **Android** và **Web** thông qua **Expo**.

Lấy cảm hứng từ các tính năng theo phong cách “OnlyFans”, OnlyIdeas còn hướng tới việc tích hợp công cụ AI để tạo, phân tích và dịch các ý tưởng, nhạc, hoặc nội dung do người dùng đóng góp.

README này là bản thảo mở rộng, bám sát repository, được soạn dựa trên nội dung README hiện có và các file nguồn hiện tại.

## Tổng quan 📌

### Stack at a glance

| Lĩnh vực | Công nghệ |
|---|---|
| Khung ứng dụng | `React Native` + `Expo` |
| Điều hướng | `expo-router` |
| Auth + Data + Storage | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Cơ sở dữ liệu | `Amazon DynamoDB` (qua mô hình GraphQL của Amplify) |
| Lưu trữ tệp | `Amazon S3` |
| Mục tiêu | iOS, Android, Web |

OnlyIdeas sử dụng:

- `expo-router` cho điều hướng và các màn hình theo route.
- `aws-amplify` + `@aws-amplify/ui-react-native` cho auth, API, DataStore và storage.
- Các module backend của Amplify cho **Auth (Cognito)**, **API (AppSync GraphQL)** và **Storage (S3)**.

Luồng người dùng hiện tại:

1. Đăng nhập qua Amplify Authenticator.
2. Home feed hiển thị danh sách creator (`User` records).
3. Mở hồ sơ creator và xem bài đăng/trạng thái paywall.
4. Tạo bài đăng mới kèm tùy chọn tải ảnh lên S3.

## Tính năng ✨

- Trang danh sách creator và profile.
- Đăng nhập / đăng xuất với Amplify UI Authenticator.
- Tạo bài đăng mới với tích hợp trình chọn ảnh.
- Tải ảnh lên S3 và truy xuất ảnh.
- Lưu trữ model `User` và `Post` nhờ GraphQL.
- Khởi chạy iOS, Android và Web từ một project Expo.

## Cấu trúc project 🗂️

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

## Yêu cầu trước khi cài đặt ✅

- Khuyến nghị Node.js 18+.
- npm (lockfile là `package-lock.json`).
- Bộ công cụ tương thích với Expo:
  - iOS Simulator + Xcode (cho mô phỏng iOS nội bộ).
  - Android Studio + SDK/emulator (cho mô phỏng Android nội bộ).
- Tài khoản AWS để provision Amplify.
- Amplify CLI cho việc thiết lập backend.

## Cài đặt 🚀

### 1. Clone Repo

Bạn có thể dùng remote phù hợp với quy trình làm việc:

| Lệnh | Ghi chú |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | Tham chiếu lịch sử/địa chỉ lưu trữ cũ |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | Repository hiện tại (khuyến nghị) |

Sau đó mở đúng thư mục dự án:

```bash
cd onlyideas-react-native
```

Repository này được thiết kế riêng cho nền tảng **OnlyIdeas**, tập trung vào sáng tạo và kiếm tiền từ ý tưởng.

### 2. Cài đặt dependencies

Từ root project, chạy:

```bash
npm install
```

Lệnh này cài các Node modules cần thiết, bao gồm **Expo**, **React Native** và **aws-amplify**.

## Cấu hình & khởi tạo AWS Amplify ☁️

1. **Cài đặt Amplify CLI** (nếu chưa có):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Cấu hình Amplify** với thông tin xác thực AWS:

   ```bash
   amplify configure
   ```

   - Đăng nhập AWS console, tạo mới hoặc dùng IAM user hiện có.
   - Cung cấp `accessKeyId` và `secretAccessKey`.
   - Đặt tên profile mới (ví dụ: `onlyideas`).

3. **Khởi tạo Amplify** trong project này:

   ```bash
   amplify init
   ```

   Các gợi ý khi đáp án:

   - Environment name: `dev` (hoặc theo lựa chọn của bạn)
   - Default editor: theo lựa chọn của bạn
   - Authentication method: `AWS profile`
   - Profile: chọn profile vừa cấu hình

4. **Đẩy backend Amplify**:

   ```bash
   amplify push
   ```

Lệnh này sẽ provision backend AWS (Cognito, AppSync, S3, v.v.) cho OnlyIdeas.

## Chạy app ▶️

Dùng **Expo** để chạy app trên các nền tảng khác nhau:

```bash
npx expo start
```

Hoặc qua package scripts:

| Script | Command | Mục đích |
|---|---|---|
| `npm start` | `expo start` | Khởi chạy Expo dev server |
| `npm run ios` | `expo start --ios` | Mở iOS simulator |
| `npm run android` | `expo start --android` | Mở Android emulator |
| `npm run web` | `expo start --web` | Chạy target web |

- Nhấn `i` để mở iOS Simulator (yêu cầu macOS + Xcode).
- Nhấn `a` để mở Android emulator (yêu cầu Android Studio & SDK).
- Nhấn `w` để mở bản web trong trình duyệt.

### Chạy trên Web

Vì project này dùng một số thư viện đặc thù của **React Native** (ví dụ `@aws-amplify/ui-react-native`), bạn có thể cần xử lý import có điều kiện khi gặp lỗi khi bundling cho web. Ở nhiều trường hợp, bản **web** sẽ hoạt động ngay. Nếu gặp vấn đề, bạn có thể:

- Bỏ hoặc thay thế các import chỉ dành cho native, hoặc
- Bỏ qua bản web và tiếp tục dùng nền tảng native.

## Ghi chú cấu hình ⚙️

### File sinh bắt buộc: `src/aws-exports.js`

`app/_layout.js` import `../src/aws-exports`, nhưng file này do Amplify sinh ra và không được commit trong repository. Chạy `amplify init` + `amplify push` sẽ tạo ra nó.

### Kiến trúc backend Amplify

Từ `amplify/backend/backend-config.json`, project này bao gồm:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Thông tin auth bổ sung theo đúng trạng thái repository:

- AppSync hiện đang dùng xác thực mặc định là `API_KEY` với AWS IAM làm provider bổ sung.

### Mô hình dữ liệu GraphQL

Được định nghĩa trong `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- Model `User` với các trường hồ sơ (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- Model `Post` với `text`, `image` tùy chọn, `likes`, và chỉ mục `userID` (`byUser`).

### Cấu hình Expo/Babel

- `index.js` tải async iterator polyfill và `expo-router/entry`.
- `babel.config.js` bao gồm:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## Ví dụ sử dụng 🧪

### Tạo và đăng bài

1. Mở app rồi đăng nhập.
2. Nhấn `New post` trên màn hình chính.
3. Nhập nội dung bài đăng.
4. Tùy chọn chọn ảnh từ thư viện.
5. Nhấn `Post` để upload ảnh và lưu bản ghi `Post`.

### Luồng backend cục bộ (điển hình)

```bash
amplify status
amplify pull
amplify push
```

Nếu bạn sửa schema/models, hãy tái tạo artifacts cần thiết bằng các lệnh Amplify CLI tương ứng trong môi trường của bạn.

## Ghi chú phát triển 🛠️

- Routing theo tệp qua `expo-router` trong `app/`.
- Ứng dụng hiện tại dùng kết hợp `DataStore` và mutation trực tiếp bằng `API.graphql`.
- Khi auth `signIn`, `_layout.js` lắng nghe qua `Hub` và cố gắng tạo bản ghi `User` tương ứng.
- Không có script `test` hoặc `lint` chuyên dụng nào hiện được định nghĩa trong `package.json`.
- Thư mục `i18n/` đã tồn tại; các file README theo ngôn ngữ đã được thêm.
- Các liên kết ngôn ngữ được giữ dưới dạng một dòng chọn lựa duy nhất ở đầu README này.

## Gỡ lỗi 🧯

### `Cannot find module '../src/aws-exports'`

Chạy:

```bash
amplify init
amplify push
```

Đảm bảo `src/aws-exports.js` đã được tạo tại máy local.

### Auth thành công nhưng feed người dùng trống

- Xác nhận listener `Hub` khi sign-in đã chạy và mutation tạo user đã thành công.
- Kiểm tra AppSync auth mode và quyền truy cập.
- Kiểm tra dữ liệu `User` trong bảng điều khiển DynamoDB/AppSync.

### Upload ảnh lỗi khi tạo bài mới

- Xác nhận tài nguyên S3 đã tồn tại trong backend Amplify.
- Kiểm tra người dùng đã xác thực có quyền upload hay không.
- Kiểm tra kết nối mạng và thử lại sau khi đăng nhập lại.

### Lỗi build web do import native-only

Import có điều kiện các module chỉ dành cho native, hoặc tập trung phát triển iOS/Android nếu tính năng web bị ảnh hưởng.

## Roadmap / Bước tiếp theo 🧭

- **Tích hợp AI**: Thêm endpoint hoặc gọi API bên thứ ba (ví dụ OpenAI) để hỗ trợ tạo nội dung tự động, phân tích hợp âm nhạc, hoặc dịch thuật.
- **Monetization**: Tích hợp đăng ký hoặc thanh toán (ví dụ Stripe) nếu bạn muốn tái hiện các tính năng mô hình hóa doanh thu.
- **Triển khai**: Dùng [EAS Build](https://docs.expo.dev/eas/) hoặc giải pháp tương tự để tạo app độc lập cho iOS & Android.
- Mở rộng bộ README đa ngôn ngữ trong `i18n/` dùng đường dẫn language links ở đầu file này.

## Acknowledgments 🙌

- Dự án gốc bởi [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Được chỉnh sửa lại và đổi thương hiệu thành **OnlyIdeas**, tập trung giúp mọi người chia sẻ và kiếm tiền từ ý tưởng, với các tính năng AI cho âm nhạc, dịch thuật và hợp tác nghiên cứu đã được lên kế hoạch.

Để biết thêm chi tiết về codebase và tính năng gốc, xem README trong repository gốc.

## Giấy phép 📄

Hiện chưa có tệp `LICENSE` trong repository này.

Giả định: tất cả quyền được bảo lưu theo mặc định cho tới khi maintainer thêm giấy phép rõ ràng.

---

Chúc bạn xây dựng **OnlyIdeas** hiệu quả, và thoải mái điều chỉnh nền tảng để bảo vệ cũng như tối ưu hóa giá trị ý tưởng của người dùng với sự hỗ trợ của AI.


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
