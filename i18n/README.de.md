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

**OnlyIdeas** ist eine Full-Stack-Anwendung, die Menschen dabei unterstützt, ihre Ideen zu teilen und zu monetarisieren. Sie integriert **AWS Amplify** für Benutzerauthentifizierung, Datenspeicherung (AppSync & DynamoDB) und Datei-Hosting (S3). Du kannst dieses Projekt über **Expo** auf **iOS**, **Android** und **Web** ausführen.

Inspiriert von „OnlyFans-ähnlichen“ Funktionen zielt OnlyIdeas außerdem darauf ab, KI-Tools zur Generierung, Analyse und Übersetzung von von Nutzer:innen beigetragenen Ideen, Musik oder Medien zu integrieren.

Diese README ist ein erweiterter, repository-genauer Entwurf auf Basis der bestehenden README-Inhalte und der aktuellen Quelldateien.

## Überblick 📌

### Stack auf einen Blick

| Bereich | Technologie |
|---|---|
| App-Framework | `React Native` + `Expo` |
| Navigation | `expo-router` |
| Auth + Daten + Storage | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Datenbank | `Amazon DynamoDB` (über Amplify GraphQL-Modelle) |
| Dateispeicher | `Amazon S3` |
| Zielplattformen | iOS, Android, Web |

OnlyIdeas verwendet:

- `expo-router` für Navigation und routenbasierte Screens.
- `aws-amplify` + `@aws-amplify/ui-react-native` für Auth, API, DataStore und Storage.
- Amplify-Backend-Kategorien für **Auth (Cognito)**, **API (AppSync GraphQL)** und **Storage (S3)**.

Aktueller User-Flow:

1. Anmelden über Amplify Authenticator.
2. Der Home-Feed listet Creator (`User`-Einträge).
3. Creator-Profil öffnen und Posts/Paywall-Status ansehen.
4. Einen neuen Post erstellen, optional mit Bild-Upload nach S3.

## Funktionen ✨

- Creator-Übersicht und Profilseiten.
- Sign in / sign out mit Amplify UI Authenticator.
- Erstellung neuer Posts mit Image-Picker-Integration.
- S3-Bildupload und Abruf von Bildern.
- GraphQL-gestützte Persistenz der Modelle `User` und `Post`.
- iOS-, Android- und Web-Startziele aus einem einzigen Expo-Projekt.

## Projektstruktur 🗂️

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

## Voraussetzungen ✅

- Node.js 18+ empfohlen.
- npm (Lockfile ist `package-lock.json`).
- Expo-kompatible Tooling:
  - iOS Simulator + Xcode (für lokale iOS-Simulation).
  - Android Studio + SDK/Emulator (für lokale Android-Simulation).
- AWS-Kontozugriff für Amplify-Provisionierung.
- Amplify CLI für Backend-Setup.

## Installation 🚀

### 1. Repository klonen

Beibehaltung des bestehenden kanonischen Befehls:

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

Repository-genaues Remote, das aktuell in diesem Repo konfiguriert ist:

```bash
git clone git@github.com:lachlanchen/onlyideas-react-native.git
cd onlyideas-react-native
```

Dieses Repository ist speziell auf die **OnlyIdeas**-Plattform zugeschnitten und fokussiert sich auf Kreativität und Monetarisierung.

### 2. Abhängigkeiten installieren

Führe im Projekt-Root aus:

```bash
npm install
```

Dadurch werden die erforderlichen Node-Module installiert, einschließlich **Expo**, **React Native** und **aws-amplify**.

## AWS Amplify konfigurieren und initialisieren ☁️

1. **Amplify CLI installieren** (falls noch nicht vorhanden):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Amplify konfigurieren** mit deinen AWS-Zugangsdaten:

   ```bash
   amplify configure
   ```

   - In der AWS-Konsole anmelden und einen vorhandenen IAM-User verwenden oder neu erstellen.
   - `accessKeyId` und `secretAccessKey` angeben.
   - Das neue Profil benennen (z. B. `onlyideas`).

3. **Amplify initialisieren** in diesem Projekt:

   ```bash
   amplify init
   ```

   Empfohlene Eingaben:

   - Environment-Name: `dev` (oder nach Wahl)
   - Standard-Editor: nach Wahl
   - Authentifizierungsmethode: `AWS profile`
   - Profil: das gerade konfigurierte auswählen

4. **Amplify-Backend deployen**:

   ```bash
   amplify push
   ```

Damit wird das AWS-Backend (Cognito, AppSync, S3 usw.) für OnlyIdeas bereitgestellt.

## App starten ▶️

Verwende **Expo**, um die App auf verschiedenen Plattformen zu starten:

```bash
npx expo start
```

Oder über Package-Skripte:

| Skript | Befehl | Zweck |
|---|---|---|
| `npm start` | `expo start` | Expo-Dev-Server starten |
| `npm run ios` | `expo start --ios` | iOS-Simulator starten |
| `npm run android` | `expo start --android` | Android-Emulator starten |
| `npm run web` | `expo start --web` | Web-Ziel ausführen |

- Drücke `i`, um den iOS Simulator zu öffnen (macOS + Xcode erforderlich).
- Drücke `a`, um einen Android-Emulator zu öffnen (Android Studio & SDK erforderlich).
- Drücke `w`, um den Web-Build im Browser zu öffnen.

### Ausführung im Web

Da dieses Projekt einige **React Native**-spezifische Bibliotheken nutzt (z. B. `@aws-amplify/ui-react-native`), musst du diese Imports für Web-Bundles ggf. bedingt behandeln, wenn ein Fehler auftritt. In vielen Fällen funktioniert **web** sofort. Falls Probleme auftreten, entweder:

- Imports entfernen oder ersetzen, die rein nativ sind, oder
- den Web-Build auslassen und auf nativen Plattformen weiterentwickeln.

## Konfigurationshinweise ⚙️

### Erforderliche generierte Datei: `src/aws-exports.js`

`app/_layout.js` importiert `../src/aws-exports`, aber diese Datei wird von Amplify generiert und ist in diesem Repository nicht eingecheckt. Das Ausführen von `amplify init` + `amplify push` sollte sie erzeugen.

### Amplify-Backend-Struktur

Aus `amplify/backend/backend-config.json` geht hervor, dass dieses Projekt Folgendes enthält:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Zusätzlicher repository-genauer Auth-Detailhinweis:

- Die standardmäßige AppSync-Authentifizierung ist derzeit `API_KEY`, mit AWS IAM als zusätzlichem Provider.

### GraphQL-Datenmodell

Definiert in `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- `User`-Modell mit Profilfeldern (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- `Post`-Modell mit `text`, optionalem `image`, `likes` und `userID`-Index (`byUser`)

### Expo/Babel-Setup

- `index.js` lädt das Async-Iterator-Polyfill und `expo-router/entry`.
- `babel.config.js` enthält:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## Nutzungsbeispiele 🧪

### Einen Post erstellen und veröffentlichen

1. App öffnen und anmelden.
2. Auf dem Home-Screen `New post` antippen.
3. Post-Text eingeben.
4. Optional ein Bild aus der Mediathek auswählen.
5. Auf `Post` tippen, um das Bild hochzuladen und den `Post`-Eintrag zu speichern.

### Lokaler Backend-Workflow (typisch)

```bash
amplify status
amplify pull
amplify push
```

Wenn du Schema/Modelle änderst, generiere Artefakte nach Bedarf mit Amplify-CLI-Befehlen in deiner Umgebung neu.

## Entwicklungsnotizen 🛠️

- Routing ist dateibasiert über `expo-router` unter `app/`.
- Die aktuelle App mischt `DataStore` und direkte `API.graphql`-Mutation-Nutzung.
- Bei Auth-`signIn` lauscht `_layout.js` über `Hub` und versucht, einen passenden `User`-Eintrag zu erstellen.
- In `package.json` sind derzeit keine dedizierten `test`- oder `lint`-Skripte definiert.
- Das Verzeichnis `i18n/` existiert; sprachspezifische README-Dateien sind in diesem Entwurfsschritt geplant, aber noch nicht hinzugefügt.
- Sprachlinks werden absichtlich als eine einzelne Optionszeile am Anfang dieser README gehalten.

## Fehlerbehebung 🧯

### `Cannot find module '../src/aws-exports'`

Ausführen:

```bash
amplify init
amplify push
```

Stelle sicher, dass `src/aws-exports.js` lokal generiert wurde.

### Auth funktioniert, aber der User-Feed ist leer

- Prüfen, ob der `Hub`-Sign-in-Listener ausgeführt wurde und die User-Erstellungs-Mutation erfolgreich war.
- AppSync-Auth-Modus und Berechtigungen prüfen.
- Daten in der DynamoDB-/AppSync-Konsole für `User`-Einträge verifizieren.

### Bildupload bei neuem Post schlägt fehl

- Sicherstellen, dass die S3-Storage-Ressource im Amplify-Backend existiert.
- Prüfen, ob der authentifizierte User Upload-Berechtigung hat.
- Netzwerkzugang prüfen und nach erneuter Authentifizierung erneut versuchen.

### Web-Build-Fehler mit nur-nativen Imports

Nur-native Module bedingt importieren oder bei Web-Kompatibilitätsproblemen auf iOS/Android fokussieren.

## Roadmap / Nächste Schritte 🧭

- **KI-Integration**: Endpunkte oder Drittanbieter-API-Aufrufe (z. B. OpenAI) hinzufügen, um automatische Inhaltserstellung, Musikakkord-Analyse oder Übersetzungen zu unterstützen.
- **Monetarisierung**: Abo- oder Zahlungsfunktionen (z. B. Stripe) integrieren, falls monetarisierte Features nachgebildet werden sollen.
- **Deployment**: [EAS Build](https://docs.expo.dev/eas/) oder Ähnliches verwenden, um eigenständige Apps für iOS & Android zu erzeugen.
- Das i18n-README-Set unter `i18n/` mithilfe der Sprachlinks am Anfang dieser Datei erweitern.

## Danksagung 🙌

- Ursprüngliches Projekt von [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Angepasst und als **OnlyIdeas** neu gebrandet, mit Fokus darauf, Menschen beim Teilen und Monetarisieren ihrer Ideen zu unterstützen, mit geplanten KI-Funktionen für Musik, Sprachübersetzung und Forschungszusammenarbeit.

Für zusätzliche Details zur ursprünglichen Codebasis und ihren Features siehe die README im Original-Repository.

## Mitwirken 🤝

Beiträge sind willkommen. Bis eine eigene `CONTRIBUTING.md` ergänzt wird, folge bitte diesem schlanken Ablauf:

1. Fork des Repos erstellen.
2. Einen Feature-Branch anlegen.
3. Änderungen fokussiert halten und auf mindestens einer Zielplattform testen.
4. Einen Pull Request mit klaren Setup-/Reproduktionshinweisen öffnen.

Wenn du Amplify-Ressourcen änderst, nimm die entsprechenden `amplify/`-Updates und Migrationshinweise in die PR-Beschreibung auf.

## Lizenz 📄

Derzeit ist in diesem Repository keine `LICENSE`-Datei vorhanden.

Annahme: Standardmäßig sind alle Rechte vorbehalten, solange/bis von den Maintainern keine explizite Lizenz hinzugefügt wird.

---

Viel Erfolg beim Bauen von **OnlyIdeas**. Passe die Plattform gern so an, dass Nutzerideen mit KI-Unterstützung geschützt und profitabel genutzt werden können.
