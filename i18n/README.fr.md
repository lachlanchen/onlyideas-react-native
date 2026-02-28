[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# Application full-stack OnlyIdeas

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

**OnlyIdeas** est une application full-stack qui aide les gens à partager et monétiser leurs idées. Elle s'intègre à **AWS Amplify** pour l'authentification des utilisateurs, le stockage de données (AppSync & DynamoDB) et l'hébergement de fichiers (S3). Vous pouvez exécuter ce projet sur **iOS**, **Android** et **Web** via **Expo**.

Inspiré par des fonctionnalités de type “OnlyFans”, OnlyIdeas vise également à intégrer des outils d’IA pour générer, analyser et traduire les idées, musiques ou contenus médias fournis par les utilisateurs.

Ce README est une version élargie, conforme au dépôt, basée sur le contenu existant et les fichiers source actuels.

## Vue d'ensemble 📌

### Stack en un coup d'œil

| Domaine | Technologie |
|---|---|
| Framework de l'application | `React Native` + `Expo` |
| Navigation | `expo-router` |
| Auth + Données + Stockage | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Base de données | `Amazon DynamoDB` (via les modèles GraphQL d’Amplify) |
| Stockage de fichiers | `Amazon S3` |
| Cibles | iOS, Android, Web |

OnlyIdeas utilise :

- `expo-router` pour la navigation et les écrans basés sur les routes.
- `aws-amplify` + `@aws-amplify/ui-react-native` pour l'authentification, l'API, DataStore et le stockage.
- Les catégories backend d'Amplify pour **Auth (Cognito)**, **API (AppSync GraphQL)** et **Storage (S3)**.

Flux utilisateur actuel :

1. Connexion via l'Authenticator d'Amplify.
2. Le fil d'accueil affiche les créateurs (`enregistrements User`).
3. Ouvrir un profil de créateur et afficher les publications / l'état de paywall.
4. Créer une nouvelle publication avec un téléchargement d'image optionnel vers S3.

## Fonctionnalités ✨

- Pages de listing et de profil de créateurs.
- Connexion / déconnexion avec l'Authenticator d'Amplify UI.
- Création de nouvelles publications avec intégration du sélecteur d'images.
- Téléchargement et récupération d'images S3.
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
├── i18n/                    # Dossier de traduction des README (vide pour l'instant)
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
- Un accès à un compte AWS pour le provisionnement Amplify.
- La CLI Amplify pour la configuration backend.

## Installation 🚀

### 1. Cloner le dépôt

Utilisez le remote qui correspond à votre flux de travail :

| Commande | Notes |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | Référence historique/archivage |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | Dépôt actuel (recommandé) |

Ensuite, ouvrez le bon répertoire de projet :

```bash
cd onlyideas-react-native
```

Ce dépôt est spécifiquement conçu pour la plateforme **OnlyIdeas**, avec un focus sur la créativité et la monétisation.

### 2. Installer les dépendances

À partir de la racine du projet, exécutez :

```bash
npm install
```

Cela installe les modules Node nécessaires, y compris **Expo**, **React Native** et **aws-amplify**.

## Configurer et initialiser AWS Amplify ☁️

1. **Installer la CLI Amplify** (si ce n'est pas déjà fait) :

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Configurer Amplify** avec vos identifiants AWS :

   ```bash
   amplify configure
   ```

   - Connectez-vous à la console AWS, créez ou utilisez un utilisateur IAM existant.
   - Fournissez `accessKeyId` et `secretAccessKey`.
   - Nommez le nouveau profil (ex. : `onlyideas`).

3. **Initialiser Amplify** dans ce projet :

   ```bash
   amplify init
   ```

   Paramètres recommandés :

   - Nom d'environnement : `dev` (ou votre choix)
   - Éditeur par défaut : votre choix
   - Méthode d'authentification : `AWS profile`
   - Profil : sélectionnez celui que vous venez de configurer

4. **Pousser le backend Amplify** :

   ```bash
   amplify push
   ```

Cela provisionne le backend AWS (Cognito, AppSync, S3, etc.) pour OnlyIdeas.

## Lancer l'application ▶️

Utilisez **Expo** pour démarrer votre app sur différentes plateformes :

```bash
npx expo start
```

Ou via les scripts package :

| Script | Commande | Objectif |
|---|---|---|
| `npm start` | `expo start` | Démarrer le serveur de développement Expo |
| `npm run ios` | `expo start --ios` | Lancer le simulateur iOS |
| `npm run android` | `expo start --android` | Lancer l'émulateur Android |
| `npm run web` | `expo start --web` | Exécuter la cible Web |

- Appuyez sur `i` pour ouvrir le simulateur iOS (macOS + Xcode requis).
- Appuyez sur `a` pour ouvrir un émulateur Android (nécessite Android Studio & SDK).
- Appuyez sur `w` pour ouvrir la version web dans votre navigateur.

### Lancer sur le Web

Parce que ce projet utilise quelques librairies spécifiques à **React Native** (ex. `@aws-amplify/ui-react-native`), il peut être nécessaire de gérer ces imports de manière conditionnelle si vous voyez une erreur pendant le bundling pour le web. Dans de nombreux cas, le **web** fonctionne immédiatement. Si vous rencontrez des problèmes, faites l'un des choix suivants :

- Supprimez ou remplacez les imports purement natifs,
- Ou ignorez la build web et continuez avec les plateformes natives.

## Notes de configuration ⚙️

### Fichier généré requis : `src/aws-exports.js`

`app/_layout.js` importe `../src/aws-exports`, mais ce fichier est généré par Amplify et n'est pas commit dans ce dépôt. Exécuter `amplify init` + `amplify push` doit le générer.

### Forme du backend Amplify

Depuis `amplify/backend/backend-config.json`, ce projet inclut :

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Détails d'authentification supplémentaires provenant du dépôt :

- L'authentification par défaut d'AppSync est actuellement `API_KEY` avec AWS IAM en fournisseur additionnel.

### Modèle GraphQL

Défini dans `amplify/backend/api/OnlyFansCloneApp/schema.graphql` :

- Modèle `User` avec des champs de profil (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- Modèle `Post` avec `text`, image optionnelle, `likes` et l'index `userID` (`byUser`)

### Configuration Expo/Babel

- `index.js` charge le polyfill d'async iterator et `expo-router/entry`.
- `babel.config.js` inclut :
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## Exemples d'utilisation 🧪

### Créer et publier une publication

1. Ouvrez l'app et connectez-vous.
2. Appuyez sur `New post` sur l'écran d'accueil.
3. Saisissez le texte de la publication.
4. Optionnellement, sélectionnez une image dans la bibliothèque.
5. Appuyez sur `Post` pour télécharger l'image et enregistrer l'entrée `Post`.

### Flux backend local (typique)

```bash
amplify status
amplify pull
amplify push
```

Si vous modifiez le schéma ou les modèles, régénérez les artefacts selon les besoins avec les commandes Amplify CLI dans votre environnement.

## Notes de développement 🛠️

- La navigation est basée sur les fichiers via `expo-router` sous `app/`.
- L'application combine actuellement `DataStore` et l'utilisation directe des mutations `API.graphql`.
- Lors d'un `signIn` d'authentification, `_layout.js` écoute via `Hub` et tente de créer un enregistrement `User` correspondant.
- Aucune commande dédiée `test` ou `lint` n'est définie actuellement dans `package.json`.
- Le dossier `i18n/` existe ; des fichiers de README par langue sont prévus mais n'étaient pas encore ajoutés dans cette version intermédiaire.
- Les liens de langue sont intentionnellement conservés sous forme d'une seule ligne d'options en haut de ce README.

## Dépannage 🧯

### `Cannot find module '../src/aws-exports'`

Exécutez :

```bash
amplify init
amplify push
```

Vérifiez que `src/aws-exports.js` est généré localement.

### Authentification réussie mais fil utilisateur vide

- Vérifiez que le listener d'authentification `Hub` s'est bien exécuté et que la mutation de création d'utilisateur a réussi.
- Vérifiez le mode d'authentification et les permissions AppSync.
- Vérifiez les données dans la console DynamoDB/AppSync pour les enregistrements `User`.

### Le téléchargement d'image échoue sur une nouvelle publication

- Vérifiez que la ressource de stockage S3 existe bien dans le backend Amplify.
- Vérifiez que l'utilisateur authentifié a la permission de télécharger.
- Contrôlez l'accès réseau puis réessayez après reconnexion.

### Erreurs de build Web liées aux imports uniquement natifs

Importez conditionnellement les modules natifs, ou concentrez-vous sur iOS/Android pour le développement si la compatibilité web se dégrade.

## Feuille de route / Prochaines étapes 🧭

- **Intégration IA** : ajouter des endpoints ou appels d'API tiers (ex. OpenAI) pour la génération automatisée de contenu, l'analyse d'accords musicaux ou les traductions.
- **Monétisation** : intégrer des fonctions d'abonnement ou de paiement (ex. Stripe) si vous souhaitez reproduire des fonctionnalités monétisées.
- **Déploiement** : utiliser [EAS Build](https://docs.expo.dev/eas/) ou un outil similaire pour générer des applications autonomes pour iOS et Android.
- Étendre l'ensemble des README i18n sous `i18n/` en s'appuyant sur les liens de langue en haut de ce fichier.

## Remerciements 🙌

- Projet original de [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Adapté et rebrandé en **OnlyIdeas**, avec pour objectif d'aider les gens à partager et monétiser leurs idées, avec des fonctionnalités IA prévues pour la musique, la traduction de langues et la collaboration de recherche.

Pour plus de détails sur la base de code originale et ses fonctionnalités, consultez le README du dépôt d'origine.

## Contribution 🤝

Les contributions sont les bienvenues. En attendant qu'un fichier `CONTRIBUTING.md` dédié soit ajouté, suivez ce flux léger :

1. Faites un fork du dépôt.
2. Créez une branche de fonctionnalité.
3. Gardez les changements ciblés et testez au moins sur une plateforme.
4. Ouvrez une pull request avec des notes de configuration/reproduction claires.

Si vous modifiez des ressources Amplify, incluez les mises à jour `amplify/` correspondantes et les notes de migration dans la description de la PR.

## Licence 📄

Aucun fichier `LICENSE` n'est actuellement présent dans ce dépôt.

Hypothèse : tous les droits sont réservés par défaut jusqu'à ce qu'une licence explicite soit ajoutée par les mainteneurs.

---

Amusez-vous à développer **OnlyIdeas**, et n'hésitez pas à adapter la plateforme pour protéger et monétiser les idées des utilisateurs avec l'aide de l'IA.


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
