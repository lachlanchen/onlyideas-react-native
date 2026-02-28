[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Aplicación Full Stack OnlyIdeas

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20Android%20%7C%20Web-2ea44f)
![Expo](https://img.shields.io/badge/Expo-48-000020?logo=expo)
![React Native](https://img.shields.io/badge/React%20Native-0.71-61dafb?logo=react)
![AWS Amplify](https://img.shields.io/badge/AWS-Amplify-orange?logo=amazon-aws)
![Backend](https://img.shields.io/badge/Backend-AppSync%20%2B%20DynamoDB-ff9900)
![Storage](https://img.shields.io/badge/Storage-S3-569A31)
![Auth](https://img.shields.io/badge/Auth-Cognito-DD344C)
![License](https://img.shields.io/badge/License-Not%20Specified-lightgrey)

**OnlyIdeas** es una aplicación full stack que ayuda a las personas a compartir y monetizar sus ideas. Se integra con **AWS Amplify** para autenticación de usuarios, almacenamiento de datos (AppSync y DynamoDB) y alojamiento de archivos (S3). Puedes ejecutar este proyecto en **iOS**, **Android** y **Web** mediante **Expo**.

Inspirada en funciones de estilo “OnlyFans”, OnlyIdeas también busca integrar herramientas de IA para generar, analizar y traducir ideas, música o contenido multimedia aportado por usuarios.

Este README es un borrador ampliado y fiel al repositorio, basado en el contenido existente del README y en los archivos fuente actuales.

## Resumen 📌

### Stack de un vistazo

| Área | Tecnología |
|---|---|
| Framework de la app | `React Native` + `Expo` |
| Navegación | `expo-router` |
| Auth + Datos + Almacenamiento | `aws-amplify` + `@aws-amplify/ui-react-native` |
| API | `AWS AppSync (GraphQL)` |
| Base de datos | `Amazon DynamoDB` (mediante modelos GraphQL de Amplify) |
| Almacenamiento de archivos | `Amazon S3` |
| Plataformas objetivo | iOS, Android, Web |

OnlyIdeas usa:

- `expo-router` para navegación y pantallas basadas en rutas.
- `aws-amplify` + `@aws-amplify/ui-react-native` para autenticación, API, DataStore y almacenamiento.
- Categorías de backend de Amplify para **Auth (Cognito)**, **API (AppSync GraphQL)** y **Storage (S3)**.

Flujo actual de usuario:

1. Iniciar sesión mediante Amplify Authenticator.
2. El feed principal muestra creadores (registros `User`).
3. Abrir el perfil de un creador y ver publicaciones/estado de paywall.
4. Crear una nueva publicación con carga opcional de imagen a S3.

## Funcionalidades ✨

- Listado de creadores y páginas de perfil.
- Inicio y cierre de sesión con Amplify UI Authenticator.
- Creación de nuevas publicaciones con integración de selector de imágenes.
- Carga y recuperación de imágenes en S3.
- Persistencia de modelos `User` y `Post` respaldada por GraphQL.
- Objetivos de ejecución para iOS, Android y Web desde un solo proyecto Expo.

## Estructura del Proyecto 🗂️

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

## Requisitos Previos ✅

- Se recomienda Node.js 18+.
- npm (el lockfile es `package-lock.json`).
- Herramientas compatibles con Expo:
  - iOS Simulator + Xcode (para simulación local en iOS).
  - Android Studio + SDK/emulador (para simulación local en Android).
- Acceso a una cuenta de AWS para aprovisionar Amplify.
- Amplify CLI para configurar el backend.

## Instalación 🚀

### 1. Clonar el Repositorio

Conservando el comando canónico existente:

```bash
git clone git@github.com:lachlanchen/onlyideas.git
cd onlyideas
```

Remote fiel al repositorio configurado actualmente en este repo:

```bash
git clone git@github.com:lachlanchen/onlyideas-react-native.git
cd onlyideas-react-native
```

Este repositorio está adaptado específicamente para la plataforma **OnlyIdeas**, con enfoque en creatividad y monetización.

### 2. Instalar Dependencias

Desde la raíz del proyecto, ejecuta:

```bash
npm install
```

Esto instala los módulos de Node necesarios, incluyendo **Expo**, **React Native** y **aws-amplify**.

## Configurar e Inicializar AWS Amplify ☁️

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
   - Asigna un nombre al nuevo perfil (por ejemplo, `onlyideas`).

3. **Inicializa Amplify** en este proyecto:

   ```bash
   amplify init
   ```

   Prompts recomendados:

   - Nombre del entorno: `dev` (o el que prefieras)
   - Editor predeterminado: el de tu preferencia
   - Método de autenticación: `AWS profile`
   - Perfil: selecciona el que acabas de configurar

4. **Haz push del backend de Amplify**:

   ```bash
   amplify push
   ```

Esto aprovisiona el backend de AWS (Cognito, AppSync, S3, etc.) para OnlyIdeas.

## Ejecutar la App ▶️

Usa **Expo** para iniciar tu app en distintas plataformas:

```bash
npx expo start
```

O mediante scripts de package:

| Script | Command | Purpose |
|---|---|---|
| `npm start` | `expo start` | Start Expo dev server |
| `npm run ios` | `expo start --ios` | Launch iOS simulator |
| `npm run android` | `expo start --android` | Launch Android emulator |
| `npm run web` | `expo start --web` | Run web target |

- Presiona `i` para abrir el simulador de iOS (requiere macOS + Xcode).
- Presiona `a` para abrir un emulador de Android (requiere Android Studio y SDK).
- Presiona `w` para abrir la versión web en tu navegador.

### Ejecución en Web

Como este proyecto usa algunas librerías específicas de **React Native** (por ejemplo, `@aws-amplify/ui-react-native`), puede que necesites manejar esas importaciones de forma condicional si aparece un error al empaquetar para web. En muchos casos, **web** funcionará directamente. Si encuentras problemas, puedes:

- Eliminar o reemplazar importaciones que sean exclusivamente nativas, o
- Omitir la compilación web y continuar usando plataformas nativas.

## Notas de Configuración ⚙️

### Archivo generado obligatorio: `src/aws-exports.js`

`app/_layout.js` importa `../src/aws-exports`, pero este archivo lo genera Amplify y no está versionado en este repositorio. Ejecutar `amplify init` + `amplify push` debería generarlo.

### Estructura del backend de Amplify

Según `amplify/backend/backend-config.json`, este proyecto incluye:

- `auth/OnlyFansCloneApp` (Cognito)
- `api/OnlyFansCloneApp` (AppSync GraphQL)
- `storage/s3onlyfanscloneappstorageb3e1fac4` (S3)

Detalle adicional de autenticación fiel al repositorio:

- La autenticación predeterminada de AppSync actualmente es `API_KEY`, con AWS IAM como proveedor adicional.

### Modelo de datos GraphQL

Definido en `amplify/backend/api/OnlyFansCloneApp/schema.graphql`:

- Modelo `User` con campos de perfil (`name`, `handle`, `bio`, `avatar`, `coverImage`, `subscriptionPrice`)
- Modelo `Post` con `text`, `image` opcional, `likes` e índice `userID` (`byUser`)

### Configuración de Expo/Babel

- `index.js` carga el polyfill de async iterator y `expo-router/entry`.
- `babel.config.js` incluye:
  - `@babel/plugin-proposal-export-namespace-from`
  - `react-native-reanimated/plugin`
  - `expo-router/babel`

## Ejemplos de Uso 🧪

### Crear y publicar una publicación

1. Abre la app e inicia sesión.
2. Toca `New post` en la pantalla principal.
3. Introduce el texto de la publicación.
4. Opcionalmente, selecciona una imagen desde la biblioteca.
5. Toca `Post` para subir la imagen y guardar el registro `Post`.

### Flujo típico de backend local

```bash
amplify status
amplify pull
amplify push
```

Si modificas el esquema/modelos, regenera los artefactos cuando sea necesario con comandos de Amplify CLI en tu entorno.

## Notas de Desarrollo 🛠️

- El enrutamiento es basado en archivos mediante `expo-router` bajo `app/`.
- La app actual mezcla uso de `DataStore` y mutaciones directas con `API.graphql`.
- En `signIn`, `_layout.js` escucha mediante `Hub` e intenta crear un registro `User` correspondiente.
- Actualmente no hay scripts dedicados de `test` o `lint` definidos en `package.json`.
- El directorio `i18n/` existe; los README por idioma están planificados, pero aún no se agregan en este borrador.
- Los enlaces de idioma se mantienen intencionalmente como una única línea de opciones al inicio de este README.

## Solución de Problemas 🧯

### `Cannot find module '../src/aws-exports'`

Ejecuta:

```bash
amplify init
amplify push
```

Asegúrate de que `src/aws-exports.js` se genere localmente.

### La autenticación funciona, pero el feed de usuarios está vacío

- Confirma que se ejecutó el listener de `Hub` en `sign-in` y que la mutación de creación de usuario se completó correctamente.
- Revisa el modo de autenticación de AppSync y los permisos.
- Verifica en la consola de DynamoDB/AppSync que existan registros `User`.

### Falla la carga de imágenes en nueva publicación

- Confirma que el recurso de almacenamiento S3 exista en el backend de Amplify.
- Verifica que el usuario autenticado tenga permisos para subir archivos.
- Revisa el acceso de red y vuelve a intentar después de reautenticar.

### Errores de compilación web con importaciones solo nativas

Importa módulos solo nativos de forma condicional, o enfócate en iOS/Android para desarrollo si la compatibilidad web se rompe.

## Hoja de Ruta / Próximos Pasos 🧭

- **Integración de IA**: Añadir endpoints o llamadas a API de terceros (por ejemplo, OpenAI) para soportar generación automática de contenido, análisis de acordes musicales o traducciones.
- **Monetización**: Incorporar funciones de suscripción o pagos (por ejemplo, Stripe) si quieres replicar funcionalidades monetizadas.
- **Despliegue**: Usar [EAS Build](https://docs.expo.dev/eas/) u otra alternativa para generar apps standalone para iOS y Android.
- Ampliar el conjunto de README i18n en `i18n/` usando los enlaces de idioma al inicio de este archivo.

## Agradecimientos 🙌

- Proyecto original de [GonzaloVolonterio](https://github.com/GonzaloVolonterio/react-native-onlyfans-clone-app).
- Adaptado y renombrado como **OnlyIdeas**, enfocado en ayudar a las personas a compartir y monetizar sus ideas, con funciones de IA planificadas para música, traducción de idiomas y colaboración en investigación.

Para más detalles sobre el código base y las funcionalidades originales, consulta el README del repositorio original.

## Contribuir 🤝

Las contribuciones son bienvenidas. Mientras no exista un `CONTRIBUTING.md` dedicado, sigue este flujo ligero:

1. Haz fork del repositorio.
2. Crea una rama de funcionalidad.
3. Mantén los cambios acotados y prueba al menos en una plataforma objetivo.
4. Abre un pull request con notas claras de configuración/reproducción.

Si cambias recursos de Amplify, incluye en la descripción del PR las actualizaciones correspondientes en `amplify/` y notas de migración.

## Licencia 📄

Actualmente no hay un archivo `LICENSE` en este repositorio.

Suposición: todos los derechos están reservados por defecto, salvo que los mantenedores agreguen una licencia explícita.

---

Disfruta construyendo **OnlyIdeas** y adapta libremente la plataforma para proteger y monetizar ideas de usuarios con ayuda de IA.
