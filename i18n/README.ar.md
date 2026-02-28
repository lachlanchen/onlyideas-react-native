[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# تطبيق OnlyIdeas المتكامل (Full Stack)

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20Android%20%7C%20Web-2ea44f)
![Expo](https://img.shields.io/badge/Expo-48-000020?logo=expo)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61dafb?logo=react)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-orange?logo=amazon-aws)
![Backend](https://img.shields.io/badge/Backend-AppSync%20%2B%20DynamoDB-ff9900)
![Storage](https://img.shields.io/badge/Storage-S3-569A31)
![Auth](https://img.shields.io/badge/Auth-Cognito-DD344C)
![License](https://img.shields.io/badge/License-Not%20Specified-lightgrey)

**OnlyIdeas** هو تطبيق متكامل (Full Stack) يساعد الأشخاص على مشاركة أفكارهم وتحقيق الدخل منها. يتكامل مع **AWS Amplify** لمصادقة المستخدمين، وتخزين البيانات (AppSync و DynamoDB)، واستضافة الملفات (S3). يمكنك تشغيل هذا المشروع على **iOS** و **Android** و **Web** عبر **Expo**.

استلهامًا من ميزات على نمط “OnlyFans-style”، يهدف OnlyIdeas أيضًا إلى دمج أدوات الذكاء الاصطناعي لتوليد أفكار المستخدمين أو الموسيقى أو الوسائط التي يساهمون بها، وتحليلها وترجمتها.

هذا README هو مسودة موسعة ودقيقة بالنسبة للمستودع، مبنية على محتوى README الحالي وملفات المصدر الحالية.

## نظرة عامة 📌

### لمحة سريعة عن التقنيات

| المجال | التقنية |
|---|---|
| إطار التطبيق | `React Native` + `Expo` |
| التنقل | `expo-router` |
| المصادقة + البيانات + التخزين | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| قاعدة البيانات | `Amazon DynamoDB` (عبر نماذج Amplify GraphQL) |
| تخزين الملفات | `Amazon S3` |
| المنصات المستهدفة | iOS, Android, Web |

يستخدم OnlyIdeas:

- `expo-router` للتنقل والشاشات المعتمدة على المسارات.
- `aws-amplify` + `@aws-amplify/ui-react-native` للمصادقة، وواجهة API، وDataStore، والتخزين.
- فئات Amplify الخلفية لكل من **Auth (Cognito)** و **API (AppSync GraphQL)** و **Storage (S3)**.

تدفق المستخدم الحالي:

1. تسجيل الدخول عبر Amplify Authenticator.
2. تعرض الصفحة الرئيسية قائمة المبدعين (سجلات `User`).
3. فتح ملف منشئ ومشاهدة المنشورات وحالة حائط الدفع.
4. إنشاء منشور جديد مع رفع صورة اختياري إلى S3.

## الميزات ✨

- صفحات عرض المبدعين والملفات الشخصية.
- تسجيل الدخول / تسجيل الخروج باستخدام Amplify UI Authenticator.
- إنشاء منشور جديد مع تكامل منتقي الصور.
- رفع الصور إلى S3 واسترجاعها.
- حفظ نماذج `User` و `Post` المدعومة بـ GraphQL.
- التشغيل على iOS وAndroid وWeb من مشروع Expo واحد.

## بنية المشروع 🗂️

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

## المتطلبات المسبقة ✅

- يُنصح باستخدام Node.js 18+.
- npm (ملف القفل هو `package-lock.json`).
- أدوات متوافقة مع Expo:
  - iOS Simulator + Xcode (لمحاكاة iOS محليًا).
  - Android Studio + SDK/emulator (لمحاكاة Android محليًا).
- وصول إلى حساب AWS لتجهيز موارد Amplify.
- Amplify CLI لإعداد الخلفية.

## التثبيت 🚀

### 1. استنساخ المستودع

مع الحفاظ على الأمر الأساسي الحالي كما هو:

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

المستودع الفعلي المضبوط حاليًا لهذا المشروع:

```bash
git clone git@github.com:lachlanchen/onlyideas-react-native.git
cd onlyideas-react-native
```

تم تخصيص هذا المستودع تحديدًا لمنصة **OnlyIdeas** مع التركيز على الإبداع وتحقيق الدخل.

### 2. تثبيت الاعتماديات

من جذر المشروع، شغّل:

```bash
npm install
```

سيؤدي هذا إلى تثبيت وحدات Node المطلوبة، بما في ذلك **Expo** و **React Native** و **aws-amplify**.

## إعداد وتهيئة AWS Amplify ☁️

1. **تثبيت Amplify CLI** (إذا لم تثبّته مسبقًا):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **إعداد Amplify** باستخدام بيانات اعتماد AWS الخاصة بك:

   ```bash
   amplify configure
   ```

   - سجّل الدخول إلى AWS console، وأنشئ مستخدم IAM أو استخدم مستخدمًا موجودًا.
   - قدّم `accessKeyId` و `secretAccessKey`.
   - سمِّ الملف الشخصي الجديد (مثلًا: `onlyideas`).

3. **تهيئة Amplify** داخل هذا المشروع:

   ```bash
   amplify init
   ```

   خيارات موصى بها أثناء الأسئلة:

   - اسم البيئة: `dev` (أو ما تختاره)
   - المحرر الافتراضي: حسب اختيارك
   - طريقة المصادقة: `AWS profile`
   - الملف الشخصي: اختر الذي أعددته للتو

4. **دفع موارد Amplify الخلفية**:

   ```bash
   amplify push
   ```

هذا يجهّز البنية الخلفية على AWS (Cognito وAppSync وS3 وغيرها) لـ OnlyIdeas.

## تشغيل التطبيق ▶️

استخدم **Expo** لتشغيل التطبيق على منصات مختلفة:

```bash
npx expo start
```

أو عبر سكربتات الحزمة:

| Script | Command | Purpose |
|---|---|---|
| `npm start` | `expo start` | Start Expo dev server |
| `npm run ios` | `expo start --ios` | Launch iOS simulator |
| `npm run android` | `expo start --android` | Launch Android emulator |
| `npm run web` | `expo start --web` | Run web target |

- اضغط `i` لفتح iOS Simulator (يتطلب macOS + Xcode).
- اضغط `a` لفتح Android emulator (يتطلب Android Studio وSDK).
- اضغط `w` لفتح نسخة الويب في المتصفح.

### التشغيل على الويب

لأن هذا المشروع يستخدم بعض المكتبات الخاصة بـ **React Native** (مثل `@aws-amplify/ui-react-native`)، قد تحتاج إلى التعامل الشرطي مع هذه الاستيرادات إذا ظهر خطأ أثناء bundling للويب. في كثير من الحالات سيعمل **web** مباشرة. إذا واجهت مشاكل، يمكنك:

- إزالة الاستيرادات الأصلية البحتة أو استبدالها، أو
- تجاوز نسخة الويب ومتابعة التطوير على المنصات الأصلية.

## ملاحظات الإعداد ⚙️

### ملف مولّد مطلوب: `src/aws-exports.js`

يقوم `app/_layout.js` باستيراد `../src/aws-exports`، لكن هذا الملف يتم توليده بواسطة Amplify وغير محفوظ في هذا المستودع. تشغيل `amplify init` + `amplify push` يجب أن يولّده.

### شكل البنية الخلفية في Amplify

استنادًا إلى `amplify/backend/backend-config.json`، يتضمن هذا المشروع:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

تفصيل إضافي دقيق حول المصادقة:

- وضع المصادقة الافتراضي في AppSync هو حاليًا `API_KEY` مع AWS IAM كمزوّد إضافي.

### نموذج بيانات GraphQL

مُعرّف في `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- نموذج `User` مع حقول الملف الشخصي (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- نموذج `Post` مع `text`، و`image` اختياري، و`likes`، وفهرس `userID` (`byUser`)

### إعداد Expo/Babel

- `index.js` يقوم بتحميل async iterator polyfill و`expo-router/entry`.
- `babel.config.js` يتضمن:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## أمثلة الاستخدام 🧪

### إنشاء منشور ونشره

1. افتح التطبيق وسجّل الدخول.
2. اضغط `New post` في الشاشة الرئيسية.
3. أدخل نص المنشور.
4. اختياريًا، اختر صورة من المكتبة.
5. اضغط `Post` لرفع الصورة وحفظ سجل `Post`.

### سير عمل الخلفية المحلية (شائع)

```bash
amplify status
amplify pull
amplify push
```

إذا عدّلت schema/models، أعد توليد الملفات الناتجة حسب الحاجة باستخدام أوامر Amplify CLI في بيئتك.

## ملاحظات التطوير 🛠️

- التوجيه معتمد على الملفات عبر `expo-router` داخل `app/`.
- التطبيق الحالي يمزج بين `DataStore` واستخدام مباشر لطفرات `API.graphql`.
- عند حدث `signIn`، يستمع `_layout.js` عبر `Hub` ويحاول إنشاء سجل `User` مطابق.
- لا توجد حاليًا سكربتات `test` أو `lint` مخصصة في `package.json`.
- مجلد `i18n/` موجود؛ وملفات README اللغوية مخططة لكنها غير مضافة بعد في هذه المسودة.
- روابط اللغات محفوظة عمدًا كسطر خيارات واحد أعلى هذا README.

## استكشاف الأخطاء وإصلاحها 🧯

### `Cannot find module '../src/aws-exports'`

شغّل:

```bash
amplify init
amplify push
```

تأكد من توليد `src/aws-exports.js` محليًا.

### نجاح المصادقة لكن خلاصة المستخدمين فارغة

- تأكد من تنفيذ مستمع `Hub` لحدث تسجيل الدخول ونجاح طفرة إنشاء المستخدم.
- تحقق من وضع المصادقة والصلاحيات في AppSync.
- راجع البيانات في DynamoDB/AppSync console لسجلات `User`.

### فشل رفع الصور عند إنشاء منشور جديد

- تأكد من وجود مورد تخزين S3 في Amplify backend.
- تحقق أن المستخدم الموثق لديه صلاحية الرفع.
- تحقق من اتصال الشبكة وأعد المحاولة بعد إعادة المصادقة.

### أخطاء بناء الويب بسبب استيرادات أصلية فقط

استخدم استيرادًا شرطيًا للوحدات الأصلية فقط، أو ركّز على iOS/Android أثناء التطوير إذا تعطلت توافقية الويب.

## خارطة الطريق / الخطوات القادمة 🧭

- **دمج الذكاء الاصطناعي**: إضافة endpoints أو استدعاءات API خارجية (مثل OpenAI) لدعم توليد المحتوى تلقائيًا، أو تحليل أكوردات الموسيقى، أو الترجمة.
- **تحقيق الدخل**: إدراج ميزات الاشتراك أو الدفع (مثل Stripe) إذا أردت محاكاة ميزات مدفوعة.
- **النشر**: استخدم [EAS Build](https://docs.expo.dev/eas/) أو ما يشابهه لإنتاج تطبيقات مستقلة لنظامي iOS وAndroid.
- توسيع مجموعة README متعددة اللغات تحت `i18n/` باستخدام روابط اللغات أعلى هذا الملف.

## شكر وتقدير 🙌

- المشروع الأصلي من [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- تم تكييفه وإعادة تسميته إلى **OnlyIdeas** مع التركيز على مساعدة الناس في مشاركة أفكارهم وتحقيق الربح منها، مع ميزات ذكاء اصطناعي مخطط لها للموسيقى وترجمة اللغات والتعاون البحثي.

لمزيد من التفاصيل حول قاعدة الشيفرة الأصلية وميزاتها، راجع README في المستودع الأصلي.

## المساهمة 🤝

المساهمات مرحّب بها. إلى أن تتم إضافة ملف `CONTRIBUTING.md` مخصص، يرجى اتباع هذا التدفق الخفيف:

1. اعمل Fork للمستودع.
2. أنشئ فرعًا لميزة جديدة.
3. أبقِ التعديلات مركزة واختبر على منصة مستهدفة واحدة على الأقل.
4. افتح Pull Request مع ملاحظات إعداد/إعادة إنتاج واضحة.

إذا كنت تغيّر موارد Amplify، أدرج تحديثات `amplify/` المقابلة وملاحظات الترحيل في وصف الـ PR.

## الترخيص 📄

لا يوجد ملف `LICENSE` حاليًا في هذا المستودع.

افتراض: جميع الحقوق محفوظة افتراضيًا ما لم/إلى أن يضيف المشرفون ترخيصًا صريحًا.

---

استمتع ببناء **OnlyIdeas**، ويمكنك تخصيص المنصة لحماية أفكار المستخدمين وتحقيق الربح منها بمساعدة الذكاء الاصطناعي.
