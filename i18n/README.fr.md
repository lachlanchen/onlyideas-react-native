[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Application Full Stack OnlyIdeas

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20Android%20%7C%20Web-2ea44f)
![Expo](https://img.shields.io/badge/Expo-48-000020?logo=expo)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61dafb?logo=react)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-orange?logo=amazon-aws)
![Backend](https://img.shields.io/badge/Backend-AppSync%20%2B%20DynamoDB-ff9900)
![Storage](https://img.shields.io/badge/Storage-S3-569A31)
![Auth](https://img.shields.io/badge/Auth-Cognito-DD344C)
![License](https://img.shields.io/badge/License-Not%20Specified-lightgrey)

**OnlyIdeas** est une application full stack qui aide les personnes à partager et monétiser leurs idées. Elle s’intègre à **AWS Amplify** pour l’authentification des utilisateurs, le stockage des données (AppSync & DynamoDB) et l’hébergement de fichiers (S3). Vous pouvez exécuter ce projet sur **iOS**, **Android** et **Web** via **Expo**.

Inspiré de fonctionnalités de type « OnlyFans », OnlyIdeas vise aussi à intégrer des outils IA pour générer, analyser et traduire des idées, de la musique ou des médias fournis par les utilisateurs.

Ce README est une version enrichie et fidèle au dépôt, basée sur le contenu README existant et les fichiers sources actuels.

## Vue d’ensemble 📌

### Stack en un coup d’œil

| Domaine | Technologie |
|---|---|
| Framework app | `React Native` + `Expo` |
| Navigation | `expo-router` |
| Auth + Data + Storage | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Base de données | `Amazon DynamoDB` (via les modèles GraphQL Amplify) |
| Stockage de fichiers | `Amazon S3` |
| Cibles | iOS, Android, Web |

OnlyIdeas utilise :

- `expo-router` pour la navigation et les écrans basés sur les routes.
- `aws-amplify` + `@aws-amplify/ui-react-native` pour l’auth, l’API, DataStore et le stockage.
- Les catégories backend Amplify pour **Auth (Cognito)**, **API (AppSync GraphQL)** et **Storage (S3)**.

Flux utilisateur actuel :

1. Connexion via Amplify Authenticator.
2. Le flux d’accueil liste les créateurs (enregistrements `User`).
3. Ouverture d’un profil créateur et affichage des publications/état paywall.
4. Création d’une nouvelle publication avec téléversement d’image optionnel vers S3.

## Fonctionnalités ✨

- Liste des créateurs et pages de profil.
- Connexion / déconnexion avec Amplify UI Authenticator.
- Création de nouvelles publications avec intégration du sélecteur d’images.
- Téléversement d’images vers S3 et récupération des images.
- Persistance des modèles `User` et `Post` via GraphQL.
- Cibles iOS, Android et Web depuis un seul projet Expo.

## Structure du projet 🗂️

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

## Prérequis ✅

- Node.js 18+ recommandé.
- npm (le lockfile est `package-lock.json`).
- Outils compatibles Expo :
  - iOS Simulator + Xcode (pour la simulation locale iOS).
  - Android Studio + SDK/émulateur (pour la simulation locale Android).
- Accès à un compte AWS pour le provisionnement Amplify.
- Amplify CLI pour la configuration backend.

## Installation 🚀

### 1. Cloner le dépôt

Conservation de la commande canonique existante :

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

Remote fidèle au dépôt actuellement configuré dans ce repo :

```bash
git clone git@github.com:lachlanchen/onlyideas-react-native.git
cd onlyideas-react-native
```

Ce dépôt est spécifiquement conçu pour la plateforme **OnlyIdeas**, avec un focus sur la créativité et la monétisation.

### 2. Installer les dépendances

Depuis la racine du projet, exécutez :

```bash
npm install
```

Cela installe les modules Node nécessaires, dont **Expo**, **React Native** et **aws-amplify**.

## Configurer et initialiser AWS Amplify ☁️

1. **Installer Amplify CLI** (si ce n’est pas déjà fait) :

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Configurer Amplify** avec vos identifiants AWS :

   ```bash
   amplify configure
   ```

   - Connectez-vous à la console AWS, puis créez ou utilisez un utilisateur IAM existant.
   - Fournissez `accessKeyId` et `secretAccessKey`.
   - Nommez le nouveau profil (ex. `onlyideas`).

3. **Initialiser Amplify** dans ce projet :

   ```bash
   amplify init
   ```

   Réponses recommandées :

   - Nom d’environnement : `dev` (ou votre choix)
   - Éditeur par défaut : votre choix
   - Méthode d’authentification : `AWS profile`
   - Profil : sélectionnez celui que vous venez de configurer

4. **Pousser le backend Amplify** :

   ```bash
   amplify push
   ```

Cela provisionne le backend AWS (Cognito, AppSync, S3, etc.) pour OnlyIdeas.

## Lancer l’application ▶️

Utilisez **Expo** pour lancer votre application sur différentes plateformes :

```bash
npx expo start
```

Ou via les scripts du package :

| Script | Commande | Objectif |
|---|---|---|
| `npm start` | `expo start` | Démarrer le serveur de dev Expo |
| `npm run ios` | `expo start --ios` | Lancer le simulateur iOS |
| `npm run android` | `expo start --android` | Lancer l’émulateur Android |
| `npm run web` | `expo start --web` | Lancer la cible web |

- Appuyez sur `i` pour ouvrir le simulateur iOS (macOS + Xcode requis).
- Appuyez sur `a` pour ouvrir un émulateur Android (Android Studio & SDK requis).
- Appuyez sur `w` pour ouvrir la version web dans votre navigateur.

### Exécution sur le Web

Comme ce projet utilise certaines bibliothèques spécifiques **React Native** (ex. `@aws-amplify/ui-react-native`), il peut être nécessaire de gérer conditionnellement ces imports si vous rencontrez une erreur lors du bundling web. Dans de nombreux cas, la cible **web** fonctionne directement. En cas de problème, vous pouvez :

- Supprimer ou remplacer les imports strictement natifs, ou
- Ignorer la cible web et continuer sur les plateformes natives.

## Notes de configuration ⚙️

### Fichier généré requis : `src/aws-exports.js`

`app/_layout.js` importe `../src/aws-exports`, mais ce fichier est généré par Amplify et n’est pas versionné dans ce dépôt. Exécuter `amplify init` + `amplify push` doit le générer.

### Structure backend Amplify

D’après `amplify/backend/backend-config.json`, ce projet inclut :

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Détail d’auth supplémentaire fidèle au dépôt :

- Le mode d’authentification par défaut AppSync est actuellement `API_KEY` avec AWS IAM comme fournisseur additionnel.

### Modèle de données GraphQL

Défini dans `amplify/backend/api/OnlyFansCloneApp/schema.graphql` :

- Modèle `User` avec champs de profil (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- Modèle `Post` avec `text`, `image` optionnelle, `likes` et index `userID` (`byUser`)

### Configuration Expo/Babel

- `index.js` charge le polyfill async iterator et `expo-router/entry`.
- `babel.config.js` inclut :
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## Exemples d’utilisation 🧪

### Créer et publier une publication

1. Ouvrez l’application et connectez-vous.
2. Appuyez sur `New post` sur l’écran d’accueil.
3. Entrez le texte de la publication.
4. Sélectionnez éventuellement une image depuis la bibliothèque.
5. Appuyez sur `Post` pour téléverser l’image et enregistrer l’enregistrement `Post`.

### Workflow backend local (typique)

```bash
amplify status
amplify pull
amplify push
```

Si vous modifiez le schéma/les modèles, régénérez les artefacts si nécessaire via les commandes Amplify CLI dans votre environnement.

## Notes de développement 🛠️

- Le routage est basé sur les fichiers via `expo-router` sous `app/`.
- L’application actuelle mélange l’usage de `DataStore` et de mutations directes `API.graphql`.
- Lors d’un `signIn`, `_layout.js` écoute via `Hub` et tente de créer un enregistrement `User` correspondant.
- Aucun script `test` ou `lint` dédié n’est actuellement défini dans `package.json`.
- Le répertoire `i18n/` existe ; les fichiers README de langues sont prévus mais pas encore ajoutés dans cette étape de brouillon.
- Les liens de langue sont volontairement conservés sous la forme d’une ligne d’options unique en haut de ce README.

## Dépannage 🧯

### `Cannot find module '../src/aws-exports'`

Exécutez :

```bash
amplify init
amplify push
```

Assurez-vous que `src/aws-exports.js` est bien généré localement.

### L’auth réussit mais le flux utilisateur est vide

- Confirmez que le listener `Hub` sur la connexion s’est exécuté et que la mutation de création utilisateur a réussi.
- Vérifiez le mode d’auth AppSync et les permissions.
- Vérifiez les données dans la console DynamoDB/AppSync pour les enregistrements `User`.

### L’envoi d’image échoue sur une nouvelle publication

- Confirmez que la ressource de stockage S3 existe dans le backend Amplify.
- Vérifiez que l’utilisateur authentifié a la permission de téléverser.
- Vérifiez l’accès réseau et réessayez après ré-authentification.

### Erreurs de build web avec des imports uniquement natifs

Importez conditionnellement les modules natifs uniquement, ou concentrez le développement sur iOS/Android si la compatibilité web casse.

## Feuille de route / Prochaines étapes 🧭

- **Intégration IA** : Ajouter des endpoints ou des appels API tiers (ex. OpenAI) pour prendre en charge la génération automatique de contenu, l’analyse d’accords musicaux ou les traductions.
- **Monétisation** : Intégrer des fonctionnalités d’abonnement ou de paiement (ex. Stripe) si vous souhaitez reproduire des fonctionnalités monétisées.
- **Déploiement** : Utiliser [EAS Build](https://docs.expo.dev/eas/) ou équivalent pour générer des applications autonomes iOS & Android.
- Étendre l’ensemble README i18n sous `i18n/` en utilisant les liens de langue en haut de ce fichier.

## Remerciements 🙌

- Projet original par [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Adapté et rebrandé en **OnlyIdeas**, avec un focus sur l’aide au partage et à la monétisation des idées, et des fonctionnalités IA planifiées pour la musique, la traduction linguistique et la collaboration en recherche.

Pour plus de détails sur le codebase original et ses fonctionnalités, consultez le README du dépôt d’origine.

## Contribution 🤝

Les contributions sont les bienvenues. En attendant l’ajout d’un `CONTRIBUTING.md` dédié, merci de suivre ce flux léger :

1. Forkez le dépôt.
2. Créez une branche de fonctionnalité.
3. Gardez les changements ciblés et testez sur au moins une plateforme cible.
4. Ouvrez une pull request avec des notes claires de configuration/reproduction.

Si vous modifiez des ressources Amplify, incluez les mises à jour `amplify/` correspondantes et les notes de migration dans la description de la PR.

## Licence 📄

Aucun fichier `LICENSE` n’est actuellement présent dans ce dépôt.

Hypothèse : tous droits réservés par défaut tant qu’aucune licence explicite n’est ajoutée par les mainteneurs.

---

Bonne construction avec **OnlyIdeas**, et n’hésitez pas à adapter la plateforme pour protéger et valoriser les idées des utilisateurs avec l’assistance de l’IA.
