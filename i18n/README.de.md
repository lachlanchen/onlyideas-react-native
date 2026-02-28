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

**OnlyIdeas** ist eine Full-Stack-Anwendung, mit der Menschen ihre Ideen teilen und monetarisieren können. Sie nutzt **AWS Amplify** für Benutzerauthentifizierung, Datenspeicherung (AppSync & DynamoDB) und Datei-Hosting (S3). Du kannst dieses Projekt über **Expo** auf **iOS**, **Android** und **Web** ausführen.

Angeregt von „OnlyFans-ähnlichen“ Funktionen zielt OnlyIdeas außerdem darauf ab, KI-Werkzeuge für die Erstellung, Analyse und Übersetzung von Nutzerideen, Musik oder Medien zu integrieren.

Diese README ist ein erweiterter, repository-konsistenter Entwurf auf Basis des vorhandenen README-Inhalts und der aktuellen Quelldateien.

## Überblick 📌

### Technologiestack auf einen Blick

| Bereich | Technologie |
|---|---|
| App-Framework | `React Native` + `Expo` |
| Navigation | `expo-router` |
| Auth + Daten + Storage | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Datenbank | `Amazon DynamoDB` (via Amplify GraphQL models) |
| Dateispeicherung | `Amazon S3` |
| Ziele | iOS, Android, Web |

OnlyIdeas verwendet:

- `expo-router` für Navigation und route-basierte Screens.
- `aws-amplify` + `@aws-amplify/ui-react-native` für Auth, API, DataStore und Storage.
- Amplify-Backend-Kategorien für **Auth (Cognito)**, **API (AppSync GraphQL)** und **Storage (S3)**.

Aktueller Nutzerfluss:

1. Anmeldung über den Amplify Authenticator.
2. Der Start-Feed listet Ersteller (`User`-Einträge) auf.
3. Öffne ein Erstellerprofil und sieh dir die Posts/Paywall-Status an.
4. Erstelle einen neuen Post mit optionalem Bild-Upload zu S3.

## Funktionen ✨

- Ersteller-Listen und Profilseiten.
- An- und Abmelden mit dem Amplify UI Authenticator.
- Erstellung neuer Beiträge mit Integration eines Bildauswählers.
- S3-Bildupload und Abruf von Bildern.
- GraphQL-basierte Persistenz der Modelle `User` und `Post`.
- iOS-, Android- und Web-Startziele aus einem einzigen Expo-Projekt.

## Projektstruktur 🗂️

```text
.
├── app/
│   ├── _layout.js           # Amplify-Konfiguration + Authenticator-Wrapper
│   ├── index.js             # Start-Feed (Nutzerliste)
│   ├── newPost.js           # Beitrag erstellen + optionaler Bild-Upload
│   └── user/[id].js         # Erstellerprofil + Beiträge
├── src/
│   ├── components/
│   │   ├── UserCard.js
│   │   ├── UserProfileHeader.js
│   │   └── Post.js
│   ├── graphql/             # Generierte Operations-/Schema-Artefakte
│   └── models/              # Amplify modelgen-Ausgaben
├── amplify/
│   └── backend/             # Amplify-Backend-Ressourcen (auth/api/storage)
├── i18n/                    # Verzeichnis für übersetzte READMEs
│   ├── README.ar.md
│   ├── README.de.md
│   ├── README.es.md
│   ├── README.fr.md
│   ├── README.ja.md
│   ├── README.ko.md
│   ├── README.ru.md
│   ├── README.vi.md
│   └── README.zh-Hant.md
├── app.json
├── babel.config.js
├── index.js
└── package.json
```

## Voraussetzungen ✅

- Node.js 18+ empfohlen.
- npm (Lockfile ist `package-lock.json`).
- Expo-kompatible Tools:
  - iOS-Simulator + Xcode (für lokale iOS-Simulation).
  - Android Studio + SDK/Emulator (für lokale Android-Simulation).
- AWS-Kontozugriff für die Amplify-Provisionierung.
- Amplify CLI für das Backend-Setup.

## Installation 🚀

### 1. Repository klonen

Nutze dein bevorzugtes Remote-Repository:

| Befehl | Hinweise |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | Historischer/archivarischer Verweis |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | Aktuelles Repository (empfohlen) |

Dann öffne das richtige Projektverzeichnis:

```bash
cd onlyideas-react-native
```

Dieses Repository ist speziell auf die **OnlyIdeas**-Plattform zugeschnitten und fokussiert sich auf Kreativität und Monetarisierung.

### 2. Abhängigkeiten installieren

Vom Projekt-Root aus ausführen:

```bash
npm install
```

Damit werden die benötigten Node-Module installiert, einschließlich **Expo**, **React Native** und **aws-amplify**.

## AWS Amplify einrichten und initialisieren ☁️

1. **Amplify CLI** installieren (falls noch nicht geschehen):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Amplify konfigurieren** mit deinen AWS-Zugangsdaten:

   ```bash
   amplify configure
   ```

   - Melde dich in der AWS-Konsole an, erstelle oder verwende einen vorhandenen IAM-User.
   - Gib `accessKeyId` und `secretAccessKey` an.
   - Benenne das neue Profil (z. B. `onlyideas`).

3. **Amplify in diesem Projekt initialisieren**:

   ```bash
   amplify init
   ```

   Empfohlene Eingaben:

   - Environment-Name: `dev` (oder deine Wahl)
   - Standardeditor: deine Wahl
   - Authentifizierungsmethode: `AWS profile`
   - Profil: wähle das soeben konfigurierte Profil aus

4. **Amplify-Backend bereitstellen**:

   ```bash
   amplify push
   ```

Damit wird das AWS-Backend (Cognito, AppSync, S3 usw.) für OnlyIdeas bereitgestellt.

## App starten ▶️

Nutze **Expo**, um deine App auf verschiedenen Plattformen zu starten:

```bash
npx expo start
```

Oder über Paket-Skripte:

| Skript | Befehl | Zweck |
|---|---|---|
| `npm start` | `expo start` | Expo-Dev-Server starten |
| `npm run ios` | `expo start --ios` | iOS-Simulator starten |
| `npm run android` | `expo start --android` | Android-Emulator starten |
| `npm run web` | `expo start --web` | Web-Ziel starten |

- Drücke `i`, um den iOS-Simulator zu öffnen (macOS + Xcode erforderlich).
- Drücke `a`, um einen Android-Emulator zu öffnen (erfordert Android Studio & SDK).
- Drücke `w`, um den Web-Build im Browser zu öffnen.

### Web-Ausführung

Da dieses Projekt einige **React Native**-spezifische Bibliotheken nutzt (z. B. `@aws-amplify/ui-react-native`), musst du möglicherweise solche Importe bei Bundling für Web bedingt behandeln, falls du einen Fehler siehst. In vielen Fällen funktioniert **web** direkt. Bei Problemen kannst du:

- Importe entfernen oder ersetzen, die ausschließlich nativ sind, oder
- den Web-Build überspringen und weiter mit den nativen Plattformen arbeiten.

## Konfigurationshinweise ⚙️

### Erforderliche generierte Datei: `src/aws-exports.js`

`app/_layout.js` importiert `../src/aws-exports`, aber diese Datei wird von Amplify erzeugt und ist in diesem Repository nicht versioniert. Durch Ausführung von `amplify init` + `amplify push` sollte sie generiert werden.

### Aufbau des Amplify-Backends

Aus `amplify/backend/backend-config.json` geht hervor, dass dieses Projekt Folgendes enthält:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Zusätzlicher Authentifizierungs-Detailhinweis aus dem Repository:

- Die Standard-AppSync-Authentifizierung ist derzeit `API_KEY`, zusätzlich als Anbieter ist AWS IAM konfiguriert.

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

## Beispiele zur Nutzung 🧪

### Beitrag erstellen und veröffentlichen

1. App öffnen und anmelden.
2. Tippe auf `New post` im Startbildschirm.
3. Gib den Beitragstext ein.
4. Optional wähle ein Bild aus der Bibliothek.
5. Tippe auf `Post`, um das Bild hochzuladen und den `Post`-Datensatz zu speichern.

### Lokaler Backend-Workflow (typisch)

```bash
amplify status
amplify pull
amplify push
```

Wenn du Schema/Modelle anpasst, generiere die Artefakte bei Bedarf neu mit den entsprechenden Amplify-CLI-Befehlen in deinem Umfeld.

## Entwicklungshinweise 🛠️

- Routing ist dateibasiert über `expo-router` im Verzeichnis `app/`.
- Die aktuelle App kombiniert `DataStore` und direkte `API.graphql`-Mutationen.
- Bei Auth `signIn` überwacht `_layout.js` über `Hub` und versucht, einen passenden `User`-Datensatz zu erzeugen.
- In `package.json` sind aktuell keine dedizierten `test`- oder `lint`-Skripte definiert.
- Das `i18n/`-Verzeichnis existiert; README-Dateien in verschiedenen Sprachen sind hier vorgesehen.
- Sprachlinks werden bewusst als einzelne Optionszeile ganz oben in dieser README gehalten.

## Fehlerbehebung 🧯

### `Cannot find module '../src/aws-exports'`

Ausführen:

```bash
amplify init
amplify push
```

Stelle sicher, dass `src/aws-exports.js` lokal generiert wurde.

### Authentifizierung klappt, aber der Nutzer-Feed ist leer

- Prüfe, ob der `Hub`-Sign-in-Listener ausgeführt wurde und die User-Erstellungs-Mutation erfolgreich war.
- Prüfe den AppSync-Auth-Modus und die Berechtigungen.
- Prüfe die Daten in der DynamoDB/AppSync-Konsole für `User`-Datensätze.

### Bild-Upload bei neuem Beitrag schlägt fehl

- Bestätige, dass die S3-Speicherressource im Amplify-Backend existiert.
- Prüfe, ob der authentifizierte Nutzer Upload-Berechtigungen besitzt.
- Prüfe die Netzwerkanbindung und versuche es nach erneuter Authentifizierung erneut.

### Web-Build-Fehler bei nativ-only Importen

Importiere native-only Module bedingt oder konzentriere dich auf iOS/Android, wenn die Web-Kompatibilität Probleme bereitet.

## Roadmap / Nächste Schritte 🧭

- **KI-Integration**: Füge Endpunkte oder Third-Party-API-Aufrufe hinzu (z. B. OpenAI), um automatisierte Inhaltsgenerierung, Musikakkordanalyse oder Übersetzungen zu unterstützen.
- **Monetarisierung**: Integriere Abo- oder Zahlungsfunktionen (z. B. Stripe), wenn du monetarisierte Funktionen nachbauen willst.
- **Deployment**: Nutze [EAS Build](https://docs.expo.dev/eas/) oder vergleichbare Tools, um eigenständige Apps für iOS und Android zu erzeugen.
- Erweitere das i18n-README-Set im `i18n/`-Verzeichnis mithilfe der Sprachlinks am Anfang dieser Datei.

## Danksagung 🙌

- Originalprojekt von [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Adaptiert und als **OnlyIdeas** neu gebrandet, mit Fokus darauf, Menschen beim Teilen und Monetarisieren ihrer Ideen zu unterstützen, mit geplanten KI-Funktionen für Musik, Sprachübersetzung und Forschungszusammenarbeit.

Für zusätzliche Details zur ursprünglichen Codebasis und zu Funktionen, prüfe bitte die README im Original-Repository.

## Mitwirken 🤝

Beiträge sind willkommen. Bis eine dedizierte `CONTRIBUTING.md` hinzugefügt wird, folge bitte diesem leichtgewichtigen Ablauf:

1. Repository forken.
2. Einen Feature-Branch erstellen.
3. Änderungen fokussiert halten und auf mindestens einer Zielplattform testen.
4. Eine Pull Request mit klaren Setup-/Reproduktionshinweisen öffnen.

Wenn du Amplify-Ressourcen änderst, füge die entsprechenden `amplify/`-Änderungen und Migrationshinweise in die PR-Beschreibung ein.

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## License 📄

Es ist derzeit keine `LICENSE`-Datei in diesem Repository vorhanden.

Annahme: Alle Rechte sind standardmäßig vorbehalten, sofern nicht explizit eine Lizenz durch die Maintainer hinzugefügt wird.

---

Viel Spaß beim Bauen von **OnlyIdeas** und passe die Plattform gerne an, um Nutzerideen mit KI-Unterstützung zu schützen und zu monetarisieren.
