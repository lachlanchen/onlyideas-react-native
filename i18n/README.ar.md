[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# تطبيق OnlyIdeas الكامل

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

**OnlyIdeas** هو تطبيق full-stack يساعد المستخدمين على مشاركة أفكارهم وتحويلها إلى مصدر دخل. يدمج **AWS Amplify** للمصادقة، وتخزين البيانات (**AppSync** و **DynamoDB**)، واستضافة الملفات (**S3**). يمكنك تشغيل المشروع على **iOS** و **Android** و **Web** عبر **Expo**.

استلهم المشروع من خصائص بنمط **OnlyFans**، وهدفه أيضًا إدماج أدوات الذكاء الاصطناعي لتوليد وتحليل وترجمة أفكار المستخدمين والموسيقى أو المحتوى الإعلامي.

هذا الملف هو نسخة موسعة ودقيقة للمستودع مبنية على محتوى README الحالي وملفات المصدر الفعلية.

## نظرة عامة 📌

### لمحة سريعة عن التقنيات

| المجال | التقنية |
|---|---|
| إطار العمل | `React Native` + `Expo` |
| التنقل | `expo-router` |
| المصادقة + البيانات + التخزين | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| قاعدة البيانات | `Amazon DynamoDB` (عبر نماذج Amplify GraphQL) |
| تخزين الملفات | `Amazon S3` |
| المنصات المستهدفة | iOS, Android, Web |

يستخدم OnlyIdeas:

- `expo-router` للتنقل بين الشاشات المبنية على المسارات.
- `aws-amplify` + `@aws-amplify/ui-react-native` للمصادقة وواجهة API و`DataStore` والتخزين.
- فئات Amplify الخاصة بـ **Auth (Cognito)** و **API (AppSync GraphQL)** و **Storage (S3)**.

تدفق المستخدم الحالي:

1. تسجيل الدخول عبر `Amplify Authenticator`.
2. تعرض الصفحة الرئيسية خريطة للمستخدمين (مبدعين).
3. فتح ملف المبدع لعرض المنشورات وحالة الحاجز المدفوع.
4. إنشاء منشور جديد مع خيار رفع صورة إلى S3.

## المميزات ✨

- صفحات قوائم المبدعين والملفات الشخصية.
- تسجيل الدخول/الخروج عبر `Amplify UI Authenticator`.
- إنشاء منشور جديد مع دعم اختيار الصورة.
- رفع الصور واسترجاعها من S3.
- تخزين نماذجي `User` و `Post` عبر GraphQL.
- تشغيل iOS وAndroid وWeb من مشروع Expo واحد.

## هيكلة المشروع 🗂️

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

## المتطلبات المبدئية ✅

- يُفضَّل استخدام Node.js 18+.
- npm (ملف التثبيت المقفل هو `package-lock.json`).
- أدوات متوافقة مع Expo:
  - iOS Simulator + Xcode (للتشغيل المحلي على iOS).
  - Android Studio + SDK/emulator (للتشغيل المحلي على Android).
- حساب AWS لإعداد Amplify.
- `Amplify CLI` لإعداد الخلفية.

## التثبيت 🚀

### 1. استنساخ المستودع

استخدم أي remote يناسب سير عملك:

| Command | Notes |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | مرجع تاريخي/أرشيفي |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | المستودع الحالي (موصى به) |

ثم افتح مجلد المشروع الصحيح:

```bash
cd onlyideas-react-native
```

هذا المستودع مخصّص خصيصًا لمنصة **OnlyIdeas** مع تركيز على الإبداع وتحقيق العائد.

### 2. تثبيت الاعتمادات

من جذر المشروع:

```bash
npm install
```

سيتم تثبيت الوحدات الأساسية المطلوبة، بما فيها **Expo** و **React Native** و **aws-amplify**.

## تهيئة وبدء AWS Amplify ☁️

1. **تثبيت Amplify CLI** (إن لم تكن مثبتًا بعد):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **إعداد Amplify** بمفاتيح AWS الخاصة بك:

   ```bash
   amplify configure
   ```

   - سجّل دخولك إلى AWS console وأنشئ أو استخدم مستخدم IAM موجود.
   - وفّر `accessKeyId` و `secretAccessKey`.
   - سمِّ البروفايل الجديد (مثلًا: `onlyideas`).

3. **تهيئة Amplify** داخل هذا المشروع:

   ```bash
   amplify init
   ```

   الإعدادات المقترحة:

   - اسم البيئة: `dev` (أو اختيارك).
   - المحرر الافتراضي: حسب تفضيلك.
   - طريقة المصادقة: `AWS profile`
   - البروفايل: اختر البروفايل الذي أعددته.

4. **رفع backend الخاص بـ Amplify**:

   ```bash
   amplify push
   ```

هذا ينشئ البنية الخلفية على AWS (Cognito وAppSync وS3 وغيرها) لمشروع OnlyIdeas.

## تشغيل التطبيق ▶️

استخدم **Expo** لفتح التطبيق على منصات مختلفة:

```bash
npx expo start
```

أو عبر سكربتات الحزمة:

| Script | Command | Purpose |
|---|---|---|
| `npm start` | `expo start` | بدء سيرفر تطوير Expo |
| `npm run ios` | `expo start --ios` | تشغيل مقلد iOS |
| `npm run android` | `expo start --android` | تشغيل محاكي Android |
| `npm run web` | `expo start --web` | تشغيل هدف الويب |

- اضغط `i` لفتح iOS Simulator (يتطلب macOS + Xcode).
- اضغط `a` لفتح Android emulator (يتطلب Android Studio وSDK).
- اضغط `w` لعرض الويب في المتصفح.

### تشغيل على الويب

بما أن المشروع يستخدم بعض مكتبات **React Native** المتخصصة (مثل `@aws-amplify/ui-react-native`)، قد تحتاج إلى استيرادها بشكل شرطي إذا ظهرت أخطاء أثناء تجميع الويب. في كثير من الحالات يعمل الويب مباشرة، وإن ظهرت مشاكل:

- أزل أو استبدل الاستيرادات الصافية للمنصات الأصلية، أو
- تجاهل تشغيل نسخة الويب وركّز على iOS/Android.

## ملاحظات التهيئة ⚙️

### الملف المولّد المطلوب: `src/aws-exports.js`

`app/_layout.js` يستورد `../src/aws-exports`، لكن هذا الملف يولّده Amplify وليس موجودًا في المستودع. تشغيل `amplify init` + `amplify push` يفترض أن يُنشئه.

### شكل backend في Amplify

حسب `amplify/backend/backend-config.json`، يتضمن هذا المشروع:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

تفصيل مصادقة إضافي:

- وضع مصادقة AppSync الافتراضي هو حاليًا `API_KEY` مع AWS IAM كمزوّد إضافي.

### نموذج بيانات GraphQL

معرّف في `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- نموذج `User` مع حقول الملف الشخصي (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- نموذج `Post` مع `text`, `image` اختياري, `likes`, وفهرس `userID` (`byUser`)

### إعداد Expo/Babel

- `index.js` يحمل polyfill لمؤشر المكرّر غير المتزامن و `expo-router/entry`.
- ملف `babel.config.js` يحتوي على:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## أمثلة الاستخدام 🧪

### إنشاء منشور ونشره

1. افتح التطبيق وسجّل الدخول.
2. اضغط `New post` في الشاشة الرئيسية.
3. اكتب نص المنشور.
4. اختياريًا اختر صورة من المكتبة.
5. اضغط `Post` لرفع الصورة وحفظ سجل `Post`.

### سير عمل backend محلي (نموذجي)

```bash
amplify status
amplify pull
amplify push
```

إذا عدّلت schema/models، أعد توليد المخرجات اللازمة بأوامر Amplify CLI المناسبة في بيئتك.

## ملاحظات التطوير 🛠️

- يعتمد التوجيه على الملفات عبر `expo-router` داخل `app/`.
- التطبيق الحالي يجمع بين `DataStore` واستخدام طفرات `API.graphql` مباشرة.
- عند حدث `signIn`، يراقب `_layout.js` عبر `Hub` ويحاول إنشاء سجل `User` مطابق.
- لا توجد حالياً سكربتات `test` أو `lint` مخصصة في `package.json`.
- مجلد `i18n/` موجود؛ ملفات README بلغات أخرى مخططة ضمن هذه الدفعة.
- روابط اللغات موجودة كسطر خيارات واحد في أعلى هذا الملف.

## استكشاف الأخطاء وإصلاحها 🧯

### `Cannot find module '../src/aws-exports'`

نفّذ:

```bash
amplify init
amplify push
```

تأكد من وجود `src/aws-exports.js` مولّدًا محليًا.

### نجح تسجيل الدخول لكن التغذية فارغة

- تأكد من تشغيل مستمع `Hub` عند تسجيل الدخول وأن طفرة إنشاء المستخدم نجحت.
- راجع وضع مصادقة AppSync والأذونات.
- تحقق من وجود بيانات `User` في واجهات DynamoDB/AppSync.

### فشل رفع الصورة عند إنشاء منشور جديد

- تأكد من وجود مورد تخزين S3 في backend الخاص بـ Amplify.
- تحقق من وجود صلاحية رفع للمستخدم الموثّق.
- تحقق من الشبكة ثم أعد المحاولة بعد إعادة المصادقة.

### أخطاء بناء الويب بسبب استيرادات أصلية فقط

استخدم استيرادًا شرطيًا للوحدات الأصلية فقط، أو ركّز على iOS/Android إذا تعذرت مطابقة الويب.

## خارطة الطريق / الخطوات التالية 🧭

- **دمج الذكاء الاصطناعي**: إضافة نقاط نهاية أو استدعاءات API طرف ثالث (مثل OpenAI) لدعم التوليد الآلي، تحليل الألحان، أو الترجمة.
- **الربحية**: إضافة نظام اشتراك أو دفع (مثل Stripe) إذا كنت تريد خصائص مماثلة للمنتجات المدفوعة.
- **النشر**: استخدام [EAS Build](https://docs.expo.dev/eas/) أو أدوات مشابهة لإنشاء تطبيقات مستقلة لـ iOS وAndroid.
- توسيع ملفات README متعددة اللغات داخل `i18n/` باستخدام روابط اللغات أعلى هذه الصفحة.

## الشكر والتقدير 🙌

- المشروع الأصلي من [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- تمت إعادة التوجيه وإعادة تسمية المشروع إلى **OnlyIdeas** مع تركيز واضح على مشاركة الناس لأفكارهم وتحقيق الدخل منها، مع ميزات ذكاء اصطناعي مخططة للموسيقى وترجمة اللغة والتعاون البحثي.

لمزيد من التفاصيل حول قاعدة الكود الأصلية وميزاتها، راجع README في المستودع الأصلي.

## المساهمة 🤝

المساهمات مرحّب بها. إلى أن يتم إضافة ملف `CONTRIBUTING.md` مخصص، اتبع التسلسل الخفيف التالي:

1. Fork للمستودع.
2. إنشاء فرع للميزة.
3. إبقاء التعديلات مركزة واختبارها على منصة مستهدفة واحدة على الأقل.
4. فتح طلب سحب (Pull Request) مع ملاحظات إعداد/إعادة إنتاج واضحة.

إذا كنت تغيّر موارد Amplify، أدرج تغييرات `amplify/` المقابلة وملاحظات الترحيل داخل وصف PR.

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## License 📄

لا يوجد ملف `LICENSE` حاليًا في هذا المستودع.

الافتراض: جميع الحقوق محفوظة افتراضًا ما لم يتم إضافة ترخيص صريح من قبل المسؤولين.

---

استمتع ببناء **OnlyIdeas**، ويمكنك تخصيص المنصة بحرية لحماية الأفكار وتحقيق الربح منها بمساعدة الذكاء الاصطناعي.
