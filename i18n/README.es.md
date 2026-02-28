[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# Aplicación Full Stack OnlyIdeas

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

**OnlyIdeas** es una aplicación full stack que ayuda a las personas a compartir y monetizar sus ideas. Se integra con **AWS Amplify** para autenticación de usuarios, almacenamiento de datos (**AppSync** y **DynamoDB**) y alojamiento de archivos (**S3**). Puedes ejecutar este proyecto en **iOS**, **Android** y **Web** a través de **Expo**.

Inspirada en funciones con estilo de **OnlyFans**, OnlyIdeas también busca integrar herramientas de IA para generar, analizar y traducir ideas, música o contenido multimedia aportado por los usuarios.

Este README es una versión ampliada y precisa del repositorio, basada en el contenido existente del README y en los archivos fuente actuales.

## Descripción general 📌

### Stack de un vistazo

| Área | Tecnología |
|---|---|
| Framework de la app | `React Native` + `Expo` |
| Navegación | `expo-router` |
| Autenticación + Datos + Almacenamiento | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Base de datos | `Amazon DynamoDB` (vía modelos GraphQL de Amplify) |
| Almacenamiento de archivos | `Amazon S3` |
| Plataformas objetivo | iOS, Android, Web |

OnlyIdeas usa:

- `expo-router` para navegación y pantallas basadas en rutas.
- `aws-amplify` + `@aws-amplify/ui-react-native` para autenticación, API, DataStore y almacenamiento.
- Categorías de backend de Amplify para **Auth (Cognito)**, **API (AppSync GraphQL)** y **Storage (S3)**.

Flujo actual de usuario:

1. Inicia sesión con Amplify Authenticator.
2. El feed principal muestra creadores (registros `User`).
3. Abre un perfil de creador y consulta sus publicaciones/estado de paywall.
4. Crea una publicación nueva con carga opcional de imagen a S3.

## Funcionalidades ✨

- Listado de creadores y páginas de perfil.
- Inicio y cierre de sesión con Amplify UI Authenticator.
- Creación de nuevas publicaciones con integración de selector de imágenes.
- Carga y recuperación de imágenes en S3.
- Persistencia de modelos `User` y `Post` con soporte de GraphQL.
- Objetivos de ejecución para iOS, Android y Web desde un solo proyecto de Expo.

## Estructura del proyecto 🗂️

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

## Requisitos previos ✅

- Node.js 18+ recomendado.
- npm (el lockfile es `package-lock.json`).
- Herramientas compatibles con Expo:
  - iOS Simulator + Xcode (para simulación local en iOS).
  - Android Studio + SDK/emulador (para simulación local en Android).
- Acceso a cuenta de AWS para aprovisionar Amplify.
- Amplify CLI para configuración del backend.

## Instalación 🚀

### 1. Clonar el repositorio

Usa el remote que prefiera tu flujo de trabajo:

| Command | Notes |
|---|---|
| `git clone git@github.com:lachlanchen/onlyideas.git` | Referencia histórica/archival |
| `git clone git@github.com:lachlanchen/onlyideas-react-native.git` | Repositorio actual (recomendado) |

Luego abre el directorio correcto:

```bash
cd onlyideas-react-native
```

Este repositorio está diseñado específicamente para la plataforma **OnlyIdeas**, con enfoque en creatividad y monetización.

### 2. Instalar dependencias

Desde la raíz del proyecto, ejecuta:

```bash
npm install
```

Esto instala los módulos de Node necesarios, incluyendo **Expo**, **React Native** y **aws-amplify**.

## Configurar e inicializar AWS Amplify ☁️

1. **Instala Amplify CLI** (si aún no lo hiciste):

   ```bash
   npm install -g @aws-amplify/cli
   ```

2. **Configura Amplify** con tus credenciales de AWS:

   ```bash
   amplify configure
   ```

   - Inicia sesión en la consola de AWS, crea o usa un usuario IAM existente.
   - Proporciona `accessKeyId` y `secretAccessKey`.
   - Nombra el nuevo perfil (por ejemplo, `onlyideas`).

3. **Inicializa Amplify** en este proyecto:

   ```bash
   amplify init
   ```

   Sugerencias recomendadas:

   - Nombre de entorno: `dev` (o el que prefieras)
   - Editor predeterminado: el que elijas
   - Método de autenticación: `AWS profile`
   - Perfil: selecciona el que acabas de configurar

4. **Despliega el backend de Amplify**:

   ```bash
   amplify push
   ```

Esto aprovisiona el backend de AWS (Cognito, AppSync, S3, etc.) para OnlyIdeas.

## Ejecutar la app ▶️

Usa **Expo** para lanzar tu app en diferentes plataformas:

```bash
npx expo start
```

O mediante scripts de `package`:

| Script | Command | Purpose |
|---|---|---|
| `npm start` | `expo start` | Inicia el servidor de desarrollo de Expo |
| `npm run ios` | `expo start --ios` | Abre el simulador de iOS |
| `npm run android` | `expo start --android` | Abre el emulador de Android |
| `npm run web` | `expo start --web` | Ejecuta el objetivo web |

- Pulsa `i` para abrir el simulador de iOS (requiere macOS + Xcode).
- Pulsa `a` para abrir un emulador de Android (requiere Android Studio y SDK).
- Pulsa `w` para abrir la build web en tu navegador.

### Ejecutar en Web

Como este proyecto usa algunas librerías específicas de **React Native** (por ejemplo, `@aws-amplify/ui-react-native`), puede que necesites manejar esas importaciones de forma condicional si al hacer el bundle para web aparece un error. En la mayoría de los casos, la web funcionará directamente. Si tienes problemas, puedes:

- Quitar o sustituir importaciones nativas puras, o
- Omitir la build web y continuar con plataformas nativas.

## Notas de configuración ⚙️

### Archivo generado requerido: `src/aws-exports.js`

`app/_layout.js` importa `../src/aws-exports`, pero este archivo lo genera Amplify y no está incluido en el repositorio. Ejecutar `amplify init` + `amplify push` debería generarlo.

### Forma del backend de Amplify

En `amplify/backend/backend-config.json`, este proyecto incluye:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Detalle adicional de autenticación:

- La autenticación predeterminada de AppSync actualmente es `API_KEY` con AWS IAM como proveedor adicional.

### Modelo de datos de GraphQL

Definido en `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- Modelo `User` con campos de perfil (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- Modelo `Post` con `text`, imagen opcional (`image`), `likes` e índice `userID` (`byUser`)

### Configuración de Expo/Babel

- `index.js` carga el polyfill de `async iterator` y `expo-router/entry`.
- `babel.config.js` incluye:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## Ejemplos de uso 🧪

### Crear y publicar una publicación

1. Abre la app e inicia sesión.
2. Toca `New post` en la pantalla principal.
3. Escribe el texto de la publicación.
4. Opcionalmente, selecciona una imagen de la galería.
5. Toca `Post` para subir la imagen y guardar el registro `Post`.

### Flujo típico del backend local

```bash
amplify status
amplify pull
amplify push
```

Si modificas el esquema/modelos, regenera los artefactos según sea necesario con los comandos de Amplify CLI en tu entorno.

## Notas de desarrollo 🛠️

- El enrutamiento es basado en archivos mediante `expo-router` bajo `app/`.
- La app actual mezcla `DataStore` y uso directo de mutaciones `API.graphql`.
- Al autenticarse (`signIn`), `_layout.js` escucha con `Hub` e intenta crear el `User` correspondiente.
- Actualmente no hay scripts dedicados de `test` o `lint` definidos en `package.json`.
- El directorio `i18n/` existe; los README de idiomas están previstos pero aún no se han añadido en este borrador.
- Los enlaces de idioma se mantienen intencionadamente como una sola línea de opciones al inicio de este README.

## Solución de problemas 🧯

### `Cannot find module '../src/aws-exports'`

Ejecuta:

```bash
amplify init
amplify push
```

Asegúrate de que `src/aws-exports.js` se genere localmente.

### La autenticación es correcta pero el feed de usuarios está vacío

- Confirma que se haya ejecutado el listener de `Hub` en `signIn` y la mutación para crear usuario haya tenido éxito.
- Revisa el modo de autenticación y permisos de AppSync.
- Verifica datos en la consola de DynamoDB/AppSync para registros `User`.

### Falla la carga de imágenes al crear una publicación

- Confirma que el recurso de almacenamiento S3 exista en el backend de Amplify.
- Verifica que el usuario autenticado tenga permiso para subir.
- Comprueba el acceso a la red y vuelve a intentarlo después de reautenticar.

### Errores de compilación web con importaciones nativas

Importa módulos nativos de forma condicional, o enfócate en iOS/Android durante el desarrollo si la compatibilidad web se rompe.

## Hoja de ruta / Próximos pasos 🧭

- **Integración de IA**: añadir endpoints o llamadas a API de terceros (por ejemplo, OpenAI) para soportar generación automatizada de contenido, análisis de acordes musicales o traducciones.
- **Monetización**: incorporar funciones de suscripción o pago (por ejemplo, Stripe) si deseas replicar funcionalidades monetizadas.
- **Despliegue**: Usa [EAS Build](https://docs.expo.dev/eas/) o similar para generar apps independientes para iOS y Android.
- Expandir el conjunto de README i18n en `i18n/` usando los enlaces de idioma en el inicio de este archivo.

## Agradecimientos 🙌

- Proyecto original de [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Adaptado y renombrado como **OnlyIdeas**, enfocado en ayudar a las personas a compartir y monetizar sus ideas, con funciones de IA planificadas para música, traducción de idiomas y colaboración en investigación.

Para detalles adicionales sobre la base de código original y sus características, revisa el README del repositorio original.

## Contribuir 🤝

Las contribuciones son bienvenidas. Hasta que se añada un `CONTRIBUTING.md` dedicado, sigue este flujo ligero:

1. Haz un fork del repo.
2. Crea una rama de característica.
3. Mantén los cambios enfocados y pruebalos en al menos una plataforma.
4. Abre un pull request con notas claras de configuración/reproducción.

Si cambias recursos de Amplify, incluye los cambios correspondientes de `amplify/` y notas de migración en la descripción del PR.

## Licencia 📄

Actualmente no hay un archivo `LICENSE` presente en este repositorio.

Se asume que todos los derechos están reservados por defecto hasta que los mantenedores agreguen una licencia explícita.

---

Disfruta construyendo **OnlyIdeas** y siéntete libre de adaptar la plataforma para proteger y monetizar ideas de usuarios con asistencia de IA.


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
