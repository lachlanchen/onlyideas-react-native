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

**OnlyIdeas** — это full-stack приложение, которое помогает людям делиться своими идеями и монетизировать их. Оно интегрировано с **AWS Amplify** для аутентификации пользователей, хранения данных (AppSync и DynamoDB) и размещения файлов (S3). Проект можно запускать на **iOS**, **Android** и **Web** через **Expo**.

Вдохновлённый возможностями в стиле “OnlyFans”, проект OnlyIdeas также нацелен на интеграцию AI-инструментов для генерации, анализа и перевода пользовательских идей, музыки или медиаконтента.

Этот README — расширенный и соответствующий текущему репозиторию черновик, основанный на существующем содержимом README и актуальных файлах исходного кода.

## Обзор 📌

### Стек в двух словах

| Область | Технология |
|---|---|
| Фреймворк приложения | `React Native` + `Expo` |
| Навигация | `expo-router` |
| Auth + Data + Storage | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| База данных | `Amazon DynamoDB` (через модели Amplify GraphQL) |
| Хранилище файлов | `Amazon S3` |
| Целевые платформы | iOS, Android, Web |

OnlyIdeas использует:

- `expo-router` для навигации и экранов на основе маршрутов.
- `aws-amplify` + `@aws-amplify/ui-react-native` для auth, API, DataStore и storage.
- Backend-категории Amplify для **Auth (Cognito)**, **API (AppSync GraphQL)** и **Storage (S3)**.

Текущий пользовательский сценарий:

1. Вход через Amplify Authenticator.
2. На главной ленте отображаются авторы (записи `User`).
3. Открытие профиля автора и просмотр постов/состояния paywall.
4. Создание нового поста с необязательной загрузкой изображения в S3.

## Возможности ✨

- Список авторов и страницы профилей.
- Вход / выход через Amplify UI Authenticator.
- Создание новых постов с интеграцией выбора изображений.
- Загрузка изображений в S3 и получение изображений.
- Сохранение моделей `User` и `Post` через GraphQL.
- Запуск на iOS, Android и Web из одного Expo-проекта.

## Структура проекта 🗂️

```text
.
├── app/
│   ├── _layout.js           # Конфигурация Amplify + обёртка Authenticator
│   ├── index.js             # Главная лента (список пользователей)
│   ├── newPost.js           # Создание поста + необязательная загрузка изображения
│   └── user/[id].js         # Профиль автора + посты
├── src/
│   ├── components/
│   │   ├── UserCard.js
│   │   ├── UserProfileHeader.js
│   │   └── Post.js
│   ├── graphql/             # Сгенерированные операции/артефакты схемы
│   └── models/              # Результаты Amplify modelgen
├── amplify/
│   └── backend/             # Backend-ресурсы Amplify (auth/api/storage)
├── i18n/                    # Директория переводов README (сейчас пуста)
├── app.json
├── babel.config.js
├── index.js
└── package.json
```

## Требования ✅

- Рекомендуется Node.js 18+.
- npm (lockfile: `package-lock.json`).
- Инструменты, совместимые с Expo:
  - iOS Simulator + Xcode (для локальной симуляции iOS).
  - Android Studio + SDK/emulator (для локальной симуляции Android).
- Доступ к AWS-аккаунту для развертывания Amplify.
- Amplify CLI для настройки backend.

## Установка 🚀

### 1. Клонируйте репозиторий

С сохранением существующей канонической команды:

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

Текущий репозиторий с корректным remote:

```bash
git clone git@github.com:lachlanchen/onlyideas-react-native.git
cd onlyideas-react-native
```

Этот репозиторий специально адаптирован под платформу **OnlyIdeas**, с фокусом на креативность и монетизацию.

### 2. Установите зависимости

Из корня проекта выполните:

```bash
npm install
```

Команда установит необходимые модули Node, включая **Expo**, **React Native** и **aws-amplify**.

## Настройка и инициализация AWS Amplify ☁️

1. **Установите Amplify CLI** (если ещё не установлен):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Настройте Amplify** с вашими AWS-учётными данными:

   ```bash
   amplify configure
   ```

   - Войдите в AWS Console, создайте IAM-пользователя или используйте существующего.
   - Укажите `accessKeyId` и `secretAccessKey`.
   - Задайте имя профиля (например, `onlyideas`).

3. **Инициализируйте Amplify** в проекте:

   ```bash
   amplify init
   ```

   Рекомендуемые ответы в мастере:

   - Environment name: `dev` (или другое значение)
   - Default editor: на ваш выбор
   - Authentication method: `AWS profile`
   - Profile: выберите профиль, который только что настроили

4. **Выполните push backend-ресурсов Amplify**:

   ```bash
   amplify push
   ```

Эта команда развернёт AWS backend для OnlyIdeas (Cognito, AppSync, S3 и т.д.).

## Запуск приложения ▶️

Используйте **Expo** для запуска приложения на разных платформах:

```bash
npx expo start
```

Или через скрипты из `package.json`:

| Скрипт | Команда | Назначение |
|---|---|---|
| `npm start` | `expo start` | Запуск Expo dev server |
| `npm run ios` | `expo start --ios` | Запуск iOS Simulator |
| `npm run android` | `expo start --android` | Запуск Android emulator |
| `npm run web` | `expo start --web` | Запуск web-версии |

- Нажмите `i`, чтобы открыть iOS Simulator (нужны macOS + Xcode).
- Нажмите `a`, чтобы открыть Android emulator (нужны Android Studio и SDK).
- Нажмите `w`, чтобы открыть web-сборку в браузере.

### Запуск в Web

Поскольку в проекте используются некоторые библиотеки, специфичные для **React Native** (например, `@aws-amplify/ui-react-native`), при сборке web-версии может понадобиться условная обработка таких импортов. Во многих случаях **web** работает сразу. Если возникают проблемы, можно:

- Удалить или заменить импорты, которые работают только в native-среде, или
- Пропустить web-сборку и продолжить разработку для native-платформ.

## Заметки по конфигурации ⚙️

### Обязательный сгенерированный файл: `src/aws-exports.js`

`app/_layout.js` импортирует `../src/aws-exports`, но этот файл генерируется Amplify и не хранится в репозитории. После `amplify init` + `amplify push` он должен появиться.

### Структура backend в Amplify

Согласно `amplify/backend/backend-config.json`, проект включает:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Дополнительная, подтверждённая по репозиторию деталь по auth:

- Для AppSync по умолчанию используется аутентификация `API_KEY`, а AWS IAM подключён как дополнительный провайдер.

### Модель данных GraphQL

Определена в `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- Модель `User` с полями профиля (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- Модель `Post` с `text`, необязательным `image`, `likes` и индексом `userID` (`byUser`)

### Настройка Expo/Babel

- `index.js` подключает polyfill async iterator и `expo-router/entry`.
- `babel.config.js` включает:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## Примеры использования 🧪

### Создание и публикация поста

1. Откройте приложение и выполните вход.
2. Нажмите `New post` на главном экране.
3. Введите текст поста.
4. При необходимости выберите изображение из библиотеки.
5. Нажмите `Post`, чтобы загрузить изображение и сохранить запись `Post`.

### Локальный workflow backend (типичный)

```bash
amplify status
amplify pull
amplify push
```

Если вы меняете schema/models, при необходимости заново генерируйте артефакты через команды Amplify CLI в вашем окружении.

## Заметки по разработке 🛠️

- Роутинг файловый, через `expo-router` в каталоге `app/`.
- В текущем приложении смешивается использование `DataStore` и прямых мутаций `API.graphql`.
- При auth `signIn` файл `_layout.js` слушает события через `Hub` и пытается создать соответствующую запись `User`.
- Отдельные скрипты `test` и `lint` сейчас не определены в `package.json`.
- Каталог `i18n/` существует; файлы README на других языках запланированы, но на этапе этого черновика ещё не добавлены.
- Ссылки на языки намеренно оставлены одной строкой опций в верхней части этого README.

## Устранение неполадок 🧯

### `Cannot find module '../src/aws-exports'`

Выполните:

```bash
amplify init
amplify push
```

Убедитесь, что `src/aws-exports.js` сгенерирован локально.

### Аутентификация проходит, но лента пользователей пустая

- Убедитесь, что listener `Hub` на `sign-in` сработал и мутация создания пользователя завершилась успешно.
- Проверьте режим auth AppSync и разрешения.
- Проверьте данные `User` в консоли DynamoDB/AppSync.

### Не загружается изображение при создании поста

- Убедитесь, что ресурс S3 storage существует в backend Amplify.
- Проверьте, что у аутентифицированного пользователя есть права на загрузку.
- Проверьте сетевое подключение и повторите попытку после повторной аутентификации.

### Ошибки web-сборки из-за native-only импортов

Используйте условный импорт модулей, работающих только в native-среде, или сосредоточьтесь на iOS/Android во время разработки, если совместимость с web нарушается.

## Roadmap / Следующие шаги 🧭

- **AI Integration**: добавить endpoints или вызовы сторонних API (например, OpenAI) для автоматической генерации контента, анализа музыкальных аккордов или переводов.
- **Monetization**: интегрировать подписки или платежи (например, Stripe), если вы хотите воспроизвести монетизируемые возможности.
- **Deployment**: использовать [EAS Build](https://docs.expo.dev/eas/) или аналогичный инструмент для сборки standalone-приложений под iOS и Android.
- Расширять набор README-переводов в `i18n/` через языковые ссылки в верхней части файла.

## Благодарности 🙌

- Оригинальный проект: [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Проект адаптирован и переименован в **OnlyIdeas** с фокусом на помощь людям в публикации и монетизации их идей, с планируемыми AI-функциями для музыки, языкового перевода и исследовательского сотрудничества.

Для дополнительных деталей по исходной кодовой базе и возможностям см. README в оригинальном репозитории.

## Участие в разработке 🤝

Контрибьюции приветствуются. Пока отдельный `CONTRIBUTING.md` не добавлен, используйте этот упрощённый процесс:

1. Сделайте fork репозитория.
2. Создайте feature-ветку.
3. Делайте точечные изменения и проверяйте их как минимум на одной целевой платформе.
4. Откройте pull request с понятными заметками по настройке/воспроизведению.

Если вы изменяете ресурсы Amplify, добавьте соответствующие изменения в `amplify/` и миграционные заметки в описание PR.

## Лицензия 📄

Файл `LICENSE` в текущем репозитории отсутствует.

Предположение: по умолчанию все права защищены до тех пор, пока мейнтейнеры явно не добавят лицензию.

---

Удачной разработки **OnlyIdeas**. При необходимости адаптируйте платформу так, чтобы защищать и монетизировать пользовательские идеи с помощью AI.
