[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Ứng dụng Full Stack OnlyIdeas

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20Android%20%7C%20Web-2ea44f)
![Expo](https://img.shields.io/badge/Expo-48-000020?logo=expo)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61dafb?logo=react)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-orange?logo=amazon-aws)
![Backend](https://img.shields.io/badge/Backend-AppSync%20%2B%20DynamoDB-ff9900)
![Storage](https://img.shields.io/badge/Storage-S3-569A31)
![Auth](https://img.shields.io/badge/Auth-Cognito-DD344C)
![License](https://img.shields.io/badge/License-Not%20Specified-lightgrey)

**OnlyIdeas** là một ứng dụng full-stack giúp mọi người chia sẻ và kiếm tiền từ ý tưởng của mình. Dự án tích hợp **AWS Amplify** cho xác thực người dùng, lưu trữ dữ liệu (AppSync & DynamoDB) và lưu trữ tệp (S3). Bạn có thể chạy dự án này trên **iOS**, **Android** và **Web** thông qua **Expo**.

Lấy cảm hứng từ các tính năng kiểu “OnlyFans”, OnlyIdeas cũng hướng tới tích hợp các công cụ AI để tạo, phân tích và dịch các ý tưởng, âm nhạc hoặc nội dung media do người dùng đóng góp.

README này là bản nháp mở rộng, bám sát repository, được xây dựng từ nội dung README hiện có và các tệp mã nguồn hiện tại.

## Tổng quan 📌

### Stack trong một bảng

| Khu vực | Công nghệ |
|---|---|
| Framework ứng dụng | `React Native` + `Expo` |
| Điều hướng | `expo-router` |
| Auth + Data + Storage | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Cơ sở dữ liệu | `Amazon DynamoDB` (qua mô hình GraphQL của Amplify) |
| Lưu trữ tệp | `Amazon S3` |
| Nền tảng mục tiêu | iOS, Android, Web |

OnlyIdeas sử dụng:

- `expo-router` cho điều hướng và các màn hình theo route.
- `aws-amplify` + `@aws-amplify/ui-react-native` cho auth, API, DataStore và storage.
- Các category backend của Amplify cho **Auth (Cognito)**, **API (AppSync GraphQL)** và **Storage (S3)**.

Luồng người dùng hiện tại:

1. Đăng nhập qua Amplify Authenticator.
2. Bảng tin trang chủ hiển thị danh sách creator (bản ghi `User`).
3. Mở trang hồ sơ creator và xem bài viết/trạng thái paywall.
4. Tạo bài viết mới với tùy chọn tải ảnh lên S3.

## Tính năng ✨

- Danh sách creator và trang hồ sơ.
- Đăng nhập / đăng xuất với Amplify UI Authenticator.
- Tạo bài viết mới với tích hợp chọn ảnh.
- Tải ảnh lên S3 và lấy ảnh về hiển thị.
- Lưu trữ model `User` và `Post` dựa trên GraphQL.
- Chạy iOS, Android và Web từ một dự án Expo duy nhất.

## Cấu trúc dự án 🗂️

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

## Điều kiện tiên quyết ✅

- Khuyến nghị Node.js 18+.
- npm (lockfile là `package-lock.json`).
- Bộ công cụ tương thích Expo:
  - iOS Simulator + Xcode (để mô phỏng iOS cục bộ).
  - Android Studio + SDK/emulator (để mô phỏng Android cục bộ).
- Tài khoản AWS có quyền để provision Amplify.
- Amplify CLI để thiết lập backend.

## Cài đặt 🚀

### 1. Clone Repo

Giữ nguyên lệnh chuẩn hiện có:

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

Remote bám sát repository hiện đang được cấu hình trong repo này:

```bash
git clone git@github.com:lachlanchen/onlyideas-react-native.git
cd onlyideas-react-native
```

Repository này được tinh chỉnh riêng cho nền tảng **OnlyIdeas**, tập trung vào sáng tạo và kiếm tiền.

### 2. Cài Dependencies

Tại thư mục gốc dự án, chạy:

```bash
npm install
```

Lệnh này cài các Node module cần thiết, bao gồm **Expo**, **React Native** và **aws-amplify**.

## Cấu hình & khởi tạo AWS Amplify ☁️

1. **Cài Amplify CLI** (nếu bạn chưa cài):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Cấu hình Amplify** với thông tin xác thực AWS của bạn:

   ```bash
   amplify configure
   ```

   - Đăng nhập AWS console, tạo hoặc dùng IAM user hiện có.
   - Cung cấp `accessKeyId` và `secretAccessKey`.
   - Đặt tên profile mới (ví dụ: `onlyideas`).

3. **Khởi tạo Amplify** trong dự án này:

   ```bash
   amplify init
   ```

   Prompt khuyến nghị:

   - Tên môi trường: `dev` (hoặc tùy bạn)
   - Trình soạn thảo mặc định: tùy bạn
   - Phương thức xác thực: `AWS profile`
   - Profile: chọn profile bạn vừa cấu hình

4. **Đẩy backend Amplify**:

   ```bash
   amplify push
   ```

Thao tác này sẽ provision backend AWS (Cognito, AppSync, S3, v.v.) cho OnlyIdeas.

## Chạy ứng dụng ▶️

Dùng **Expo** để khởi chạy ứng dụng trên nhiều nền tảng:

```bash
npx expo start
```

Hoặc qua package scripts:

| Script | Command | Mục đích |
|---|---|---|
| `npm start` | `expo start` | Khởi động Expo dev server |
| `npm run ios` | `expo start --ios` | Mở iOS simulator |
| `npm run android` | `expo start --android` | Mở Android emulator |
| `npm run web` | `expo start --web` | Chạy bản web |

- Nhấn `i` để mở iOS Simulator (cần macOS + Xcode).
- Nhấn `a` để mở Android emulator (cần Android Studio & SDK).
- Nhấn `w` để mở bản web trong trình duyệt.

### Chạy trên Web

Vì dự án này dùng một số thư viện đặc thù **React Native** (ví dụ `@aws-amplify/ui-react-native`), bạn có thể cần xử lý import có điều kiện nếu gặp lỗi khi bundle cho web. Trong nhiều trường hợp, bản **web** vẫn chạy ngay mà không cần chỉnh sửa. Nếu gặp sự cố, bạn có thể:

- Gỡ hoặc thay thế các import chỉ dành cho native, hoặc
- Bỏ qua bản web và tiếp tục phát triển trên nền tảng native.

## Ghi chú cấu hình ⚙️

### Tệp được tạo bắt buộc: `src/aws-exports.js`

`app/_layout.js` import `../src/aws-exports`, nhưng tệp này do Amplify sinh ra và không được commit trong repository này. Chạy `amplify init` + `amplify push` sẽ tạo tệp đó.

### Cấu trúc backend Amplify

Theo `amplify/backend/backend-config.json`, dự án này gồm:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Chi tiết auth bổ sung bám sát repository:

- Cơ chế xác thực mặc định của AppSync hiện là `API_KEY`, với AWS IAM là provider bổ sung.

### Mô hình dữ liệu GraphQL

Được định nghĩa trong `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- Model `User` với các trường hồ sơ (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- Model `Post` với `text`, `image` tùy chọn, `likes`, và chỉ mục `userID` (`byUser`)

### Cấu hình Expo/Babel

- `index.js` nạp async iterator polyfill và `expo-router/entry`.
- `babel.config.js` bao gồm:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## Ví dụ sử dụng 🧪

### Tạo và đăng bài viết

1. Mở ứng dụng và đăng nhập.
2. Nhấn `New post` ở màn hình trang chủ.
3. Nhập nội dung bài viết.
4. Tùy chọn chọn ảnh từ thư viện.
5. Nhấn `Post` để tải ảnh lên và lưu bản ghi `Post`.

### Quy trình backend cục bộ (điển hình)

```bash
amplify status
amplify pull
amplify push
```

Nếu bạn chỉnh schema/model, hãy tái tạo artifacts khi cần bằng các lệnh Amplify CLI phù hợp trong môi trường của bạn.

## Ghi chú phát triển 🛠️

- Routing theo file thông qua `expo-router` trong `app/`.
- Ứng dụng hiện đang dùng kết hợp `DataStore` và mutation `API.graphql` trực tiếp.
- Khi auth `signIn`, `_layout.js` lắng nghe qua `Hub` và cố gắng tạo bản ghi `User` tương ứng.
- Hiện chưa có script `test` hoặc `lint` chuyên biệt trong `package.json`.
- Thư mục `i18n/` đã tồn tại; các README đa ngôn ngữ được lên kế hoạch nhưng chưa được thêm ở bước bản nháp này.
- Các liên kết ngôn ngữ được chủ đích giữ dưới dạng một dòng tùy chọn duy nhất ở đầu README này.

## Khắc phục sự cố 🧯

### `Cannot find module '../src/aws-exports'`

Chạy:

```bash
amplify init
amplify push
```

Đảm bảo `src/aws-exports.js` đã được tạo cục bộ.

### Đăng nhập thành công nhưng feed người dùng trống

- Xác nhận listener `Hub` khi sign-in đã chạy và mutation tạo user đã thành công.
- Kiểm tra auth mode và quyền truy cập của AppSync.
- Xác minh dữ liệu `User` trong DynamoDB/AppSync console.

### Tải ảnh lên thất bại khi tạo bài mới

- Xác nhận tài nguyên lưu trữ S3 tồn tại trong backend Amplify.
- Kiểm tra người dùng đã xác thực có quyền upload.
- Kiểm tra mạng và thử lại sau khi đăng nhập lại.

### Lỗi web build do import chỉ dành cho native

Import có điều kiện các module chỉ dành cho native, hoặc tập trung phát triển trên iOS/Android nếu khả năng tương thích web bị lỗi.

## Lộ trình / Bước tiếp theo 🧭

- **Tích hợp AI**: Thêm endpoint hoặc gọi API bên thứ ba (ví dụ OpenAI) để hỗ trợ tạo nội dung tự động, phân tích hợp âm nhạc hoặc dịch thuật.
- **Kiếm tiền**: Tích hợp tính năng thuê bao hoặc thanh toán (ví dụ Stripe) nếu bạn muốn tái tạo các tính năng kiếm tiền.
- **Triển khai**: Dùng [EAS Build](https://docs.expo.dev/eas/) hoặc công cụ tương tự để tạo app độc lập cho iOS & Android.
- Mở rộng bộ README đa ngôn ngữ trong `i18n/` bằng các liên kết ngôn ngữ ở đầu tệp này.

## Lời cảm ơn 🙌

- Dự án gốc bởi [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Được điều chỉnh và đổi thương hiệu thành **OnlyIdeas**, tập trung giúp mọi người chia sẻ và kiếm tiền từ ý tưởng, với kế hoạch tích hợp AI cho âm nhạc, dịch ngôn ngữ và cộng tác nghiên cứu.

Để biết thêm chi tiết về codebase và tính năng gốc, hãy xem README trong repository gốc.

## Đóng góp 🤝

Hoan nghênh đóng góp. Trong khi chưa có `CONTRIBUTING.md` chuyên biệt, vui lòng theo luồng nhẹ sau:

1. Fork repo.
2. Tạo nhánh tính năng.
3. Giữ thay đổi tập trung và kiểm tra trên ít nhất một nền tảng mục tiêu.
4. Mở pull request với ghi chú thiết lập/tái hiện lỗi rõ ràng.

Nếu bạn thay đổi tài nguyên Amplify, hãy đưa kèm cập nhật `amplify/` tương ứng và ghi chú migration trong mô tả PR.

## Giấy phép 📄

Hiện chưa có tệp `LICENSE` trong repository này.

Giả định: mặc định mọi quyền được bảo lưu trừ khi/cho đến khi maintainer thêm giấy phép rõ ràng.

---

Chúc bạn xây dựng **OnlyIdeas** hiệu quả, và tùy biến nền tảng để bảo vệ cũng như tối ưu giá trị ý tưởng người dùng với sự hỗ trợ của AI.
