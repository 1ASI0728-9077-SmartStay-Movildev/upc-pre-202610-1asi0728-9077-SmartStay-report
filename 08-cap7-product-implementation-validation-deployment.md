<div style="page-break-before: always;"></div>

# Capítulo VII: Product Implementation, Validation, and Deployment.

## 7.1. Software Configuration Management

La gestión de configuración de Smart Stay define cómo se prepara el entorno de desarrollo, cómo se versiona el código, qué convenciones se siguen y cómo se construye, empaqueta y ejecuta la solución. El backend está compuesto por **siete microservicios en ASP.NET Core (.NET 9)**: IAM, Accommodations, Bookings, Payments, Profiles, Analytics y Concierge. Se ejecutan como contenedores Docker detrás de un gateway **Nginx**, con mensajería en **ActiveMQ** y persistencia en **MySQL**. La solución incluye un cliente web en Vue y contempla aplicaciones móviles para el staff (Android nativo) y el huésped (Flutter). El código web y backend se revisó en los ZIP entregados. Los componentes móviles se describen según la documentación del equipo.
La gestión de configuración de Smart Stay define cómo se prepara el entorno de desarrollo, cómo se versiona el código, qué convenciones se siguen y cómo se construye, empaqueta y ejecuta la solución. El backend está compuesto por **siete microservicios en ASP.NET Core (.NET 9)**: IAM, Accommodations, Bookings, Payments, Profiles, Analytics y Concierge. Se ejecutan como contenedores Docker detrás de un gateway **Nginx**, con mensajería en **ActiveMQ** y persistencia en **MySQL**. Los clientes son una aplicación Android nativa (Kotlin) para el staff operativo y una aplicación Flutter para el huésped.

### 7.1.1. Software Development Environment Configuration

**Project Management**

Para la gestión del proyecto se emplearon herramientas de comunicación, planificación y control de versiones. Se creó una organización en GitHub para centralizar los repositorios y coordinar el trabajo colaborativo.

| Actividad | Herramienta |
|---|---|
| Organización del trabajo y repositorios | GitHub (organización del equipo) |
| Reuniones | Discord |
| Comunicación | WhatsApp |
| Planificación y asignación de tareas | Trello |
| Gestión de Product Backlog y Sprint Backlog | Trello |
| Control de versiones | Git con GitFlow |

**Enlaces:** [GitHub](https://github.com/) · [Discord](https://discord.com/) · [Trello](https://trello.com/)

**Trello como soporte a Scrum.** El tablero usa las listas *Product Backlog* (User Stories priorizadas), *Sprint Backlog*, *To Do*, *In Process*, *To Review* y *Done*. Cada tarjeta incluye:

- Identificador de la User Story o Engineering Task (por ejemplo `US-24`, `UT-01`).
- Descripción, responsables, checklist de subtareas y fecha límite.
- Estimación de 4 a 8 horas por Engineering Task.
- Etiquetas: `Frontend`, `Backend`, `Documentation`, `Bug`, `Enhancement` y `High Priority`.
- Adjuntos (mockups, diagramas) y enlaces a los Pull Requests relacionados.

Flujo de trabajo del Sprint:

1. **Sprint Planning:** las User Stories pasan del Product Backlog al Sprint Backlog y se descomponen en Engineering Tasks con responsable y estimación.
2. **Desarrollo diario:** cada miembro mueve sus tareas de *To Do* a *In Process* y actualiza el avance con comentarios y checklists.
3. **Code Review:** al terminar, la tarea pasa a *To Review*. Otro miembro la valida y la mueve a *Done*, o la devuelve a *In Process* si requiere cambios.
4. **Sprint Review:** se verifica que todas las tareas del Sprint estén en *Done*, se documenta el resultado y se prepara el siguiente Sprint Backlog.

Métricas de seguimiento: burndown chart manual, velocity al cerrar cada Sprint y porcentaje de tareas completadas frente a las planificadas.

**Evidencia por incorporar:** capturas o enlaces del tablero de los sprints 1 y 2.
![sprint_trello](assets/trello.jpg)
*Tablero Trello del Sprint 1 mostrando la organización de tareas*

![sprint_trello](assets/trello2.jpg)
*Tablero Trello del Sprint 2 con Engineering Tasks en progreso*

**Requirement Management**

Trello se usó para la gestión visual de tareas. **UXPressia** sirvió para elaborar *User Personas*, *Empathy Maps*, *Journey Maps* y *Lean UX Canvas*, y **Miro** para construir los escenarios *As-Is* y *To-Be*.

**Enlaces:** [Trello](https://trello.com/) · [UXPressia](https://uxpressia.com/) · [Miro](https://miro.com/es/)

**Product UX/UI Design**

El equipo utilizó **Figma** para crear *wireframes*, *mockups* y *prototipos interactivos*, validando las propuestas de diseño antes de su implementación, con principios de usabilidad y diseño centrado en el usuario.

**Enlace:** [Figma](https://www.figma.com/)

**Software Development**

| Componente | Tecnología | Herramienta |
|---|---|---|
| Aplicación web | Vue 3, JavaScript, Vite, Vue Router, Pinia, Axios, PrimeVue, vue-i18n y Three.js | Node.js y npm |
| Backend (microservicios) | C# y ASP.NET Core (.NET 9), Entity Framework Core, Swagger (Swashbuckle) | JetBrains Rider |
| Base de datos | MySQL alojada en filess.io (una sola base compartida; cada servicio usa sus propias tablas e historial de migraciones) | Contenedor `migrate` |
| Mensajería asíncrona | Apache ActiveMQ Classic 5.18 | Consola web (puerto 8161) |
| Gateway | Nginx 1.25 (reverse proxy) | Configuración en `deploy/nginx/nginx.conf` |
| Asistente inteligente | Servicio Concierge con la API de DeepSeek (opcional, con respaldo si no hay clave) | Variable `DEEPSEEK_API_KEY` |
| Contenedores | Docker y Docker Compose v2 | Docker Desktop |
| Aplicación móvil del staff | Kotlin (Android nativo) | Android Studio |
| Aplicación móvil del huésped | Flutter | Android Studio |
| Autenticación y notificaciones móviles | Firebase | Consola de Firebase |
| Autenticación de la API | JWT emitido por el servicio IAM | — |

La instalación y el mantenimiento de los IDE se realizaron con **JetBrains Toolbox**. Para ejecutar el backend no es necesario instalar .NET ni MySQL en el equipo, porque todo se compila dentro de Docker.

**Enlaces:** [JetBrains Toolbox](https://www.jetbrains.com/toolbox-app/) · [Rider](https://www.jetbrains.com/rider/) · [Android Studio](https://developer.android.com/studio) · [Flutter](https://flutter.dev/) · [Kotlin](https://kotlinlang.org/) · [Firebase](https://firebase.google.com/) · [MySQL](https://www.mysql.com/) · [Docker](https://www.docker.com/) · [Nginx](https://nginx.org/) · [ActiveMQ](https://activemq.apache.org/)

**Software Documentation**

La documentación se redactó en formato **Markdown (.md)** dentro de los repositorios, siguiendo GitFlow. Los endpoints de cada microservicio se documentan con Swagger mediante las anotaciones `[SwaggerOperation]` y `[SwaggerResponse]`. Los diagramas de arquitectura se escriben en Structurizr DSL, PlantUML y DBML.

**Software Testing**

El cliente web usa el runner incluido en [Node.js](https://nodejs.org/). Las pruebas de backend se ejecutan con el SDK de [.NET](https://dotnet.microsoft.com/download), y la prueba de humo se dirige al gateway de un entorno de demostración. Las comprobaciones de navegación se realizan en el navegador, registrando la vista, el rol y el resultado observado.

**Software Deployment**

El backend se ejecuta con **Docker Compose** (detalle en 7.1.4). Las aplicaciones móviles se ejecutan y validan con el **emulador de Android Studio** y dispositivos físicos Android.

---

### 7.1.2. Source Code Management

**Repositorios del proyecto**

El proyecto está organizado en una **organización de GitHub**, donde cada módulo tiene su propio repositorio.

| Componente | Tecnología | Repositorio | Despliegue |
|---|---|---|---|
| Aplicación móvil | Kotlin (Android nativo) | https://github.com/Movil-dev-Aplicaciones-Moviles/smartstay-application-mobile | Android Studio Emulator / APK de pruebas |
| Aplicación web | Vue 3 y Vite | ZIP `frontend-web-main.zip`. URL del repositorio por confirmar con el equipo. | Vite local y compilación estática en `dist/` |
| Backend (Web Services) | ASP.NET Core (.NET 9), microservicios | https://github.com/Movil-dev-Aplicaciones-Moviles/application-mobile-backend | Docker Compose |
| Landing Page | HTML, CSS, JavaScript | https://github.com/Movil-dev-Aplicaciones-Moviles/landing-page | GitHub Actions / GitHub Pages |

El informe documenta **GitFlow** como modelo de trabajo del equipo. Para la entrega se deben vincular los commits, ramas y Pull Requests del frontend desde su repositorio. Los ZIP no incluyen historial Git.

**Estructura de la aplicación web**

`src/` agrupa el código por dominio, entre ellos IAM, Accommodations, Bookings, Payments, Profiles, Analytics y Concierge. El código común reside en `src/shared/` y `src/router.js` centraliza rutas y control de acceso. `package.json` define los scripts y `tests/integration.test.js` reúne las pruebas disponibles. El archivo `package-lock.json` mencionado en el README no figura en el ZIP recibido. Conviene recuperarlo desde el repositorio antes de usar `npm ci`.
| Backend (Web Services) | ASP.NET Core (.NET 9), microservicios | https://github.com/Movil-dev-Aplicaciones-Moviles/application-mobile-backend | Docker Compose |
| Landing Page | HTML, CSS, JavaScript | https://github.com/Movil-dev-Aplicaciones-Moviles/landing-page | GitHub Actions / GitHub Pages |

Todos los repositorios siguen el modelo **GitFlow**.

**Estructura del repositorio backend**

```text
backend/
├── compose.microservices.yml     # Orquestación de todos los contenedores
├── backend-aw-smartstay.sln      # Solución .NET
├── .env.example                  # Plantilla de variables (el .env real no se versiona)
├── .github/workflows/            # Construcción y publicación de imágenes Docker
├── contracts/                    # Contratos HTTP y constantes compartidas
├── src/Services/                 # Un proyecto por microservicio, cada uno con su Dockerfile
│   ├── SmartStay.IAM/
│   ├── SmartStay.Accommodations/
│   ├── SmartStay.Bookings/
│   ├── SmartStay.Payments/
│   ├── SmartStay.Profiles/
│   ├── SmartStay.Analytics/
│   └── SmartStay.Concierge/
├── tests/                        # Pruebas unitarias
├── tools/                        # Migración (SmartStay.Database), seed, smoke y verificación de fronteras
├── deploy/nginx/nginx.conf       # Configuración del gateway
├── client-templates/             # Plantillas de clientes
└── docs/                         # Documentación y ADR
```

**Flujo de trabajo GitFlow**

El flujo se basa en el modelo "A Successful Git Branching Model", con ramas específicas para cada funcionalidad o corrección.

**Diagrama del flujo GitFlow:**

```text
main (producción)
 |
 |---- release/v1.0.0
 |          |
develop    |
 |         |
 |---- feature/user-authentication
 |         |
 |         (desarrollo)
 |         |
 |<-------- (merge)
 |
 |---- feature/room-management
 |         |
 |         (desarrollo)
 |         |
 |<-------- (merge)
 |
 |---- hotfix/critical-bug
 |         |
 |         (corrección)
 |         |
 |<-------- (merge a develop)
 |         |
main <---- (merge a main)
```

**Proceso de trabajo:**

1. **Nuevas funcionalidades:** se crea `feature/<nombre>` desde `develop`, se desarrolla y prueba, y se fusiona a `develop` mediante Pull Request con revisión de código. La rama se elimina tras integrarse.
2. **Preparación de versiones:** se crea `release/<versión>` desde `develop`, se hacen ajustes finales, se fusiona a `main`, se etiqueta la versión y se sincroniza de vuelta con `develop`.
3. **Correcciones críticas:** se crea `hotfix/<descripción>` desde `main`, se corrige, se fusiona a `main` y `develop` y se etiqueta la nueva versión.

**Estructura de ramas:**

- **`main`:** código estable y listo para producción. Solo recibe cambios validados y está protegida con revisión obligatoria.
- **`develop`:** rama de integración donde se combinan y prueban las funcionalidades antes de pasar a `main`.
- **`feature/*`:** una rama por funcionalidad, por ejemplo `feature/chapter-01` a `feature/chapter-05` (documentación), `feature/user-authentication`, `feature/room-management` y `feature/booking-system`.
- **`release/*`:** por ejemplo `release/v1.0.0` y `release/v1.1.0`.
- **`hotfix/*`:** por ejemplo `hotfix/login-security` y `hotfix/payment-error`.

**Evidencia de aplicación de GitFlow:**

- **Mobile App:** ramas `main`, `develop`, `feature/responsive-design` y `feature/multilanguage`; commits con `feat:`, `fix:` y `docs:`; Pull Requests con revisión de código.
- **Backend:** ramas `main`, `develop`, `feature/api-rooms` y `feature/api-bookings`; versionado semántico con tags `v1.0.0` y `v1.1.0`.

Para los mensajes de commit, el equipo aplica Conventional Commits con la forma `tipo(alcance): descripción`. Por ejemplo, `docs(ux): documentar flujo de reservas` para documentación y `fix(bookings): mostrar estado de la reserva` para correcciones. Estos mensajes son ejemplos de la convención. Las versiones usan `vMAJOR.MINOR.PATCH` conforme a versionado semántico.

**Archivos excluidos del control de versiones**

El archivo `.env` contiene la cadena de conexión a MySQL y otros secretos, por lo que está en `.gitignore` y se excluye de los contextos Docker. En el repositorio solo existe `.env.example` como plantilla. Los secretos no se suben a Git ni se muestran en capturas del informe.

**Integración continua con GitHub Actions**

El workflow `Docker` (`.github/workflows/docker-publish.yml`) construye y publica las imágenes de los microservicios:

| Aspecto | Configuración |
|---|---|
| Disparadores | `push` a `main`, tags `v*.*.*`, `pull_request` hacia `main` y ejecución diaria programada (`cron: 27 3 * * *`) |
| Estrategia | Matriz de 7 servicios en paralelo: Accommodations, Analytics, Bookings, Concierge, IAM, Payments y Profiles |
| Construcción | Docker Buildx con el `Dockerfile` de cada servicio (`src/Services/SmartStay.<Servicio>/Dockerfile`) y caché de GitHub Actions |
| Registro | GitHub Container Registry (`ghcr.io`), solo cuando el evento no es un Pull Request |
| Firma | Las imágenes publicadas se firman con cosign |

En un Pull Request el workflow solo comprueba que las imágenes compilen, sin publicarlas. Nginx y ActiveMQ usan imágenes públicas y `migrate` se construye localmente, por lo que no forman parte de la matriz.

**Verificaciones de calidad**

Las pruebas del cliente se ejecutan con el runner nativo de Node. En la revisión de este ZIP se ejecutaron `npm test` (13 pruebas aprobadas) y `npm run build` (compilación correcta, con aviso de tamaño de algunos bloques JavaScript). Las pruebas de contrato y los recorridos con respuestas simuladas se registran como evidencia de esos entornos. El despliegue y las operaciones de negocio con servicios reales requieren evidencia independiente.

El backend entregado incluye proyectos de pruebas .NET y un script de humo. El enunciado solicita también archivos de prueba `.feature` para Web Services. Esos archivos no se encontraron en el ZIP revisado y se deben recuperar o incorporar desde el repositorio correspondiente.


```bash
dotnet test backend-aw-smartstay.sln -c Release   # Pruebas unitarias
bash tools/check-boundaries.sh                    # Verifica que ningún microservicio viole las fronteras arquitectónicas
bash tools/smoke-mvp.sh                           # Prueba de humo end-to-end de 13 pasos
```

---

### 7.1.3. Source Code Style Guide & Conventions

El equipo adopta convenciones de nomenclatura y guías de estilo estandarizadas para mantener la coherencia, legibilidad y escalabilidad del código. Variables, funciones, clases y archivos se nombran en **inglés**, según las convenciones de cada lenguaje.

**Kotlin (Android Studio)**

Referencias: [Kotlin Coding Conventions](https://kotlinlang.org/docs/coding-conventions.html) y [Android Kotlin Style Guide](https://developer.android.com/kotlin/style-guide).

- **PascalCase** para clases y actividades (`LoginActivity`, `RoomManagementActivity`).
- **camelCase** para variables, funciones y parámetros (`guestName`, `validateLogin()`).
- Organización modular por paquetes (`activities`, `services`, `models`, `adapters`).
- Nombres descriptivos y consistentes para layouts XML y recursos visuales.

Componentes utilizados: `Activity`, `Fragment`, `RecyclerView`, `Intent`, `ViewModel`, Firebase y layouts XML.

**C# y ASP.NET Core (backend)**

Referencias: [C# Coding Conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions) y [ASP.NET Core fundamentals](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/).

| Elemento | Convención | Ejemplo |
|---|---|---|
| Clases, interfaces (prefijo `I`), métodos públicos | PascalCase | `RoomsController`, `IRoomQueryService` |
| Variables locales y parámetros | camelCase | `roomId`, `hotelQueryService` |
| Namespaces | `SmartStay.<Servicio>.<Capa>` | `SmartStay.Accommodations.Interfaces.REST` |
| Controladores | Sufijo `Controller` y ruta `api/v1/[controller]` | `HotelsController` → `/api/v1/hotels` |
| DTOs | `record` con sufijo `Resource` | `CreateHotelResource`, `HotelResource` |
| Comandos y consultas | Prefijo de intención | `CreateHotelCommand`, `GetHotelByIdQuery` |
| Conversión entre capas | Clases `...Assembler` | `HotelResourceFromEntityAssembler` |

Cada servicio se organiza por capas (`Domain`, `Application`, `Infrastructure` e `Interfaces`). Los controladores solo traducen HTTP a comandos y consultas, sin reglas de negocio. Cada endpoint declara su autorización por rol (`Guest`, `Admin`, `ChainAdmin`) y se documenta con Swagger. Los comentarios XML documentan los controladores públicos.

**Reglas de arquitectura:**

- Cada servicio tiene su propio `DbContext` y sus propias tablas; ninguno accede al `DbContext` de otro.
- Los servicios se comunican por HTTP con contratos (`contracts/`) o por eventos en ActiveMQ.
- El código compartido se limita a contratos y constantes, nunca entidades ni repositorios.
- Los importes usan `decimal` y los precios los calcula el servidor, nunca el cliente.
- Las consultas SQL usan parámetros, sin concatenación de cadenas.
- El script `tools/check-boundaries.sh` verifica estas fronteras automáticamente.

**JavaScript y Vue**

La aplicación web utiliza componentes de archivo único `.vue`, con `<script setup>` en las vistas revisadas. Los nombres de archivo usan minúsculas y guiones, como `booking-form.vue`. Las funciones y variables se nombran en camelCase. La presentación, las reglas del dominio y el acceso HTTP se ubican en carpetas diferenciadas. Los textos de interfaz se centralizan en `src/locales/es.json` y `src/locales/en.json`. La comprobación disponible se ejecuta con `npm test` y `npm run build`.

**Buenas prácticas comunes**

- Nomenclatura en inglés.
- Principio **DRY** (*Don't Repeat Yourself*): evitar duplicación de código.
- Principio **KISS** (*Keep It Simple, Stupid*): priorizar soluciones simples y claras.
- Código documentado y con convenciones homogéneas entre la aplicación móvil y el backend.
- Formato automatizado mediante linters y herramientas de formateo de cada entorno.
- Commits con prefijos `feat:`, `fix:` y `docs:`, y revisión de código mediante Pull Request.

---

### 7.1.4. Software Deployment Configuration

El despliegue considera los aspectos que garantizan la disponibilidad y correcta operación de los componentes del sistema.

**Backend (Web Services)**

El backend se ejecuta con **Docker Compose** a partir del archivo `compose.microservices.yml`. Solo la base de datos MySQL está alojada de forma remota (filess.io); los demás componentes corren como contenedores.

```text
Clientes (app Android, app Flutter, web)
        │
        ▼
Nginx Gateway (puerto 8080)  ← único puerto publicado
        │
        ├── /api/v1/authentication, /api/v1/users     → IAM
        ├── /api/v1/rooms, /api/v1/hotels, /tours     → Accommodations
        ├── /api/v1/bookings                          → Bookings
        ├── /api/v1/payments                          → Payments
        ├── /api/v1/profiles                          → Profiles
        ├── /api/v1/analytics                         → Analytics
        └── /api/v1/concierge                         → Concierge ──▶ API de DeepSeek

Bookings, Payments y Analytics  ⇄  ActiveMQ
Servicios con persistencia      ⇄  MySQL (filess.io)
```

**Contenedores definidos:**

| Servicio | Imagen o construcción | Función |
|---|---|---|
| `migrate` | `tools/SmartStay.Database/Dockerfile` | Crea o actualiza los esquemas y siembra datos; termina al finalizar |
| `activemq` | `apache/activemq-classic:5.18.3` | Broker de mensajería (puertos 61616 y 8161) con volumen persistente `activemq_data` |
| `gateway` | `nginx:1.25-alpine` | Punto de entrada único; monta `deploy/nginx/nginx.conf` |
| `iam`, `accommodations`, `bookings`, `payments`, `profiles`, `analytics`, `concierge` | `src/Services/SmartStay.<Servicio>/Dockerfile` | Microservicios .NET 9 en el puerto interno 8080 |

Los microservicios usan `expose` (accesibles solo dentro de la red de Docker); únicamente el gateway publica un puerto. Todos tienen `healthcheck` y dependencias declaradas con `depends_on`. El orden de arranque es: `migrate`, luego `activemq` e `iam`, después el resto de servicios y por último el gateway. Concierge no usa base de datos.

**Variables de configuración (`.env`):**

| Variable | Obligatoria | Descripción |
|---|---|---|
| `MYSQL_CONNECTION_STRING` | Sí | Cadena de conexión a filess.io (conservar `SslMode=Required;Pooling=false;`) |
| `JWT_SECRET`, `JWT_ISSUER`, `JWT_AUDIENCE`, `JWT_EXPIRATION_HOURS` | No | Tienen valor por defecto; el secreto debe cambiarse fuera de la demostración |
| `ACTIVEMQ_USER`, `ACTIVEMQ_PASSWORD` | No | Credenciales del broker |
| `GATEWAY_PORT` | No | Puerto del gateway (por defecto 8080) |
| `DEEPSEEK_API_KEY`, `DEEPSEEK_MODEL` | No | Clave y modelo de DeepSeek; sin clave, Concierge responde con un respaldo |

En una instalación nueva se copia `.env.example` a `.env` y se completa la cadena de conexión.

**Requisitos previos:** Docker Desktop con contenedores Linux y Docker Compose v2, una base MySQL en filess.io y conexión a Internet.

**Instalación inicial (base nueva):**

```powershell
docker compose -f compose.microservices.yml config --quiet
docker compose -f compose.microservices.yml build migrate
docker compose -f compose.microservices.yml run --rm migrate check
docker compose -f compose.microservices.yml run --rm migrate migrate
docker compose -f compose.microservices.yml run --rm migrate seed
docker compose -f compose.microservices.yml up --build -d
docker compose -f compose.microservices.yml restart gateway
docker compose -f compose.microservices.yml ps
```

Las migraciones se ejecutan una por servicio y de forma secuencial, nunca en paralelo. El comando `seed` prepara datos de demostración. Ejecutarlo en una base destinada a la demo y registrar la revisión del repositorio utilizada. El backend incluye la migración `20261109000000_AddRoomLayout` de Accommodations.
Las migraciones se ejecutan una por servicio y de forma secuencial, nunca en paralelo. El comando `seed` agrega usuarios de demostración sin borrar datos existentes.

**Arranque diario** (imágenes ya construidas y base inicializada):

```powershell
docker compose -f compose.microservices.yml up -d --no-deps --no-build --wait activemq iam accommodations bookings payments profiles analytics concierge
docker compose -f compose.microservices.yml up -d --no-deps --no-build gateway
docker compose -f compose.microservices.yml restart gateway
```

Se reinicia el gateway porque Nginx guarda en memoria las direcciones internas de los servicios, que cambian al recrear contenedores.

**Verificación y apagado:**

```powershell
Invoke-RestMethod 'http://localhost:8080/health'
Invoke-RestMethod 'http://localhost:8080/api/v1/rooms/search?district=Lima&guests=2'
docker compose -f compose.microservices.yml stop
```

Al detener los contenedores se conservan el volumen de ActiveMQ y los datos remotos de MySQL.

**Exposición pública para demostraciones.** Para que las aplicaciones móviles en otras redes accedan al backend se usa un túnel **Cloudflare Quick Tunnel** que apunta únicamente al gateway:

```powershell
& 'C:\Program Files (x86)\cloudflared\cloudflared.exe' tunnel --url http://localhost:8080
```

La dirección `https://<nombre-aleatorio>.trycloudflare.com` cambia en cada ejecución, por lo que se actualiza la URL base de las aplicaciones cliente. Nunca se exponen MySQL, ActiveMQ ni las APIs individuales.

**Validación del despliegue.** La prueba `bash tools/smoke-mvp.sh` ejecuta 13 pasos: salud del gateway, autenticación, catálogo de habitaciones, recomendaciones de Concierge, creación de reservas, consulta de reservas propias, aislamiento entre huéspedes (HTTP 403), alcance de administradores por hotel (HTTP 403) y cancelación con liberación del inventario.

| Usuario de prueba | Rol | Ámbito |
|---|---|---|
| `admin` | `admin` | Hotel Bolívar (Lima) |
| `admin_cusco` | `admin` | Cusco Andean Lodge |
| `chain_admin` | `chain_admin` | Toda la cadena |
| `guest1`, `guest2` | `guest` | Huéspedes |

Las contraseñas de demostración se entregan fuera del informe.

**Web Application Deployment**

El cliente se prepara en un entorno Node compatible con el proyecto y se conecta al gateway mediante `VITE_MOVILDEV_API_URL`. El valor es el origen HTTP o HTTPS, sin el sufijo `/api/v1`, que el cliente añade. Los archivos de entorno de Vite contienen configuración pública y se incorporan al build. Las claves de DeepSeek y las credenciales de infraestructura corresponden al backend.

1. En la raíz del frontend, instalar dependencias con `npm install`, o con `npm ci` si se recupera el lockfile del repositorio.
2. Configurar el origen del gateway en `.env.development.local` y ejecutar `npm run dev`. Para una prueba local, usar `http://localhost:8080` si coincide con el puerto del gateway.
3. Ejecutar `npm test` y `npm run build`. Configurar el origen de producción antes de compilar.
4. Publicar el contenido de `dist/` en un alojamiento estático y configurar el retorno de `index.html` para las rutas de Vue Router, como `/catalog`. Si la web se sirve por HTTPS, usar también un gateway HTTPS.
5. Verificar el catálogo y las rutas privadas desde el origen publicado. Si se utiliza el túnel temporal, mantener el gateway activo y reconstruir el frontend cuando cambie la URL.

El README del frontend registra pruebas unitarias y compilación, consultas públicas al gateway real y flujos de navegador con respuestas simuladas. La prueba con cuentas reales de demostración y el enlace de despliegue web definitivo quedan por confirmar. El ZIP web no incluye un workflow de publicación.

**Mobile Application Deployment**

Las aplicaciones móviles se desarrollan con **Android Studio**: la del staff en **Kotlin** (Android nativo) y la del huésped en **Flutter**.

1. **Preparación del entorno:** SDK de Android, emuladores y dependencias de compilación configurados en Android Studio.
2. **Estructura del proyecto Kotlin:**
   - `activities/`: pantallas principales.
   - `adapters/`: listas dinámicas y `RecyclerView`.
   - `models/`: entidades y estructuras de datos.
   - `services/`: conexión con las APIs REST.
   - `res/layout/`: interfaces XML.
   - `assets/`: recursos gráficos.
3. **Compilación y ejecución:** se ejecutan en el emulador y en dispositivos físicos. Android Studio genera los APK de prueba (`./gradlew :app:assembleDebug`) y se instalan con `adb install`. Las versiones se administran con GitHub y GitFlow.
4. **Servicios integrados:** consumo de las APIs RESTful a través del gateway (URL local o del túnel) y Firebase para autenticación y notificaciones.

**Evidencia por incorporar:** captura de la app móvil en el emulador o un dispositivo de prueba.
![Android Studio Emulator](assets/Chapter-IIII//android-studio-emulator.jpg)

*El emulador de Android Studio permite validar la aplicación móvil en distintos dispositivos y versiones de Android antes de su despliegue final.*

**Landing Page**

La Landing Page se despliega con **GitHub Actions** en GitHub Pages: https://movil-dev-aplicaciones-moviles.github.io/landing-page/

**Integración y despliegue continuo (CI/CD)**

- Todos los repositorios están conectados a **GitHub** y siguen GitFlow.
- En el backend, GitHub Actions construye las imágenes de los siete microservicios y las publica en `ghcr.io` al integrar en `main` o al etiquetar una versión.
- En la Landing Page, GitHub Actions publica el sitio al fusionar en `main`.
- Las versiones móviles se compilan y prueban desde Android Studio antes de cada entrega.

**Limitaciones conocidas**

- IoT para domótica está definido como diseño en el capítulo IV. La integración con un gateway IoT y la prueba de comandos y telemetría quedan pendientes en la versión entregada. ActiveMQ documenta mensajería entre servicios.
- El código entregado no aporta evidencia de un componente Web3 desplegado. El visor disponible es una experiencia 3D/360° en el navegador.


- La base MySQL gratuita de filess.io tiene límites de espacio y conexiones, por lo que se usan pocos datos, una instancia por API y `Pooling=false`.
- Una sola base y credenciales compartidas son una simplificación académica; en producción cada servicio tendría su propia base.
- El túnel de Cloudflare es temporal y adecuado para demostraciones, no para producción.

### 7.2.1. Sprint 1

#### 7.2.1.1. Sprint Planning 1.

A través de una reunión en la plataforma Discord, se planteó el inicio del Sprint 1. Durante la sesión se discutieron los objetivos principales, el cronograma de trabajo y la distribución de tareas para el desarrollo de la presencia digital de la startup.

| Sprint #                         | Sprint 1                                                                                                                                                                                          |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Sprint Planning Background**   |                                                                                                                                                                                                   |
| Date                             | 2026-10-19                                                                                                                                                                                        |
| Time                             | 09:30 pm (GMT-5)                                                                                                                                                                                  |
| Location                         | Modalidad remota mediante la plataforma Discord                                                                                                                                                   |
| Prepared By                      | Howard Robles, Guillermo Arturo                                                                                                                                                                   |
| Attendees (to planning meeting)  | Arévalo Meza, John Telesforo <br /> Howard Robles, Guillermo Arturo <br /> Santur Tello, Andrea Elizabeth <br /> Verona Flores, Ítalo Sebastián <br />|
| Sprint n-1 Review Summary        | No hubo sprint anterior                                                                                                                                                                           |
| Sprint n-1 Retrospective Summary | No hubo sprint anterior                                                                                                                                                                           |
| **Sprint Goal & User Stories**   |                                                                                                                                                                                                   |
| Sprint 1 Goal                    | Entregar una primera versión de la landing page de SmartStay para que los administradores de hoteles y los huéspedes puedan conocer los beneficios de la plataforma según su perfil, consultar casos de éxito e información de la empresa, y solicitar una demostración o contactar al equipo comercial.                                                                                                                                                                                                 |
| Sprint 1 Velocity                | 15                                                                                                                                                                                                  |
| Sum of Story Points              | 15                                                                                                                                                                                                 |

#### 7.2.1.2. Sprint Backlog 1.

| ID | Historia de usuario | Story Points |
|---|---|---:|
| US-24 | Como visitante, quiero encontrar información según mi perfil de administrador de hotel o huésped para entender los beneficios de SmartStay. | 5 |
| US-26 | Como visitante interesado, quiero consultar casos de éxito y testimonios de hoteles para evaluar cómo SmartStay puede aportar a la operación hotelera. | 5 |
| US-27 | Como visitante interesado, quiero solicitar una demostración y contactar al equipo comercial para conocer mejor la plataforma. | 3 |
| US-28 | Como visitante, quiero conocer la misión, la visión y los valores de SmartStay para entender la filosofía de la empresa. | 2 |
| | **Sum of Story Points** | **15** |


| Work-item / Task | Description | Estimation (hours) |
|---|---|---:|
| US24-01 | Definir los beneficios y las llamadas a la acción para administradores de hoteles y huéspedes. | 2 |
| US24-02 | Implementar la navegación y las secciones de beneficios por perfil en la landing page. | 3 |
| US24-03 | Verificar en escritorio y móvil que ambos perfiles encuentren su sección en menos de tres clics. | 2 |
| US26-01 | Seleccionar y redactar los casos de éxito y testimonios con contenido validado por el equipo. | 2 |
| US26-02 | Implementar la sección de casos de éxito y testimonios con tarjetas adaptables. | 2 |
| US26-03 | Verificar que las tarjetas se lean correctamente en escritorio y móvil. | 1 |
| US27-01 | Implementar el botón «Solicitar demo» y el formulario de contacto comercial. | 2 |
| US27-02 | Validar los campos obligatorios y mostrar mensajes de confirmación y error. | 2 |
| US27-03 | Probar el envío al canal comercial configurado y comprobar la respuesta al visitante. | 1 |
| US28-01 | Redactar el contenido de misión, visión y valores. | 1 |
| US28-02 | Implementar la sección «Sobre nosotros» y enlazarla desde la navegación o el pie de página. | 1 |
| US28-03 | Verificar que el enlace funcione y que el contenido sea legible en móvil. | 1 |
| | **Total de horas estimadas** | **20** |

#### 7.2.1.3. Development Evidence for Sprint Review.

***Backend***

Cambios en los microservicios, la base de datos, el entorno Docker y las integraciones del backend.

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
|---|---|---|---|---|---|
| backend | main | [`67323de`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/67323dec1766d0fb8e46b6579f72571d4d0a9349) | Merge branch 'release/0.2.1' into main | Integración de la rama de publicación `release/0.2.1` en `main`. | 11/11/2026 |
| backend | main | [`e308b39`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/e308b39f2bed003bef0042c54aa255c1351f6a11) | feat(sln): add new project for smartstay.database and configure build settings. | Incorporación de `SmartStay.Database` a la solución y configuración de su compilación. | 11/11/2026 |
| backend | main | [`1b7e2d5`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/1b7e2d534137ad316b46d15659d0facbd64bb4a3) | feat(database): add separate inbox tables for bookings, payments, and analytics. | Creación de tablas inbox separadas para Bookings, Payments y Analytics. | 11/11/2026 |
| backend | main | [`dd188e5`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/dd188e5875102dc1f1990efa05bf392d9e3354e5) | Merge pull request #4 from 1ASI0728-9077-SmartStay-Movildev/develop | Integración de los cambios de `develop` mediante el PR #4. | 11/11/2026 |
| backend | main | [`6d91c99`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/6d91c9988592b5df71f4022d2fb8e0e473d39f99) | Merge pull request #3 from 1ASI0728-9077-SmartStay-Movildev/feature/deployment | Integración de `feature/deployment` mediante el PR #3. | 11/11/2026 |
| backend | main | [`62da73b`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/62da73b23eb7e7d2b0219231a6563e89774df34b) | docs: update readme with demo setup instructions for smartstay and cloudflare tunnel installation. | Actualización del README con los pasos para preparar la demo e instalar Cloudflare Tunnel. | 11/11/2026 |
| backend | main | [`bee2f3f`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/bee2f3f57e22db1f1989a369e6d72c46bffe470b) | refactor(database): rename inbox message tables and update connection string handling for payments and accommodations. | Renombrado de tablas inbox y ajustes en las cadenas de conexión de Payments y Accommodations. | 11/11/2026 |
| backend | main | [`03b7933`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/03b7933f2d7177c2c6296437e08cb1407b6a7362) | refactor(config): clear connection strings in appsettings.json for security. | Retiro de las cadenas de conexión de `appsettings.json`. | 11/11/2026 |
| backend | main | [`0d50840`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/0d5084058712ccdf1025e737af093f9f68f12ef4) | refactor(database): update connection string handling and table naming conventions for accommodations and analytics. | Ajustes en el manejo de conexiones y en los nombres de tablas de Accommodations y Analytics. | 11/11/2026 |
| backend | main | [`cfb456a`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/cfb456af3e46e912fa172826f0a02faa26b7fd7e) | refactor(docker): update mysql service configuration and remove migration scripts. | Actualización de MySQL en Docker y retiro de scripts de migración. | 11/11/2026 |
| backend | main | [`c18f739`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/c18f739dd5f9f290436690f50a3fd6b413f5ef53) | Merge branch '3d-model' into develop | Integración de la rama `3d-model` en `develop`; el commit forma parte del historial de `main`. | 11/11/2026 |
| backend | main | [`6178666`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/6178666bc14699723ee3b671b3580194100df98d) | fix(accommodations): corrige spawn de la escena VR | Corrección del punto de aparición del usuario en la escena de realidad virtual. | 10/11/2026 |
| backend | main | [`41a52ac`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/41a52ac35c819baef904b0c9c40866927f8c4158) | feat: complete room layout validation and VR support | Finalización de la validación de la distribución de habitaciones y del soporte de realidad virtual. | 09/11/2026 |
| backend | main | [`7fd2b55`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/7fd2b557674ceb64ab3f0a643c91a2b5a3970b54) | feat(frontend): add Vue 3D room designer template | Incorporación de una plantilla Vue para diseñar habitaciones en 3D. | 08/11/2026 |
| backend | main | [`afd4cee`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/afd4cee4a532acacd885167252601c64e50d835b) | feat(api): expose room layout and VR endpoints | Exposición de endpoints para la distribución de habitaciones y las vistas de realidad virtual. | 08/11/2026 |
| backend | main | [`dbb0672`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/dbb0672dbfd0e5d9531eed93b3c97830ea91f155) | feat(accommodations): add layout validation and VR contracts | Incorporación de validaciones de la distribución y contratos para realidad virtual. | 08/11/2026 |
| backend | main | [`0e0dba8`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/0e0dba8dd953dbf201d6350229296435763185d9) | feat(accommodations): persist room layout metadata | Persistencia de los metadatos de la distribución de las habitaciones. | 08/11/2026 |
| backend | main | [`85cbcd7`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/85cbcd7ed905865f7e4abe85dc6e40796e53493e) | first commit | Actualización de una línea del README. | 04/11/2026 |
| backend | main | [`8aa142e`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/8aa142ef75897527a7960491e698b4d6281bbf10) | fix(infra): update docker healthchecks, fix publish --no-restore, BOM in SQL, and HTTP 403 authorization | Correcciones en los chequeos de salud de Docker, la publicación con `--no-restore`, el BOM de SQL y la autorización HTTP 403. | 02/11/2026 |
| backend | main | [`b09f0cb`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/b09f0cb2a4dcff0ce37298203f8230aff19fb717) | fix(security): resolve audit vulnerabilities in payments atomicity, IAM session revocation, tenant boundaries and secrets | Correcciones de auditoría en atomicidad de pagos, revocación de sesiones de IAM, aislamiento entre hoteles y manejo de secretos. | 02/11/2026 |
| backend | main | [`140e2ca`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/140e2ca941f645d9bc1f12719e14ca876841791c) | fix(mvp): close all feedback gaps in Concierge truth, Bookings concurrency and permissions, 360 tour, Nearby P2P and smoke E2E | Correcciones en Concierge, concurrencia y permisos de reservas, recorrido 360°, Nearby P2P y pruebas de extremo a extremo. | 27/10/2026 |
| backend | main | [`4f4249c`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/4f4249c10494453014f88a23d3a9e457b90541e5) | feat(mvp): complete Concierge microservice, 360 tour assets, Nearby Android templates and smoke verification | Finalización de Concierge, recursos para recorridos 360°, plantillas Nearby de Android y pruebas de humo. | 27/10/2026 |
| backend | main | [`9efb8f0`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/9efb8f0f5de4c13ebcc07e2518a0d60cbe0080e8) | feat(core): complete Phase 1 reliable core, room search, availability check, ownership enforcement and reservation expiration | Incorporación de búsqueda de habitaciones, consulta de disponibilidad, verificación de titularidad y vencimiento de reservas. | 27/10/2026 |
| backend | main | [`1bd34a1`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/1bd34a105cfa0b844a140aaca20b73f54a837901) | chore(mvp): complete Phase 0 baseline, cleanup manifest, domain tests porting and monolith retirement | Preparación de la base del MVP, limpieza del manifiesto, traslado de pruebas de dominio y retiro del monolito. | 27/10/2026 |
| backend | main | [`0d0883b`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/0d0883bd5040dec5ce50232872739bfdc18d8e2a) | feat(ops): complete Phase 9 monolith decommissioning, operations runbook, compose healthchecks and migrations automation | Retiro del monolito, guía de operaciones, chequeos de salud en Compose y automatización de migraciones. | 26/10/2026 |
| backend | main | [`7ddc1b4`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/7ddc1b48c6e323c28dd3463504086375709885ec) | feat(analytics): complete Phase 8 extraction of SmartStay.Analytics, autonomous projections, migrations and gateway routing | Separación de Analytics como microservicio con proyecciones autónomas, migraciones y rutas en el gateway. | 26/10/2026 |
| backend | main | [`346098b`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/346098bca604fd09b3c1d7fda86510eef12a157d) | feat(iam): complete Phase 7 extraction of SmartStay.IAM, internal token verification, tests and gateway routing | Separación de IAM como microservicio con verificación interna de tokens, pruebas y rutas en el gateway. | 26/10/2026 |
| backend | main | [`2c59b85`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/2c59b851659b76c72ce550d02fabb58de4e873d8) | feat(profiles): complete Phase 6 extraction of SmartStay.Profiles, migrations, tests and gateway routing | Separación de Profiles como microservicio con migraciones, pruebas y rutas en el gateway. | 26/10/2026 |
| backend | main | [`8dcd954`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/8dcd95471add5e557c822fdba45b4b4b1c89879a) | feat(payments): complete Phase 5 extraction of SmartStay.Payments, outbox/inbox messaging, idempotency, saga and gateway routing | Separación de Payments como microservicio con mensajería outbox/inbox, idempotencia, saga y rutas en el gateway. | 26/10/2026 |
| backend | main | [`e79f2bd`](https://github.com/1ASI0728-9077-SmartStay-Movildev/backend/commit/e79f2bdb77eee7c8f98e398918b151724c8daee8) | feat(bookings): complete Phase 4 extraction of SmartStay.Bookings, physical night locks, tests and gateway routing | Separación de Bookings como microservicio con bloqueos por noche, pruebas y rutas en el gateway. | 26/10/2026 |

***Frontend web***

Integración de los módulos web con la API y publicación de la versión 0.2.1.

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
|---|---|---|---|---|---|
| frontend-web | main | [`8537005`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-web/commit/8537005a6e0e865f2cb65ee252eb03d4dec4022b) | Merge branch 'release/0.2.1' into main | Integración de la rama de publicación `release/0.2.1` en `main`. | 11/11/2026 |
| frontend-web | main | [`a3799a9`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-web/commit/a3799a996e4a1b4566f1e4953e9d279ef8701a96) | Merge pull request #1 from 1ASI0728-9077-SmartStay-Movildev/feature/menu | Integración de `feature/menu` mediante el PR #1. | 11/11/2026 |
| frontend-web | main | [`b245b7b`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-web/commit/b245b7b35718563e26ec7b08e2e5c7dd805e31c4) | docs: update readme.md with project setup, functionality, and validation details. | Actualización del README con la configuración, las funcionalidades y los pasos de validación. | 11/11/2026 |
| frontend-web | main | [`5992fc3`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-web/commit/5992fc3b60c513830351cc54261d1c58cbf24332) | feat(payments): add payment processing components with api integration for booking payments. | Incorporación de componentes e integración con la API para pagar reservas. | 11/11/2026 |
| frontend-web | main | [`38c8ce1`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-web/commit/38c8ce1c46e2f699dc4e67915fdeb1ed03dc62b5) | feat(profiles): add profile management components with api integration for user profiles. | Incorporación de componentes e integración con la API para gestionar perfiles. | 11/11/2026 |
| frontend-web | main | [`251e43d`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-web/commit/251e43d8d071b5ba6b3384a363b3ba1095053185) | feat(concierge): add chat functionality with request handling and api integration. | Incorporación del chat de Concierge y del manejo de solicitudes a la API. | 11/11/2026 |
| frontend-web | main | [`5e654e7`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-web/commit/5e654e7b360950ebc0810291166443e2e9068c9e) | feat(bookings): add booking detail, form, and listings components with api integration. | Incorporación del detalle, formulario y listado de reservas con integración a la API. | 11/11/2026 |
| frontend-web | main | [`0ca9ba8`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-web/commit/0ca9ba8c1fdf91568fdecaf36d763340fab64268) | feat(analytics): add analytics component and api integration for monthly performance metrics. | Incorporación de la vista de indicadores mensuales y su integración con la API. | 11/11/2026 |
| frontend-web | main | [`7e042d2`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-web/commit/7e042d2db560389327736b1fe6a08c47099b7bec) | feat: implement error normalization and http client setup for api requests. | Configuración del cliente HTTP y normalización de errores en las solicitudes a la API. | 11/11/2026 |
| frontend-web | main | [`476ba08`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-web/commit/476ba082cfc667c99a398986f90b6cf207ff720a) | feat(accommodations): add accommodations component and api integration for hotel and room listings. | Incorporación del listado de hoteles y habitaciones con integración a la API. | 11/11/2026 |

***Frontend móvil***

Implementación de la estructura inicial del MVP móvil y de las vistas 3D.

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
|---|---|---|---|---|---|
| frontend-movil | master | [`81a946c`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-movil/commit/81a946c72cde8ca4d548e27916dfa112b74ec778) | Merge pull request #2 from 1ASI0728-9077-SmartStay-Movildev/develop | Integración de `develop` en `master` mediante el PR #2. | 12/11/2026 |
| frontend-movil | master | [`1049dec`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-movil/commit/1049decac9b7326373479aa7d3354e0bcf65813f) | Merge pull request #1 from 1ASI0728-9077-SmartStay-Movildev/feature/3D-view | Integración de `feature/3D-view` mediante el PR #1. | 12/11/2026 |
| frontend-movil | master | [`0afd74b`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-movil/commit/0afd74baa96450133e8836381c162e7cb21f68c2) | feat: Add 3d views | Incorporación de las vistas 3D en la aplicación móvil. | 12/11/2026 |
| frontend-movil | master | [`b782fca`](https://github.com/1ASI0728-9077-SmartStay-Movildev/frontend-movil/commit/b782fcafa661bff2f6d95281f3cac949d845c8c0) | feat: First structure & mvp | Implementación de la estructura inicial de la aplicación móvil y su MVP. | 12/11/2026 |

#### 7.2.1.4. Testing Suite Evidence for Sprint Review.

No se realizaron pruebas unitarias ni de integración durante este sprint, ya que el enfoque principal fue establecer la base del proyecto y garantizar la funcionalidad esencial de la landing page y los módulos de IAM y Suscriptions. Las pruebas se planificarán para los próximos sprints, una vez que se hayan consolidado las funcionalidades básicas y se cuente con un entorno más estable para realizar pruebas exhaustivas.

#### 7.2.1.5. Execution Evidence for Sprint Review.

#### 7.2.1.6. Services Documentation Evidence for Sprint Review.

#### 7.2.1.7. Software Deployment Evidence for Sprint Review.

#### 7.2.1.8. Team Collaboration Insights during Sprint 1.

