

# OnlyIdeas Full Stack App

**OnlyIdeas** is a full-stack application that helps people share and monetize their ideas. It integrates with **AWS Amplify** for user authentication, data storage (AppSync & DynamoDB), and file hosting (S3). You can run this project on **iOS**, **Android**, and **Web** via **Expo**.

Inspired by “OnlyFans-style” features, OnlyIdeas also aims to integrate AI tools for generating, analyzing, and translating user-contributed ideas, music, or media.

---

## 1. Clone the Repo

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

This repository is tailored specifically for the **OnlyIdeas** platform, focusing on creativity and monetization.

---

## 2. Install Dependencies

From the project root, run:

```bash
npm install
```

This installs the necessary Node modules, including **Expo**, **React Native**, and **aws-amplify**.

---

## 3. Configure & Initialize AWS Amplify

1. **Install Amplify CLI** (if you haven’t already):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Configure Amplify** with your AWS credentials:

   ```bash
   amplify configure
   ```

   - Sign in to the AWS console, create or use an existing IAM user.
   - Provide the **accessKeyId** and **secretAccessKey**.
   - Name the new profile (e.g., `onlyideas`).

3. **Initialize Amplify** in this project:

   ```bash
   amplify init
   ```

   - Environment name: `dev` (or your choice)
   - Default editor: your choice
   - Authentication method: “AWS profile”
   - Profile: select the one you just configured

4. **Push Amplify backend**:

   ```bash
   amplify push
   ```

This provisions the AWS backend (Cognito, AppSync, S3, etc.) for OnlyIdeas.

---

## 4. Running on iOS, Android, and Web

Use **Expo** to launch your app on different platforms:

```bash
npx expo start
```

- Press **`i`** to open the iOS Simulator (macOS + Xcode required).  
- Press **`a`** to open an Android emulator (requires Android Studio & SDK).  
- Press **`w`** to open the **web** build in your browser.  

### Running on Web

Because this project uses some **React Native**-specific libraries (e.g., `@aws-amplify/ui-react-native`), you might need to conditionally handle those imports if you see an error while bundling for web. In many cases, **web** will just work out of the box. If you encounter issues, either:

- Remove or replace imports that are purely native, **or**
- Skip the web build and continue using native platforms.

---

## 5. Acknowledgments

- Original project by [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).  
- Adapted and rebranded as **OnlyIdeas**, focusing on helping people share and monetize their ideas, with planned AI features for music, language translation, and research collaboration.

For additional details on the original codebase and features, check the **README** in the original repository.

---

## 6. Next Steps

- **AI Integration**: Add endpoints or third-party API calls (e.g., OpenAI) to support automated content generation, music chord analysis, or translations.  
- **Monetization**: Incorporate subscription or payment features (e.g., Stripe) if you want to replicate monetized features.  
- **Deployment**: Use [EAS Build](https://docs.expo.dev/eas/) or similar to generate standalone apps for iOS & Android.

Enjoy building **OnlyIdeas**, and feel free to tailor the platform to protect and profit from user ideas with AI assistance!
=======
# onlyideas
OnlyIdeas.Art
