# Mi Tablero Financiero — versión con backend propio (Firebase + GitHub Pages)

Esta es la versión del tablero para desplegar tú misma, fuera de Claude.
Usa **Firebase** (Google) como backend: autenticación con Google y base de
datos Firestore. El hosting (dónde vive la página) va en **GitHub Pages**,
gratis.

## 1. Crear el proyecto en Firebase (10 min)

1. Entra a https://console.firebase.google.com y crea un proyecto nuevo
   (ej. "mi-tablero-financiero"). No necesitas tarjeta, el plan gratuito
   (Spark) alcanza de sobra para uso personal.
2. En el menú lateral: **Build → Authentication → Get started**. Activa el
   proveedor **Google**.
3. En el menú lateral: **Build → Firestore Database → Create database**.
   Elige modo **producción** (ya tienes `firestore.rules` listo) y la
   región más cercana (ej. `southamerica-east1`).
4. Ve a **Project settings** (el ícono de engranaje) → pestaña **General**
   → sección "Your apps" → clic en el ícono `</>` (Web) → regístrala con
   cualquier nombre. Firebase te muestra un objeto `firebaseConfig`.
5. Abre `index.html` en este mismo paquete, busca la sección
   `window.FIREBASE_CONFIG` (cerca del final) y reemplaza esos valores
   por los tuyos. Ese objeto no es secreto, es normal que viaje en el
   navegador — la seguridad real la dan las reglas del paso 6.
6. En Firestore → pestaña **Rules**, pega el contenido de
   `firestore.rules` (ya incluido aquí) y publica.

## 2. Subir el código a GitHub (5 min)

1. Crea un repositorio nuevo en https://github.com/new, por ejemplo
   `mi-tablero-financiero`. Público está bien (el código no tiene nada
   privado tuyo; tus datos están en Firestore, protegidos por las reglas).
2. Sube estos tres archivos: `index.html`, `firestore.rules`, `README.md`.
   Puedes arrastrarlos directo en la web de GitHub ("Add file → Upload
   files") o con Git si ya lo manejas.

## 3. Activar GitHub Pages (2 min)

1. En el repositorio: **Settings → Pages**.
2. En "Source" elige la rama `main` y la carpeta `/ (root)`.
3. Guarda. En uno o dos minutos tu tablero queda disponible en:
   `https://<tu-usuario>.github.io/mi-tablero-financiero/`

## 4. Autorizar ese dominio en Firebase

1. Vuelve a Firebase → **Authentication → Settings → Authorized domains**.
2. Agrega `<tu-usuario>.github.io` (sin "https://").
3. Sin este paso, el botón "Entrar con Google" fallará en producción.

## Cómo funciona

- Al entrar, pide iniciar sesión con Google. Eso te da un `uid` único.
- Todos tus datos (cuentas, movimientos, programados, inversiones) se
  guardan bajo `users/<tu-uid>/...` en Firestore.
- Las reglas de `firestore.rules` dicen: "solo el dueño de ese `uid` puede
  leer o escribir ahí". Así, aunque el código sea público en GitHub, tus
  datos están protegidos.
- La primera vez que entres no vas a tener cuentas cargadas (a diferencia
  de la versión de Claude, que ya trae tus saldos reales) — créalas desde
  el botón "+ Agregar" o edítalas directo en la consola de Firestore.

## Siguiente nivel para portafolio

Si quieres mostrarlo en tu CV o en una entrevista, vale la pena:
- Subir el código con mensajes de commit claros (qué hiciste y por qué).
- Agregar una captura de pantalla al README.
- Mencionar en tu CV: "Diseñé y desplegué una app web con autenticación y
  base de datos en tiempo real (Firebase) alojada en GitHub Pages", y
  enlazar el repositorio.
