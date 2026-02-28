[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# Полнофункциональное приложение OnlyIdeas

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

**OnlyIdeas** — это полнофункциональное приложение, которое помогает людям делиться идеями и монетизировать их. Оно интегрируется с **AWS Amplify** для авторизации пользователей, хранения данных (AppSync и DynamoDB) и хранения файлов (S3). Этот проект можно запускать на **iOS**, **Android** и **Web** через **Expo**.

Вдохновлённый возможностями в стиле **OnlyFans**, OnlyIdeas также нацелен на интеграцию инструментов ИИ для генерации, анализа и перевода пользовательских идей, музыки или медиа.

Этот README — расширенный черновик, максимально соответствующий репозиторию, на основе текущего содержимого исходного README и файлов проекта.

## Обзор 📌

### Стек с первого взгляда

| Область | Технологии |
|---|---|
| Фреймворк приложения | `React Native` + `Expo` |
| Навигация | `expo-router` |
| Авторизация + данные + хранилище | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| База данных | `Amazon DynamoDB` (через модели Amplify GraphQL) |
| Файловое хранилище | `Amazon S3` |
| Целевые платформы | iOS, Android, Web |

OnlyIdeas использует:

- `expo-router` для навигации и экранов по маршрутам.
- `aws-amplify` + `@aws-amplify/ui-react-native` для авторизации, API, DataStore и хранения.
- Бэкенд-категории Amplify для **Auth (Cognito)**, **API (AppSync GraphQL)** и **Storage (S3)**.

Текущий пользовательский флоу:

1. Вход через Amplify Authenticator.
2. Главная лента показывает создателей (`User` записи).
3. Открытие профиля создателя и просмотр постов/состояния paywall.
4. Создание нового поста с опциональной загрузкой изображения в S3.

## Особенности ✨

- Страницы списка создателей и профилей.
- Вход/выход с помощью Amplify UI Authenticator.
- Создание новых постов с интеграцией выбора изображения.
- Загрузка и получение изображений через S3.
- Персистентность моделей `User` и `Post` через GraphQL.
- Запуск на iOS, Android и Web из одного проекта Expo.

## Структура проекта 🗂️

```text
.
├── app/
│   ├── _layout.js           # Настройка Amplify + обёртка Authenticator
│   ├── index.js             # Главная лента (список пользователей)
│   ├── newPost.js           # Создание поста + опциональная загрузка изображения
│   └── user/[id].js         # Профиль создателя + посты
├── src/
│   ├── components/
│   │   ├── UserCard.js
│   │   ├── UserProfileHeader.js
│   │   └── Post.js
│   ├── graphql/             # Сгенерированные артефакты операций и схем
│   └── models/              # Результаты modelgen из Amplify
├── amplify/
│   └── backend/             # Ресурсы бэкенда Amplify (auth/api/storage)
├── i18n/                    # Каталог переводов README (на текущий момент пустой)
├── app.json
├── babel.config.js
├── index.js
└── package.json
```

## Требования ✅

- Рекомендуется Node.js 18+.
- npm (файл lockfile — `package-lock.json`).
- Инструменты, совместимые с Expo:
  - iOS Simulator + Xcode (для локальной симуляции iOS).
  - Android Studio + SDK/эмулятор (для локальной симуляции Android).
- Доступ к аккаунту AWS для provisioning Amplify.
- Amplify CLI для настройки бэкенда.

## Установка 🚀

### 1. Клонирование репозитория

Используйте тот remote, который подходит под ваш рабочий процесс:

| Команда | Примечание |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | Историческая/архивная ссылка |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | Текущий репозиторий (рекомендуется) |

Затем откройте нужную директорию проекта:

```bash
cd onlyideas-react-native
```

Этот репозиторий специально адаптирован под платформу **OnlyIdeas**, фокусируясь на креативе и монетизации.

### 2. Установка зависимостей

Выполните из корня проекта:

```bash
npm install
```

Это установит необходимые модули Node, включая **Expo**, **React Native** и **aws-amplify**.

## Настройка и инициализация AWS Amplify ☁️

1. **Установите Amplify CLI** (если ещё не установили):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Настройте Amplify** с вашими учетными данными AWS:

   ```bash
   amplify configure
   ```

   - Войдите в консоль AWS, создайте нового пользователя IAM или используйте существующего.
   - Укажите `accessKeyId` и `secretAccessKey`.
   - Назовите новый профиль (например, `onlyideas`).

3. **Инициализируйте Amplify** в этом проекте:

   ```bash
   amplify init
   ```

   Рекомендуемые ответы:

   - Имя окружения: `dev` (или выбранное вами)
   - Редактор по умолчанию: на ваше усмотрение
   - Метод авторизации: `AWS profile`
   - Профиль: выберите только что настроенный

4. **Опубликуйте бэкенд Amplify**:

   ```bash
   amplify push
   ```

Это создаёт инфраструктуру AWS (Cognito, AppSync, S3 и т.д.) для OnlyIdeas.

## Запуск приложения ▶️

Используйте **Expo** для запуска приложения на разных платформах:

```bash
npx expo start
```

Или через скрипты из package.json:

| Скрипт | Команда | Цель |
|---|---|---|
| `npm start` | `expo start` | Запустить сервер разработки Expo |
| `npm run ios` | `expo start --ios` | Запустить iOS-симулятор |
| `npm run android` | `expo start --android` | Запустить эмулятор Android |
| `npm run web` | `expo start --web` | Запустить web-таргет |

- Нажмите `i`, чтобы открыть iOS Simulator (требуются macOS + Xcode).
- Нажмите `a`, чтобы открыть Android-эмулятор (требуются Android Studio и SDK).
- Нажмите `w`, чтобы открыть веб-сборку в браузере.

### Запуск в Web

Поскольку проект использует некоторые **специфичные для React Native** библиотеки (например, `@aws-amplify/ui-react-native`), вам может потребоваться условно обрабатывать такие импорты, если при бандлинге для web возникает ошибка. Во многих случаях **web** работает «из коробки». Если проблемы есть, можно:

- Удалить или заменить импорты, которые используются только в нативной среде, или
- Пропустить сборку web и продолжить работу на нативных платформах.

## Примечания по конфигурации ⚙️

### Обязательный сгенерированный файл: `src/aws-exports.js`

`app/_layout.js` импортирует `../src/aws-exports`, но этот файл генерируется Amplify и не коммитится в репозиторий. После `amplify init` + `amplify push` его нужно сгенерировать.

### Конфигурация backend Amplify

В `amplify/backend/backend-config.json` указано, что проект включает:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Дополнительная деталь по авторизации из репозитория:

- Основной режим авторизации AppSync сейчас — `API_KEY`, с AWS IAM как дополнительным провайдером.

### GraphQL-модель данных

Определено в `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- Модель `User` с полями профиля (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- Модель `Post` с полями `text`, необязательный `image`, `likes` и индекс `userID` (`byUser`)

### Настройка Expo/Babel

- `index.js` подгружает polyfill для async iterator и `expo-router/entry`.
- `babel.config.js` включает:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## Примеры использования 🧪

### Создание и публикация поста

1. Откройте приложение и войдите.
2. На главной нажмите `New post`.
3. Введите текст поста.
4. При необходимости выберите изображение из библиотеки.
5. Нажмите `Post`, чтобы загрузить изображение и сохранить запись `Post`.

### Типичный локальный backend-workflow

```bash
amplify status
amplify pull
amplify push
```

Если вы меняете schema/models, при необходимости пересоздайте артефакты командами Amplify CLI в вашей среде.

## Заметки по разработке 🛠️

- Маршрутизация в `app/` реализована file-based через `expo-router`.
- Текущая версия приложения сочетает `DataStore` и прямые мутации `API.graphql`.
- При `signIn` в `_layout.js` через `Hub` отслеживается событие входа и выполняется попытка создать соответствующую запись `User`.
- В `package.json` пока не определены отдельные скрипты `test` или `lint`.
- Каталог `i18n/` существует; файлы README на разных языках запланированы, но на этом шаге не добавлены.
- Ссылки на языки намеренно оставлены в одной строке в начале этого README.

## Устранение неполадок 🧯

### `Cannot find module '../src/aws-exports'`

Выполните:

```bash
amplify init
amplify push
```

Убедитесь, что `src/aws-exports.js` сгенерирован локально.

### Аутентификация проходит, но лента пользователя пуста

- Проверьте, что обработчик входа `Hub` отработал и мутация создания пользователя успешно завершилась.
- Проверьте режим авторизации AppSync и разрешения.
- Проверьте данные в консоли DynamoDB/AppSync для записей `User`.

### Ошибка загрузки изображения при создании поста

- Убедитесь, что в бэкенде Amplify есть ресурс S3.
- Проверьте, что у авторизованного пользователя есть разрешения на загрузку.
- Проверьте сетевое подключение и повторите после повторного входа.

### Ошибки сборки web из-за нативных импортов

Условно импортируйте модули, которые работают только в нативной среде, или сосредоточьтесь на iOS/Android, если с web есть проблемы совместимости.

## Дорожная карта / Далее 🧭

- **Интеграция ИИ**: Добавить endpoints или вызовы сторонних API (например, OpenAI), чтобы поддерживать автоматическую генерацию контента, анализ музыкальных аккордов или переводы.
- **Монетизация**: Добавить функции подписки или платежей (например, Stripe), если вам нужна реализация монетизируемых функций.
- **Деплоймент**: Использовать [EAS Build](https://docs.expo.dev/eas/) или аналогичные сервисы для генерации standalone-приложений для iOS и Android.
- Расширить набор i18n README в `i18n/`, используя ссылки на языки в верхней части файла.

## Благодарности 🙌

- Исходный проект от [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Адаптирован и переименован в **OnlyIdeas**, ориентирован на помощь людям в обмене и монетизации идей, с планируемой интеграцией ИИ для музыки, машинного перевода и исследовательского сотрудничества.

Для получения дополнительных деталей о исходной кодовой базе и возможностях проверьте README в оригинальном репозитории.

## Участие 🤝

Вклад приветствуется. Пока не добавлен отдельный файл `CONTRIBUTING.md`, используйте этот лёгкий процесс:

1. Сделайте fork репозитория.
2. Создайте feature branch.
3. Держите изменения сфокусированными и тестируйте хотя бы на одной платформе.
4. Откройте pull request с чёткими инструкциями по настройке/воспроизведению.

Если вы меняете ресурсы Amplify, добавьте соответствующие изменения `amplify/` и заметки по миграции в описание PR.

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## License 📄

В текущем репозитории сейчас отсутствует файл `LICENSE`.

Предполагается, что все права защищены по умолчанию, пока поддерживающие лица не добавят явную лицензию.

---

Наслаждайтесь разработкой **OnlyIdeas** и адаптируйте платформу под защиту и монетизацию пользовательских идей с помощью ИИ.
