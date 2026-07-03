# 🔥 Firebase Setup Guide - Para Dummies

## 🎯 Objetivo

Configurar Firebase con tu cuenta `@lightforceortho.com` y habilitar **Firebase API** para que Claude pueda hacer cambios desde el código.

---

## 📋 Paso 1: Crear Cuenta Firebase (5 minutos)

### 1.1 Ir a Firebase Console

Abre tu navegador y ve a: **https://console.firebase.google.com**

### 1.2 Login con Email de LightForce

⚠️ **MUY IMPORTANTE:** Usa tu email `@lightforceortho.com`

- Click en **Sign in with Google**
- Selecciona tu cuenta de LightForce (no Gmail personal)
- Si pide permisos, acepta

### 1.3 Verificar que Estás Logged In

Arriba a la derecha debe aparecer tu foto/inicial con email `@lightforceortho.com`

✅ Si dice `@lightforceortho.com` → Perfecto, continúa
❌ Si dice `@gmail.com` → Sal y vuelve a entrar con cuenta de LightForce

---

## 📋 Paso 2: Crear Proyecto Firebase (3 minutos)

### 2.1 Click en "Add project" o "Crear proyecto"

(Es un botón grande en el centro o arriba a la derecha)

### 2.2 Configuración del Proyecto

**Pantalla 1: Nombre del proyecto**
```
Nombre: lf-hosting-test
```

- Click en **Continue**

**Pantalla 2: Google Analytics**
```
Enable Google Analytics: NO (desmarca la opción)
```

- No necesitamos analytics para este proyecto de testing
- Click en **Create project**

⏳ Espera 30-60 segundos mientras Firebase crea el proyecto

**Pantalla 3: Ready!**

- Click en **Continue**

---

## 📋 Paso 3: Habilitar Firebase API (CRÍTICO - 5 minutos)

⚠️ **ESTE PASO ES OBLIGATORIO** para que Claude pueda hacer cambios desde el código.

### 3.1 Ir a Google Cloud Console

Mientras estás en Firebase Console, click en el **ícono de engrane** (arriba izquierda) → **Project settings**

Scroll down hasta la sección **"Your project"**

Verás algo como:
```
Project ID: lf-hosting-test-abc123
```

**Copia ese Project ID** (lo necesitarás)

### 3.2 Ir a Google Cloud APIs

Abre una nueva pestaña y ve a:

**https://console.cloud.google.com/apis/library**

Arriba a la izquierda, verifica que el proyecto seleccionado sea `lf-hosting-test-abc123`

Si no lo es, click en el dropdown y selecciónalo.

### 3.3 Habilitar Firebase Management API

En el buscador de APIs, escribe:
```
Firebase Management API
```

Click en **Firebase Management API** (el primer resultado)

Click en el botón azul **ENABLE** / **HABILITAR**

⏳ Espera 10-20 segundos

✅ Verás un mensaje "API enabled" / "API habilitada"

### 3.4 Habilitar Firebase Hosting API

Vuelve atrás (flecha atrás del navegador) o ve de nuevo a:

**https://console.cloud.google.com/apis/library**

En el buscador, escribe:
```
Firebase Hosting API
```

Click en **Firebase Hosting API**

Click en **ENABLE** / **HABILITAR**

⏳ Espera 10-20 segundos

✅ Listo

### 3.5 Habilitar Cloud Run API (para el backend después)

Mismo proceso:

**https://console.cloud.google.com/apis/library**

Buscar:
```
Cloud Run API
```

Click → **ENABLE**

✅ Done

---

## 📋 Paso 4: Crear Service Account (CRÍTICO - 7 minutos)

Este paso permite que Claude interactúe con Firebase desde el código.

### 4.1 Ir a Service Accounts

Ve a:

**https://console.cloud.google.com/iam-admin/serviceaccounts**

Verifica que el proyecto sea `lf-hosting-test-abc123`

### 4.2 Crear Service Account

Click en **+ CREATE SERVICE ACCOUNT** (arriba)

**Paso 1: Service account details**
```
Service account name: firebase-admin-automation
Service account ID: firebase-admin-automation (auto-genera)
Description: Service account for Claude Code automation
```

Click en **CREATE AND CONTINUE**

**Paso 2: Grant this service account access to project**

En el dropdown "Select a role", busca y selecciona:

1. **Firebase Admin** (busca "firebase" y selecciona "Firebase Admin")
2. Click en **+ ADD ANOTHER ROLE**
3. **Cloud Run Admin** (para el backend después)
4. Click en **+ ADD ANOTHER ROLE**
5. **Service Account User**

Click en **CONTINUE**

**Paso 3: Grant users access to this service account**

Deja en blanco, click en **DONE**

### 4.3 Crear Clave JSON (Private Key)

Ahora verás tu service account en la lista.

Click en el **email del service account** (firebase-admin-automation@...)

Ve a la pestaña **KEYS** (arriba)

Click en **ADD KEY** → **Create new key**

Selecciona **JSON**

Click en **CREATE**

📥 Se descargará un archivo JSON (ejemplo: `lf-hosting-test-abc123-1a2b3c4d5e6f.json`)

⚠️ **MUY IMPORTANTE:**
- Este archivo es un secreto (como una contraseña)
- NO lo subas a GitHub
- Guárdalo en tu computadora en un lugar seguro

### 4.4 Mover el Archivo a la Carpeta del Proyecto

Abre tu **Finder** (Mac) o **Explorador de archivos** (Windows)

Mueve el archivo JSON descargado a:

```
/Users/adrianjimenez/Documents/lfo_github/digital_skills/lf-hosting-test/
```

Renómbralo a algo más simple:

```
firebase-service-account.json
```

Ruta final:
```
/Users/adrianjimenez/Documents/lfo_github/digital_skills/lf-hosting-test/firebase-service-account.json
```

---

## 📋 Paso 5: Verificar Configuración (2 minutos)

### 5.1 Verificar APIs Habilitadas

Ve a:

**https://console.cloud.google.com/apis/dashboard**

Deberías ver en la lista:

- ✅ Firebase Management API
- ✅ Firebase Hosting API
- ✅ Cloud Run API

### 5.2 Verificar Service Account

Ve a:

**https://console.cloud.google.com/iam-admin/serviceaccounts**

Deberías ver:

```
firebase-admin-automation@lf-hosting-test-abc123.iam.gserviceaccount.com
```

Con roles:
- Firebase Admin
- Cloud Run Admin
- Service Account User

---

## 🎯 Checklist Final - ¿Listo para Continuar?

Marca cada item:

- [ ] Logged in a Firebase con `@lightforceortho.com`
- [ ] Proyecto `lf-hosting-test` creado
- [ ] Firebase Management API habilitada
- [ ] Firebase Hosting API habilitada
- [ ] Cloud Run API habilitada
- [ ] Service Account creado (`firebase-admin-automation`)
- [ ] JSON key descargada y guardada en el proyecto como `firebase-service-account.json`

---

## ✅ Una Vez Completado

Avísale a Claude que terminaste:

```
"Listo, Firebase configurado. El archivo JSON está en firebase-service-account.json"
```

Claude podrá verificar el archivo y continuar con el deployment automático.

---

## 🆘 Troubleshooting

### Error: "Permission denied" al crear Service Account

**Solución:** Tu cuenta `@lightforceortho.com` necesita permisos de "Owner" en Google Cloud.

Pídele a tu IT admin (Jayke?) que te dé permisos de **Project Owner** en Google Cloud Console.

### Error: "API not enabled"

**Solución:** Vuelve a **Paso 3** y verifica que las 3 APIs estén habilitadas.

### No encuentro el archivo JSON descargado

**Solución:** 
- Mac: Busca en `~/Downloads/`
- Windows: Busca en `C:\Users\TuUsuario\Downloads\`
- Archivo empieza con el nombre del proyecto (lf-hosting-test...)

---

## 📚 Recursos

- Firebase Console: https://console.firebase.google.com
- Google Cloud Console: https://console.cloud.google.com
- APIs Library: https://console.cloud.google.com/apis/library
- Service Accounts: https://console.cloud.google.com/iam-admin/serviceaccounts

---

## 🔒 Seguridad - IMPORTANTE

⚠️ El archivo `firebase-service-account.json` es un secreto:

- ✅ Ya está en `.gitignore` (no se subirá a GitHub)
- ❌ NUNCA lo compartas en Slack/email
- ❌ NUNCA lo pegues en ningún lado
- ✅ Solo Claude lo usará localmente

Si lo pierdes, puedes crear otro desde Google Cloud Console (Paso 4.3).
