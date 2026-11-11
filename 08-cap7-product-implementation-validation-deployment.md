<div style="page-break-before: always;"></div>

# Capítulo VII: Product Implementation, Validation, and Deployment.

## 7.1. Software Configuration Management

La gestión de configuración de Smart Stay define cómo se prepara el entorno de desarrollo, cómo se versiona el código, qué convenciones se siguen y cómo se construye, empaqueta y ejecuta la solución. El backend está compuesto por **siete microservicios en ASP.NET Core (.NET 9)**: IAM, Accommodations, Bookings, Payments, Profiles, Analytics y Concierge. Se ejecutan como contenedores Docker detrás de un gateway **Nginx**, con mensajería en **ActiveMQ** y persistencia en **MySQL**. Los clientes son una aplicación Android nativa (Kotlin) para el staff operativo y una aplicación Flutter para el huésped.

### 7.1.1. Software Development Environment Configuration

#### Project Management

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

![sprint_trello](assets/trello.jpg)
*Tablero Trello del Sprint 1 mostrando la organización de tareas*

![sprint_trello](assets/trello2.jpg)
*Tablero Trello del Sprint 2 con Engineering Tasks en progreso*

#### Requirement Management

Trello se usó para la gestión visual de tareas. **UXPressia** sirvió para elaborar *User Personas*, *Empathy Maps*, *Journey Maps* y *Lean UX Canvas*, y **Miro** para construir los escenarios *As-Is* y *To-Be*.

**Enlaces:** [Trello](https://trello.com/) · [UXPressia](https://uxpressia.com/) · [Miro](https://miro.com/es/)

#### Product UX/UI Design

El equipo utilizó **Figma** para crear *wireframes*, *mockups* y *prototipos interactivos*, validando las propuestas de diseño antes de su implementación, con principios de usabilidad y diseño centrado en el usuario.

**Enlace:** [Figma](https://www.figma.com/)

#### Software Development

| Componente | Tecnología | Herramienta |
|---|---|---|
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

#### Software Documentation

La documentación se redactó en formato **Markdown (.md)** dentro de los repositorios, siguiendo GitFlow. Los endpoints de cada microservicio se documentan con Swagger mediante las anotaciones `[SwaggerOperation]` y `[SwaggerResponse]`. Los diagramas de arquitectura se escriben en Structurizr DSL, PlantUML y DBML.

#### Software Deployment

El backend se ejecuta con **Docker Compose** (detalle en 7.1.4). Las aplicaciones móviles se ejecutan y validan con el **emulador de Android Studio** y dispositivos físicos Android.

---

### 7.1.2. Source Code Management

#### Repositorios del proyecto

El proyecto está organizado en una **organización de GitHub**, donde cada módulo tiene su propio repositorio.

| Componente | Tecnología | Repositorio | Despliegue |
|---|---|---|---|
| Aplicación móvil | Kotlin (Android nativo) | https://github.com/Movil-dev-Aplicaciones-Moviles/smartstay-application-mobile | Android Studio Emulator / APK de pruebas |
| Backend (Web Services) | ASP.NET Core (.NET 9), microservicios | https://github.com/Movil-dev-Aplicaciones-Moviles/application-mobile-backend | Docker Compose |
| Landing Page | HTML, CSS, JavaScript | https://github.com/Movil-dev-Aplicaciones-Moviles/landing-page | GitHub Actions / GitHub Pages |

Todos los repositorios siguen el modelo **GitFlow**.

#### Estructura del repositorio backend

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

#### Flujo de trabajo GitFlow

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

#### Archivos excluidos del control de versiones

El archivo `.env` contiene la cadena de conexión a MySQL y otros secretos, por lo que está en `.gitignore` y se excluye de los contextos Docker. En el repositorio solo existe `.env.example` como plantilla. Los secretos no se suben a Git ni se muestran en capturas del informe.

#### Integración continua con GitHub Actions

El workflow `Docker` (`.github/workflows/docker-publish.yml`) construye y publica las imágenes de los microservicios:

| Aspecto | Configuración |
|---|---|
| Disparadores | `push` a `main`, tags `v*.*.*`, `pull_request` hacia `main` y ejecución diaria programada (`cron: 27 3 * * *`) |
| Estrategia | Matriz de 7 servicios en paralelo: Accommodations, Analytics, Bookings, Concierge, IAM, Payments y Profiles |
| Construcción | Docker Buildx con el `Dockerfile` de cada servicio (`src/Services/SmartStay.<Servicio>/Dockerfile`) y caché de GitHub Actions |
| Registro | GitHub Container Registry (`ghcr.io`), solo cuando el evento no es un Pull Request |
| Firma | Las imágenes publicadas se firman con cosign |

En un Pull Request el workflow solo comprueba que las imágenes compilen, sin publicarlas. Nginx y ActiveMQ usan imágenes públicas y `migrate` se construye localmente, por lo que no forman parte de la matriz.

#### Verificaciones de calidad

```bash
dotnet test backend-aw-smartstay.sln -c Release   # Pruebas unitarias
bash tools/check-boundaries.sh                    # Verifica que ningún microservicio viole las fronteras arquitectónicas
bash tools/smoke-mvp.sh                           # Prueba de humo end-to-end de 13 pasos
```

---

### 7.1.3. Source Code Style Guide & Conventions

El equipo adopta convenciones de nomenclatura y guías de estilo estandarizadas para mantener la coherencia, legibilidad y escalabilidad del código. Variables, funciones, clases y archivos se nombran en **inglés**, según las convenciones de cada lenguaje.

#### Kotlin (Android Studio)

Referencias: [Kotlin Coding Conventions](https://kotlinlang.org/docs/coding-conventions.html) y [Android Kotlin Style Guide](https://developer.android.com/kotlin/style-guide).

- **PascalCase** para clases y actividades (`LoginActivity`, `RoomManagementActivity`).
- **camelCase** para variables, funciones y parámetros (`guestName`, `validateLogin()`).
- Organización modular por paquetes (`activities`, `services`, `models`, `adapters`).
- Nombres descriptivos y consistentes para layouts XML y recursos visuales.

Componentes utilizados: `Activity`, `Fragment`, `RecyclerView`, `Intent`, `ViewModel`, Firebase y layouts XML.

#### C# y ASP.NET Core (backend)

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

#### Buenas prácticas comunes

- Nomenclatura en inglés.
- Principio **DRY** (*Don't Repeat Yourself*): evitar duplicación de código.
- Principio **KISS** (*Keep It Simple, Stupid*): priorizar soluciones simples y claras.
- Código documentado y con convenciones homogéneas entre la aplicación móvil y el backend.
- Formato automatizado mediante linters y herramientas de formateo de cada entorno.
- Commits con prefijos `feat:`, `fix:` y `docs:`, y revisión de código mediante Pull Request.

---

### 7.1.4. Software Deployment Configuration

El despliegue considera los aspectos que garantizan la disponibilidad y correcta operación de los componentes del sistema.

#### Backend (Web Services)

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

#### Mobile Application Deployment

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

![Android Studio Emulator](assets/Chapter-IIII//android-studio-emulator.jpg)

*El emulador de Android Studio permite validar la aplicación móvil en distintos dispositivos y versiones de Android antes de su despliegue final.*

#### Landing Page

La Landing Page se despliega con **GitHub Actions** en GitHub Pages: https://movil-dev-aplicaciones-moviles.github.io/landing-page/

#### Integración y despliegue continuo (CI/CD)

- Todos los repositorios están conectados a **GitHub** y siguen GitFlow.
- En el backend, GitHub Actions construye las imágenes de los siete microservicios y las publica en `ghcr.io` al integrar en `main` o al etiquetar una versión.
- En la Landing Page, GitHub Actions publica el sitio al fusionar en `main`.
- Las versiones móviles se compilan y prueban desde Android Studio antes de cada entrega.

#### Limitaciones conocidas

- La base MySQL gratuita de filess.io tiene límites de espacio y conexiones, por lo que se usan pocos datos, una instancia por API y `Pooling=false`.
- Una sola base y credenciales compartidas son una simplificación académica; en producción cada servicio tendría su propia base.
- El túnel de Cloudflare es temporal y adecuado para demostraciones, no para producción.