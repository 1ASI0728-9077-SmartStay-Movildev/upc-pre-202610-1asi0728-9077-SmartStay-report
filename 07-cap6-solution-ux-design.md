<div style="page-break-before: always;"></div>

# Capítulo VI: Solution UI/UX Design
## 6.1 Style Guidelines

La base de esta sección es definir la identidad visual y de diseño de Smart Stay, con el fin de asegurar consistencia, claridad y facilidad de uso en todos los puntos de contacto de la marca, tanto en medios digitales como en la experiencia general del usuario. 

**Objetivo:**
- Alinear la comunicación visual y la propuesta del producto con la misión de la startup.
- Garantizar una experiencia de usuario comprensible, accesible y visualmente atractiva.
- Permitir que el diseño pueda integrarse de manera coherente tanto en la web como en aplicaciones móviles mediante un lenguaje visual unificado.

### 6.1.1 General Style Guidelines

**Branding**

- **Logo Smart Stay:** Corresponde al logotipo principal con el que la startup se presenta frente al público y construye reconocimiento de marca.

![alt text](assets/images/cap6/logo.png)

- **Logo Modo Oscuro:** Se trata de una variante diseñada para utilizarse sobre fondos oscuros, favoreciendo el contraste visual, el descanso de la vista y, además, el ahorro de batería en ciertos dispositivos.

![alt text](assets/images/cap6/logo-modo-oscuro.png)

- **Logo Plus:** Es una versión del logotipo con una tonalidad que transmite mayor sofisticación y se utiliza para identificar a los usuarios que optan por la suscripción plus del servicio.

![alt text](assets/images/cap6/logo-plus.png)

- **Logo Plus Modo Oscuro:** Mantiene la misma finalidad del logo en modo oscuro, pero adaptado específicamente para la versión plus del servicio.

![alt text](assets/images/cap6/logo-plus-modo-oscuro.png)

- **Logos Monocromáticos:** Son versiones en blanco y negro pensadas para usos especiales, como impresiones o documentación formal.

![alt text](assets/images/cap6/logo-monocromatico-1.png)
![alt text](assets/images/cap6/logo-monocromatico-2.png)

**Colores**

La paleta toma como referencia el logotipo y los mockups de Smart Stay. Cada color tiene una función definida y no debe utilizarse como único indicador de estado.

| Rol | Aplicación |
|---|---|
| Azul corporativo | Identidad, navegación, encabezados y superficies que requieren énfasis. |
| Naranja de acento | Llamadas a la acción y elementos interactivos prioritarios; se reserva para no competir con el contenido. |
| Blanco y neutros claros | Fondos de lectura y separación de secciones. |
| Colores semánticos | Estados como disponible, ocupado, pendiente o mantenimiento; siempre acompañados por etiqueta o icono. |

Los contrastes de texto y controles deben cumplir los criterios de accesibilidad indicados en la sección 6.1.2. Los colores exactos se deben mantener como tokens compartidos, tomando los archivos de marca como referencia y evitando variaciones locales entre plataformas.

**Espaciado y composición**

Se utilizará una escala base de 8 px, con un paso auxiliar de 4 px para ajustes pequeños. Los valores de referencia son **4, 8, 16, 24, 32 y 48 px**: 4–8 px para elementos relacionados, 16–24 px entre controles y bloques, y 32–48 px para separar secciones. La escala se adapta al tamaño de pantalla sin reducir el área táctil ni la legibilidad.

**Tono de comunicación**

Smart Stay se comunica de manera **profesional y cálida**, con un tono respetuoso, sereno y directo. El lenguaje debe ser claro y cercano, sin expresiones irreverentes ni alarmistas. Los mensajes dirigidos al staff priorizan brevedad y acción; los dirigidos al huésped son acogedores y tranquilizadores. Los errores indican qué ocurrió y qué puede hacer la persona para continuar.

**Repositorio visual compartido**

Los logotipos, wireframes y mockups de este capítulo se mantienen centralizados en `assets/images/cap6/`, que funciona como referencia común del equipo. Las fuentes Cocomat Pro, Open Sans o Lato y los tokens de color y espaciado deben documentarse y reutilizarse en web y móvil; los archivos tipográficos solo se incorporarán al repositorio cuando se cuente con permiso de distribución.

**Tipografía**

- **Fuente principal (Brand & Titles):**  
  **Cocomat Pro**  
  **Uso:** Logo, encabezados y títulos principales dentro de la app o la web.  
  **Razón:** Aporta una apariencia moderna y premium, con una estética limpia que fortalece la identidad visual de la marca.

- **Fuente secundaria (Text & Paragraphs):**  
  **Open Sans o Lato**  
  **Uso:** Textos descriptivos, botones, menús, correos y cualquier bloque de contenido extenso.  
  **Razón:** Son fuentes muy legibles en pantalla, versátiles y complementan la elegancia de Cocomat Pro sin restarle protagonismo.

- **Jerarquía de uso**
1. Títulos (H1, H2): Cocomat Pro Bold.
2. Subtítulos / énfasis: Cocomat Pro Medium.
3. Texto general / párrafos: Open Sans Regular.
4. Botones y menús: Open Sans SemiBold. 

- **Sistema Tipográfico**
  - **H1 (Títulos principales):** Cocomat Pro Bold – 32px  
  - **H2 (Subtítulos / secciones):** Cocomat Pro Medium – 24px  
  - **H3 (Bloques / cards):** Cocomat Pro Medium – 20px  
  - **Texto cuerpo (párrafos):** Open Sans Regular – 16px  
  - **Texto secundario / notas:** Open Sans Regular – 14px  
  - **Botones primarios:** Open Sans SemiBold – 16px (MAYÚSCULAS)

### 6.1.2. Web, Mobile & Devices Style Guidelines 

Smart Stay ofrece una experiencia coherente en tres puntos de contacto: la Landing Page desarrollada para web, la aplicación web administrativa y las aplicaciones móviles nativas. La interfaz de cada canal se adapta a las tareas y al contexto de uso de sus usuarios, manteniendo los mismos principios de marca, lenguaje visual y retroalimentación.

| Canal | Usuario y contexto principal | Criterio de diseño |
|---|---|---|
| Landing Page web (HTML5/JS) | Visitantes que buscan conocer la propuesta de Smart Stay desde distintos dispositivos. | Diseño responsive, navegación simple y llamadas a la acción visibles sin desplazar contenido esencial. |
| Aplicación web administrativa | Administradores que consultan reportes y gestionan reservas, habitaciones e incidencias. | Priorizar la lectura rápida, la comparación de datos y la ejecución eficiente de tareas; adaptar tablas y navegación a pantallas estrechas. |
| Aplicación Android nativa (Kotlin) | Personal operativo que consulta habitaciones, recibe alertas y actualiza tareas durante sus recorridos. | Acciones frecuentes accesibles con una mano, estados operativos reconocibles de inmediato y controles apropiados a Android. |
| Aplicación móvil multiplataforma (Flutter) | Huéspedes que gestionan su estancia y solicitan servicios desde su teléfono. | Flujos breves y guiados, controles de habitación comprensibles y acceso directo a servicios, preferencias y comunicación con el hotel. |

**Principios visuales compartidos**

- **Identidad consistente:** utilizar las variantes del logotipo, la paleta cromática y las familias tipográficas definidas en la sección 6.1.1. Cocomat Pro se reserva para encabezados y títulos; Open Sans o Lato se utiliza en contenido, formularios, navegación y controles.
- **Jerarquía y legibilidad:** presentar primero la información necesaria para la tarea actual. Mantener títulos, etiquetas y acciones con jerarquías consistentes y evitar bloques extensos de texto en pantallas operativas.
- **Componentes y estados coherentes:** botones, campos, avisos, navegación y estados de reserva o habitación deben conservar el mismo significado en web y móvil, aunque su disposición se adapte al dispositivo.
- **Color con significado accesible:** emplear los colores de marca para identidad y énfasis, y colores semánticos para estados como disponible, ocupado, pendiente o mantenimiento. Acompañar siempre el color con texto, icono o forma; nunca comunicar el estado únicamente mediante color.
- **Modo claro y oscuro:** utilizar las variantes de logotipo apropiadas para el fondo y conservar contraste suficiente en ambos modos. La información, los estados y las acciones disponibles deben ser equivalentes.

**Diseño responsive para web**

La web se plantea con enfoque *mobile-first*: el contenido se organiza primero para espacios reducidos y luego se amplía cuando existe más área disponible. Los siguientes rangos son referencias de composición, no dimensiones rígidas; el diseño debe responder al espacio real del contenido.

| Referencia de ancho | Adaptación esperada |
|---|---|
| Menos de 600 px | Una columna; navegación compacta; acciones principales visibles; formularios apilados; tablas administrativas convertidas en listas o tarjetas con los datos prioritarios. |
| De 600 a 1023 px | Dos columnas cuando mejoren la lectura; filtros y paneles secundarios pueden agruparse o colapsarse; conservar controles con área táctil suficiente. |
| Desde 1024 px | Aprovechar el espacio para navegación persistente, tablas comparativas y paneles de resumen, sin estirar innecesariamente líneas de texto ni controles. |

En la Landing Page, las secciones y los elementos visuales deben reordenarse sin perder el acceso a la navegación ni a las llamadas a la acción. En la aplicación administrativa, filtros, reportes y tablas deben mantener etiquetas visibles, permitir identificar rápidamente cada registro y ofrecer una alternativa usable cuando no haya espacio para mostrar todas las columnas.

**Aplicaciones móviles y dispositivos**

- Mantener la navegación principal y las acciones frecuentes en posiciones predecibles. En la app del huésped, priorizar la estancia activa, los servicios y el control de la habitación; en la app del staff, priorizar tareas, habitaciones, incidencias y notificaciones.
- Diseñar objetivos táctiles de al menos **48 × 48 dp** en Android y proporcionar separación entre acciones cercanas. No depender de gestos ocultos: toda acción importante debe contar con un control visible.
- Solicitar permisos del dispositivo (por ejemplo, notificaciones o Bluetooth, cuando una función lo requiera) en el contexto de uso y explicar su propósito antes de abrir el diálogo del sistema. La denegación de un permiso no debe bloquear funciones que no dependan de él.
- Adaptar las vistas a orientación vertical y horizontal cuando aporte valor, especialmente en paneles o reportes. En teléfonos pequeños, priorizar el contenido esencial; en tabletas, aprovechar el espacio adicional sin convertir cada pantalla en una versión ampliada del teléfono.
- Respetar las convenciones de cada plataforma para navegación, teclado, áreas seguras, retroceso y controles del sistema, manteniendo los patrones de marca y la terminología comunes a Smart Stay.

**Referencias visuales de las aplicaciones móviles nativas**

Los siguientes mockups muestran cómo se aplican la identidad compartida y la navegación táctil a las tareas diferenciadas de cada perfil.

*Smart Stay Staff: acceso, tareas, reservas y perfil operativo.*

![Mockups móviles de Smart Stay Staff](assets/images/cap6/mockupstaff1.png)
![Pantallas adicionales de Smart Stay Staff](assets/images/cap6/mockupstaff2.png)

*Smart Stay Guest: búsqueda, habitación, servicios y perfil del huésped.*

![Mockups móviles de Smart Stay Guest](assets/images/cap6/mockuphuesped1.png)
![Pantallas adicionales de Smart Stay Guest](assets/images/cap6/mockuphuesped2.png)

**Interacción con habitaciones y dispositivos IoT**

Los controles de iluminación, temperatura, acceso y conectividad deben mostrar el valor o estado actual del dispositivo y distinguir claramente entre la acción solicitada y la confirmación recibida. Al enviar un comando, la interfaz informa que está procesándolo; solo indica que se completó cuando recibe confirmación. Si el dispositivo no responde o la conexión se interrumpe, se presenta un mensaje comprensible, el último estado conocido con su hora de actualización y una opción para reintentar cuando corresponda. Las acciones de acceso y otras operaciones sensibles requieren confirmación explícita y retroalimentación visible.

**Accesibilidad y retroalimentación**

- Mantener como objetivo de conformidad **WCAG 2.2 nivel AA** para las interfaces web: contraste mínimo de 4.5:1 para texto normal y 3:1 para texto grande, además de navegación por teclado y foco visible.
- Proporcionar etiquetas accesibles a iconos y controles, orden de lectura lógico y compatibilidad con lectores de pantalla. No usar el placeholder como única etiqueta de un campo.
- Permitir ampliación de texto y evitar que el contenido o las acciones se recorten al aumentar el tamaño de fuente. Usar lenguaje claro para explicar errores, sus causas cuando se conozcan y el siguiente paso disponible.
- Dar respuesta perceptible a acciones como iniciar sesión, confirmar check-in, enviar una solicitud, cambiar el estado de una habitación o controlar un dispositivo. Las notificaciones deben indicar el evento y su relevancia sin interrumpir tareas no relacionadas.

Estas directrices se aplican a los wireframes y mockups de la sección 6.3 y sirven como referencia compartida para evolucionar la Landing Page, la aplicación administrativa y las aplicaciones móviles sin perder consistencia ni adecuación a cada contexto de uso.

## 6.2 Information Architecture

### 6.2.1 Organization Systems

La organización combina jerarquía de navegación, secuencias para tareas y vistas matriciales para comparar datos. La categorización depende del tipo de información y del perfil que la consume, de modo que Landing Page, staff y huésped encuentran primero lo más relevante para su objetivo.

| Grupo de información | Organización visual | Esquema de categorización | Justificación |
|---|---|---|---|
| Landing Page: Home, Products, Solutions, Prices, Success Stories y Resources | Jerárquica: navegación principal, secciones y contenido de cada sección. | Por tópicos y orientada a la audiencia visitante. | Facilita explorar la propuesta desde información general hasta productos, planes y recursos. |
| Módulos de staff: Dashboard, Rooms, Bookings, Tasks, Reports y Notifications | Jerárquica por módulo; matricial en listados de habitaciones, reservas y tareas. | Según audiencia (staff) y por estado operativo. | Permite supervisar varias entidades y comparar su estado sin perder el contexto del hotel. |
| Funciones del huésped: Check-in, My Room, Services, Requests y Check-out | Secuencial en check-in/check-out y solicitud de servicios; jerárquica para acceder a la estancia y sus funciones. | Según audiencia (huésped) y por tópicos de estancia. | Acompaña tareas con un inicio, confirmación y estado final claros. |
| Reservas, tareas y notificaciones | Listas cronológicas, ordenadas por fecha o vencimiento; filtros por estado y prioridad cuando corresponda. | Cronológico y por estado. | Ayuda a identificar primero llegadas próximas, tareas pendientes y eventos recientes. |
| Catálogos extensos de servicios o recursos | Categorías por tema; orden alfabético como alternativa dentro de una categoría extensa. | Por tópicos y, secundariamente, alfabético. | Reduce el esfuerzo de exploración y permite localizar elementos conocidos. |

En pantallas pequeñas se conserva el mismo orden lógico, pero se reemplazan matrices densas por listas o tarjetas; los flujos secuenciales muestran el paso actual y permiten volver sin perder los datos ya ingresados.

- UX Heuristics & Principles Evaluation

**Usability – Inclusive Design – Information Architecture**

- **CARRERA:** Ingeniería de Software  
- **CURSO:** Aplicaciones para Dispositivos Móviles  
- **SECCIÓN:** 7454  
- **PROFESOR:** Jorge Luis Mayta Guillermo  
- **AUDITOR:** Equipo Smart Stay  
- **CLIENTE(S):** Administradores de Hoteles Boutique y Huéspedes de Hoteles  
- **SITE o APP A EVALUAR:** Smart Stay Mobile Application  

---

- TAREAS A EVALUAR

**Segmento Objetivo #1: Staff Operativo de Hoteles (Administradores y Personal)**

- Gestión de habitaciones: visualización en tiempo real del estado (disponible, ocupado, mantenimiento).
- Coordinación de tareas de limpieza: asignación rápida y seguimiento de housekeeping.
- Notificaciones operativas: alertas sobre incidencias, check-in/check-out y solicitudes de huéspedes.
- Reportes operativos: acceso a métricas de ocupación y estado del hotel.
- Control de incidencias: registro y seguimiento de problemas técnicos en habitaciones.

---

**Segmento Objetivo #2: Huéspedes de Hoteles**

- Check-in / Check-out digital: proceso rápido y sin contacto desde la aplicación.
- Control de habitación: manejo de dispositivos IoT (iluminación, temperatura, Wi-Fi).
- Solicitud de servicios: acceso a room service, limpieza y soporte técnico.
- Personalización de la experiencia: configuración de preferencias durante la estancia.
- Comunicación con el hotel: contacto directo mediante canales digitales.

---

**No incluidas en esta versión de la evaluación:**

- Integración con sistemas financieros avanzados (facturación completa).
- Conexión con plataformas externas (marketplaces o agencias de viaje).
- Funcionalidades de marketing interno del hotel.

---

***ESCALA DE SEVERIDAD***

| Nivel | Descripción |
|------|------------|
| 1 | Problema leve: no afecta significativamente la experiencia. |
| 2 | Problema moderado: genera fricción ocasional en el uso. |
| 3 | Problema grave: afecta la eficiencia del usuario de forma recurrente. |
| 4 | Problema crítico: impide completar tareas principales dentro de la app. |

---

***TABLA RESUMEN***

| # | Problema | Escala de severidad | Heurística/Principio violado |
|--|----------|---------------------|-----------------------------|
| 1 | Dificultad para visualizar el estado de habitaciones en tiempo real | 3 | Visibilidad del estado del sistema |
| 2 | Notificaciones poco configurables para el staff | 2 | Flexibilidad y eficiencia de uso |
| 3 | Navegación poco clara entre módulos principales | 3 | Consistencia y estándares |
| 4 | Exceso de pasos en el proceso de check-in digital | 2 | Minimizar carga cognitiva |
| 5 | Falta de retroalimentación inmediata en acciones del usuario | 3 | Feedback del sistema |
| 6 | Opciones de personalización poco visibles para huéspedes | 2 | Reconocimiento antes que recuerdo |

---

***ANÁLISIS GENERAL***

La arquitectura de información de Smart Stay presenta una estructura basada en tareas y roles, lo que facilita la segmentación entre usuarios internos (staff) y externos (huéspedes). Sin embargo, se identifican oportunidades de mejora en la claridad de navegación, visibilidad del estado del sistema y optimización de flujos críticos como el check-in digital.

Se concluye que una correcta reorganización de la jerarquía de información y mejora en la retroalimentación visual permitirá reducir la carga cognitiva del usuario y mejorar la eficiencia operativa del sistema.

### 6.2.2 Labeling Systems

El sistema de etiquetado define cómo se nombran las secciones, botones y funcionalidades dentro de la aplicación, permitiendo que el usuario comprenda rápidamente el propósito de cada elemento. En Smart Stay, las etiquetas se diseñan bajo principios de claridad, consistencia y orientación al usuario, adaptándose tanto al Staff Operativo como a los Huéspedes.

---

| Etiqueta | Ubicación / Componente | Función |
|----------|------------------------|--------|
| Home | Header / Navegación principal | Redirige a la pantalla principal o dashboard. Permite acceso rápido al inicio. |
| Rooms | Menú principal / App | Acceso a la gestión de habitaciones (estado, disponibilidad, mantenimiento). |
| Services | Menú principal | Muestra los servicios disponibles (limpieza, room service, soporte). |
| Dashboard | Pantalla principal | Vista general del estado del sistema y resumen de operaciones. |
| Bookings | Módulo de reservas | Permite gestionar reservas activas y futuras. |
| Check-in | Flujo principal | Permite registrar la entrada del huésped de forma digital. |
| Check-out | Flujo principal | Permite finalizar la estancia del huésped de forma rápida. |
| Login | Pantalla de acceso | Inicio de sesión del usuario. Término estándar y reconocido. |
| Sign Up | Pantalla de acceso | Registro de nuevos usuarios. Corto, claro y amigable. |
| Try Demo | Landing Page (CTA) | Llamada a la acción principal para probar la aplicación. |
| My Room | App Huésped | Acceso al control de la habitación (IoT, temperatura, iluminación). |
| Requests | App Huésped | Permite solicitar servicios del hotel desde el móvil. |
| Tasks | App Staff | Gestión de tareas operativas (limpieza, mantenimiento). |
| Notifications | Icono / App | Muestra alertas en tiempo real sobre eventos importantes. |
| Profile | Menú usuario | Configuración de cuenta y preferencias del usuario. |
| Settings | Menú secundario | Ajustes generales del sistema. |
| Reports | App Staff | Acceso a métricas y reportes operativos del hotel. |
| Contact | Landing / App | Permite comunicación con el hotel o soporte técnico. |

Las etiquetas se mantienen cortas, consistentes y vinculadas al lenguaje habitual de cada perfil. Se evita usar dos términos distintos para la misma función y se prefiere nombrar las secciones con sustantivos y las acciones con verbos claros.

| Etiqueta principal | Etiquetas asociadas | Relación |
|---|---|---|
| Rooms | Availability, Occupied, Maintenance | Estados que describen la condición actual de una habitación. |
| Bookings | Check-in, Check-out, History | Acciones y consultas asociadas a una reserva. |
| My Room | Lighting, Temperature, Wi-Fi | Controles del ambiente y conectividad de la habitación. |
| Services | Room Service, Cleaning, Technical Support | Categorías de solicitudes disponibles para el huésped. |
| Tasks | Cleaning, Maintenance, Priority, Status | Tipo y seguimiento de una actividad asignada al staff. |

---

### 6.2.3 Searching Systems

El sistema de búsqueda de Smart Stay permite a los usuarios localizar información, reservas, servicios y funcionalidades de manera rápida y eficiente. En la Landing Page, la búsqueda está orientada a descubrir contenido general sobre la plataforma, utilizando accesos directos, enlaces destacados y navegación guiada hacia secciones clave como “Try Demo” o “Benefits”.

En la aplicación móvil, el sistema de búsqueda es más funcional y está enfocado en la gestión de información específica. Permite a los usuarios filtrar y ordenar datos como habitaciones, reservas, servicios o tareas operativas, utilizando autocompletado, filtros dinámicos y persistencia de resultados. El diseño se basa en principios de usabilidad, consistencia y eficiencia, asegurando que el usuario encuentre lo que necesita sin dificultad.

---

| Search Type | Location / Component | Function |
|-------------|---------------------|----------|
| General Search | Landing Page / Header | Permite buscar información general sobre la plataforma y sus servicios (ej. "servicios", "demo", "beneficios"). Incluye autocompletado básico. |
| Try Demo / Benefits Links | Landing Page / Hero & Value Sections | Funciona como búsqueda indirecta, guiando al usuario hacia contenido relevante sin necesidad de ingresar texto. |
| Rooms Search | Mobile App / Rooms Section | Permite buscar habitaciones por número, estado (disponible, ocupado, mantenimiento) o tipo. |
| Bookings Search | Mobile App / Bookings Section | Filtrado por fechas, estado de reserva (pendiente, confirmada, cancelada) y tipo de cliente. |
| Services Search | Mobile App / Services Section | Permite buscar servicios disponibles (limpieza, room service, soporte técnico) mediante filtros y categorías. |
| Tasks Search | Mobile App / Staff Module | Permite al staff localizar tareas asignadas por prioridad, estado o tipo de actividad. |
| Notifications Search | Mobile App / Notifications Panel | Permite revisar alertas y eventos importantes mediante filtrado por tipo o fecha. |

**Presentación de resultados**

Los resultados conservan los filtros aplicados, muestran un conteo y permiten ordenar por el criterio más útil para la tarea. En móvil se presentan como listas o tarjetas; en la web administrativa pueden mostrarse como tablas con encabezados persistentes.

| Tipo de resultado | Datos visibles para reconocer cada resultado |
|---|---|
| Rooms | Número, tipo, estado y, cuando aplique, tarea activa. |
| Bookings | Huésped, habitación, fechas de estancia y estado de la reserva. |
| Services | Nombre, categoría, disponibilidad y acción para solicitar el servicio. |
| Tasks | Tipo de tarea, habitación, prioridad, vencimiento y estado. |
| Notifications | Fecha y hora, evento, habitación relacionada y estado de lectura. |

Cuando no haya coincidencias, la interfaz indica que no encontró resultados y permite limpiar o ajustar los filtros; no presenta una pantalla vacía sin explicación.

---

### 6.2.4 SEO Tags, Meta Tags y ASO Elements

Los SEO tags y meta tags son elementos fundamentales dentro de la Landing Page de Smart Stay, ya que permiten mejorar la visibilidad del sistema en motores de búsqueda, facilitar su indexación y optimizar la forma en que se presenta tanto en resultados de búsqueda como en redes sociales.

Además, estos elementos son clave para garantizar una correcta visualización en dispositivos móviles, mejorar la experiencia del usuario y aumentar la tasa de interacción (CTR).

La Landing Page de Smart Stay implementa etiquetas esenciales como: charset, viewport, title, description, keywords y favicon, las cuales permiten estructurar correctamente la información del sitio.

---

***Meta charset***

```html
<meta charset="UTF-8">
```

- Define la codificación de caracteres de la página.
- Permite que el contenido se muestre correctamente, incluyendo tildes, símbolos y caracteres especiales.
- Es fundamental para evitar errores de visualización en distintos navegadores.

---

***Meta viewport***

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

- Permite que la página sea responsive.
- Ajusta automáticamente el contenido al tamaño de la pantalla del dispositivo.
- Mejora la experiencia de usuario en smartphones y tablets.

---

***Title***

```html
<title>Smart Stay</title>
```

- Define el título de la página que aparece en la pestaña del navegador.
- Es uno de los factores más importantes para SEO.
- Se muestra como encabezado principal en los resultados de búsqueda.

---

***1. Meta Tags principales***

- **charset:** Define la codificación del documento. UTF-8 es el estándar actual.
- **viewport:** Permite adaptar la página a diferentes dispositivos y resoluciones.
- **description:** Proporciona un resumen del contenido de la página. Es el texto que aparece debajo del título en los resultados de búsqueda.
- **keywords:** Lista de palabras clave relacionadas con el sistema (ej. hotel management, mobile app, IoT hotel).
- **author:** Identifica al creador del contenido (Smart Stay Team).

---

***2. Meta Tags para Redes Sociales (Open Graph)***

```html
<meta property="og:title" content="Smart Stay">
<meta property="og:description" content="Solución móvil para gestión hotelera con IoT">
<meta property="og:image" content="assets/logo.png">
<meta property="og:url" content="https://smartstay.com">
```

- Permiten controlar cómo se muestra la página al compartirla en redes sociales.
- Mejoran la apariencia visual del enlace (imagen, título y descripción).
- Aumentan la probabilidad de interacción del usuario.

---

***3. Otros elementos importantes***

**Favicon:**

```html
<link rel="icon" href="assets/favicon.png">
```

- Representa el icono del sitio en la pestaña del navegador.
- Refuerza la identidad visual de la marca.

**Canonical URL:**

```html
<link rel="canonical" href="https://smartstay.com">
```

- Evita problemas de contenido duplicado en buscadores.

Los siguientes valores son una propuesta para la publicación. Se debe reemplazar `smartstay.com` por el dominio definitivo antes del despliegue y emplear las descripciones y palabras clave correspondientes a cada página.

***Valores SEO por página***

| Página | Title | Description | Keywords |
|---|---|---|---|
| Home | Smart Stay | Gestión hotelera inteligente | Gestión hotelera para hoteles boutique: habitaciones, servicios y control IoT desde una plataforma digital. | Smart Stay, gestión hotelera, hotel boutique, IoT hotelero |
| Products | Productos para hoteles | Smart Stay | Conoce las herramientas de Smart Stay para reservas, habitaciones, servicios y operación hotelera. | software hotelero, PMS, reservas, housekeeping, Smart Stay |
| Solutions | Soluciones hoteleras | Smart Stay | Optimiza la operación del hotel y mejora la estancia de tus huéspedes con soluciones conectadas. | soluciones hoteleras, automatización hotel, experiencia huésped, IoT |
| Prices | Planes y precios | Smart Stay | Compara los planes de Smart Stay y encuentra las funcionalidades que necesita tu hotel. | planes software hotelero, precios, gestión hotel boutique |
| Success Stories | Casos de éxito | Smart Stay | Conoce cómo hoteles y huéspedes aprovechan Smart Stay durante la operación y la estancia. | casos de éxito hoteleros, testimonios, Smart Stay |
| Resources | Recursos para hoteles | Smart Stay | Guías y contenidos sobre gestión hotelera, experiencia del huésped y tecnología IoT. | recursos hoteleros, guías hotel, gestión hotelera, IoT |
| Register / Login | Acceso a Smart Stay | Regístrate o inicia sesión para acceder a los servicios de Smart Stay. | No se prioriza su indexación; aplicar `noindex` a las páginas de acceso. |
| Aplicación administrativa | Smart Stay Admin | Dashboard | Acceso privado para la operación y administración del hotel. | Página privada; aplicar `noindex, nofollow` y excluirla del sitemap público. |

En cada página pública se definen también `author` como “Equipo Smart Stay” y `robots` como `index,follow`. Para páginas de acceso y áreas autenticadas, se usa `noindex` para evitar exponer contenido privado o de escaso valor de búsqueda.

```html
<meta name="description" content="Gestión hotelera para hoteles boutique: habitaciones, servicios y control IoT desde una plataforma digital.">
<meta name="keywords" content="Smart Stay, gestión hotelera, hotel boutique, IoT hotelero">
<meta name="author" content="Equipo Smart Stay">
<meta name="robots" content="index,follow">
```

***ASO para aplicaciones móviles***

Los textos siguientes son propuestas para las fichas de las aplicaciones nativas. Las palabras clave se incorporan a la descripción y a los campos que permita cada tienda; si la tienda no ofrece un campo específico de keywords, no se debe asumir que existe una etiqueta equivalente.

| Elemento ASO | Smart Stay Staff (Android/Kotlin) | Smart Stay Guest (Flutter) |
|---|---|---|
| App Title | Smart Stay Staff | Smart Stay Guest |
| App subtitle | Gestión hotelera en movimiento | Tu estancia, a tu manera |
| App keywords | gestión hotelera, habitaciones, housekeeping, tareas, reservas | hotel, huésped, check-in digital, room service, habitación inteligente |
| App description | Aplicación para que el personal del hotel consulte habitaciones, coordine tareas, atienda incidencias y reciba notificaciones operativas. | Aplicación para que los huéspedes gestionen su estancia, realicen check-in, controlen funciones IoT de su habitación y soliciten servicios al hotel. |

---

### 6.2.5 Navigation Systems

El sistema de navegación de Smart Stay define cómo los usuarios se desplazan dentro de la plataforma, permitiendo acceder a las distintas secciones de forma clara, rápida e intuitiva. Este sistema está diseñado bajo principios de consistencia, accesibilidad y eficiencia, adaptándose tanto a la Landing Page como a la aplicación móvil.

---

***Landing Page Navigation***

| Navigation Item | Location / Component | Function |
|-----------------|----------------------|----------|
| Home | Header | Enlace a la página principal. Permite regresar al inicio desde cualquier sección. |
| Services | Header | Acceso directo a la sección de servicios ofrecidos por la plataforma. |
| Benefits | Header / Value Section | Redirige a la sección donde se explican las ventajas del sistema. |
| Contact | Header | Permite acceder al formulario de contacto o soporte. |
| Sign Up | Header (button) | Registro de nuevos usuarios. Botón destacado visualmente. |
| Login | Header (button) | Acceso a la cuenta del usuario. Fácil de localizar. |
| Try Demo | Hero Section (CTA principal) | Llamada a la acción principal para probar la plataforma. |
| About | Footer / Company | Información institucional de Smart Stay. |
| Privacy Policy | Footer / Legal | Acceso a políticas de privacidad del sistema. |
| Terms & Conditions | Footer / Legal | Información sobre condiciones de uso de la plataforma. |

---

***Mobile Application Navigation***

| Navigation Item | Location / Component | Function |
|-----------------|----------------------|----------|
| Dashboard | Bottom Navigation | Vista general del sistema con información resumida. |
| Rooms | Bottom Navigation | Acceso a la gestión y estado de habitaciones. |
| Services | Bottom Navigation | Permite visualizar y solicitar servicios disponibles. |
| Profile | Bottom Navigation | Configuración del usuario y preferencias personales. |
| Notifications | Top Bar / Icon | Acceso a alertas y eventos importantes en tiempo real. |
| Tasks | Staff Module | Permite gestionar tareas operativas asignadas al personal. |
| Bookings | App Module | Acceso a reservas activas, historial y gestión de huéspedes. |
| Back Navigation | App Screens | Permite regresar a la pantalla anterior de forma intuitiva. |

**Recorridos principales**

- **Visitante de la Landing Page:** Home → Products o Solutions → Prices / Success Stories / Resources → Try Demo o Sign Up. La navegación del encabezado permite saltar directamente a cada sección y el footer da acceso a información institucional y legal.
- **Staff:** Login → Dashboard → Rooms o Tasks → detalle de habitación/tarea → actualización de estado o registro de incidencia. Las notificaciones enlazan con el evento relacionado y la navegación persistente permite volver a los módulos principales.
- **Huésped:** Login o Check-in → estancia activa → My Room o Services → control IoT o solicitud → confirmación y seguimiento → Check-out. En cada flujo se muestra el estado actual y una acción visible para volver o continuar.

---

## 6.3 Landing Page UI Design

El diseño de la interfaz de la Landing Page de Smart Stay tiene como objetivo principal presentar de manera clara y atractiva la propuesta de valor del sistema, captando la atención del usuario desde el primer contacto. Esta página funciona como el punto de entrada al producto, por lo que su diseño está orientado a la conversión, usabilidad y comprensión inmediata del servicio.

Se aplican principios de diseño centrado en el usuario, jerarquía visual y accesibilidad, permitiendo que tanto potenciales clientes (hoteles) como usuarios finales (huéspedes) comprendan rápidamente los beneficios de la solución.

La propuesta traduce la arquitectura de información en una navegación pública orientada al descubrimiento (Home, Products, Solutions y Prices) y en acciones claras de conversión (Try Demo y Sign Up). Los wireframes y mockups mantienen esta jerarquía y aplican el sistema visual de la sección 6.1.1. La experiencia privada se diferencia por perfil: la solución Android para staff prioriza la operación y la solución Flutter para huéspedes prioriza la estancia, los servicios y el control IoT; ambas consumen los servicios de Smart Stay definidos en las decisiones arquitectónicas.

### 6.3.1 Landing Page Wireframe

Los wireframes de la Landing Page de Smart Stay definen la estructura base de navegación, asegurando que cada sección tenga un propósito claro dentro de la experiencia del usuario. Cada pantalla está diseñada para guiar al usuario desde el descubrimiento hasta la acción (registro o uso del sistema).

Los recursos gráficos disponibles no contienen pares de capturas etiquetados para Desktop Web Browser y Mobile Web Browser. La siguiente matriz especifica la adaptación de los wireframes para ambos tamaños; las imágenes existentes son referencias de estructura y no se deben interpretar como dos variantes visuales.

| Elemento | Desktop Web Browser | Mobile Web Browser |
|---|---|---|
| Header y navegación | Logotipo, enlaces principales y acciones Sign Up/Login en una barra horizontal. | Logotipo y menú compacto; abrir la navegación con un control visible y conservar Try Demo como acción prioritaria. |
| Home y hero | Mensaje, imagen y CTA pueden distribuirse en columnas; las secciones siguen una jerarquía vertical clara. | Apilar mensaje e imagen; presentar el valor y el CTA antes del contenido secundario. |
| Products, Solutions, Success Stories y Resources | Organizar módulos en una cuadrícula y permitir comparar tarjetas en paralelo. | Convertir la cuadrícula en una columna, con títulos y acciones visibles sin desplazamiento horizontal. |
| Prices | Comparar planes y funcionalidades en columnas con encabezados persistentes. | Mostrar planes como bloques verticales; cada funcionalidad debe permanecer asociada a su plan. |
| Register y Login | Formulario centrado y acotado, con etiquetas y ayuda junto a cada campo. | Formulario de una columna, controles de ancho disponible, etiquetas persistentes y teclado adecuado al dato solicitado. |
| Footer | Enlaces agrupados en columnas por categoría. | Grupos apilados o plegables, manteniendo visibles contacto y enlaces legales. |
| Inclusión | Navegación por teclado, foco visible, orden de lectura lógico y contraste accesible. | Las mismas etiquetas y jerarquía, texto ampliable, objetivos táctiles suficientes y sin depender solo del color. |

---

***1. Home***

- **Propósito:** Página principal de presentación de Smart Stay.

- **Elementos clave:**
  - Encabezado con menú de navegación.
  - Hero con nombre de la plataforma y botón de llamada a la acción (CTA: Try Demo).
  - Sección “¿Quiénes somos?” con breve descripción.
  - Bloques de beneficios y características principales.
  - Footer con enlaces de contacto, políticas y redes sociales.

![alt text](assets/images/cap6/whome.png)

---

***2. Products***

- **Propósito:** Mostrar los productos principales que ofrece Smart Stay.

- **Elementos clave:**
  - Listado de productos o módulos del sistema.
  - Descripción breve de cada funcionalidad.
  - Íconos o ilustraciones representativas.
  - Enlaces para explorar cada producto.

![alt text](assets/images/cap6/wproductos.png)

---

***3. Solutions***

- **Propósito:** Explicar cómo la plataforma resuelve problemas específicos del sector hotelero.

- **Elementos clave:**
  - Casos de uso del sistema.
  - Beneficios aplicados a situaciones reales.
  - Explicación de soluciones para gestión, automatización e IoT.


---

***4. Prices***

- **Propósito:** Presentar los planes o modelos de precios del sistema.

- **Elementos clave:**
  - Tabla de precios o planes.
  - Comparación de funcionalidades.
  - Botones de acción para suscripción.

---

***5. Success Stories***

- **Propósito:** Generar confianza mediante casos reales o testimonios.

- **Elementos clave:**
  - Opiniones de clientes.
  - Resultados obtenidos.
  - Fotografías o elementos visuales de respaldo.

![alt text](assets/images/cap6/wreseñas.png)

---

***6. Resources***

- **Propósito:** Proporcionar contenido de apoyo para el usuario.

- **Elementos clave:**
  - Guías o documentación.
  - Artículos o blogs.
  - Material informativo sobre el sistema.

![alt text](assets/images/cap6/wrecurso.png)

---

***7. Register***

- **Propósito:** Permitir el registro de nuevos usuarios.

- **Elementos clave:**
  - Formulario de registro.
  - Campos básicos (nombre, correo, contraseña).
  - Botón de creación de cuenta.

![alt text](assets/images/cap6/wregister.png)

---

***8. Login***

- **Propósito:** Permitir el acceso a usuarios registrados.

- **Elementos clave:**
  - Formulario de inicio de sesión.
  - Campos de usuario y contraseña.
  - Opción de recuperación de contraseña.

![alt text](assets/images/cap6/wlogin.png)

Los wireframes definen la base de navegación de Smart Stay, asegurando que cada sección tenga un propósito claro:

  - Home: captar atención y presentar la plataforma.
  - Productos, Soluciones, Precios: comunicar valor y opciones.
  - Casos de Éxito, Recursos: generar confianza y soporte.
  - Registro y Login: habilitar el acceso a la app.
---

### 6.3.2 Landing Page Mock-up

Los mockups aplican el branding, la tipografía y los colores definidos en la guía general, además de materializar la jerarquía del Landing Page. Para la versión móvil se conserva el mismo contenido y prioridad de acciones, adaptando la composición según la siguiente matriz.

| Sección | Desktop Web Browser | Mobile Web Browser |
|---|---|---|
| Home | Navegación horizontal y hero con contenido e imagen en paralelo cuando el ancho lo permita. | Navegación compacta, hero apilado y Try Demo visible antes de las secciones secundarias. |
| Products y Solutions | Tarjetas y bloques comparables en varias columnas. | Tarjetas en una columna y contenido resumido antes del detalle. |
| Prices | Planes comparables en columnas, con diferencias y CTA alineados. | Planes apilados, diferencias descritas dentro de cada bloque y CTA asociado a cada plan. |
| Success Stories y Resources | Testimonios y recursos organizados en cuadrículas o bloques paralelos. | Lectura secuencial, tarjetas de ancho completo y títulos descriptivos. |
| Register y Login | Formularios centrados, con ancho limitado y ayuda contextual. | Formularios de una columna, campos de ancho disponible y acciones fáciles de alcanzar. |

Las imágenes actualmente disponibles para Landing Page no incluyen un par de mockups web Desktop/Mobile para cada página, y tampoco hay archivos de mockup para Home y Login en esta carpeta. Por ello, esta matriz define el comportamiento de la adaptación pero no sustituye esas capturas; los mockups nativos de staff y huésped mostrados en 6.1.2 corresponden a aplicaciones móviles, no a la Landing Page.

1. Landing Page

- **Cambios respecto al wireframe:**
  - Se añadió el logotipo de Smart Stay en el header.
  - Paleta de colores aplicada (azul corporativo + tonos complementarios).
  - Imagen de fondo en el Hero con llamada a la acción resaltada (“Try demo”).
  - Iconografía personalizada para los beneficios.

---

2. Product

- **Cambios respecto al wireframe:**
  - Se añadieron tarjetas visuales para cada producto.
  - Uso de iconos representativos para mejorar la comprensión.
  - Aplicación de colores para diferenciar funcionalidades.
  - Mejor organización del contenido en bloques visuales.

![alt text](assets/images/cap6/producto.png)

---

3. Solutions

- **Cambios respecto al wireframe:**
  - Se incorporaron secciones visuales para explicar soluciones específicas.
  - Uso de imágenes e iconografía para reforzar el contenido.
  - Reducción de texto y enfoque en contenido visual.
  - Mejora en la jerarquía de información.

![alt text](assets/images/cap6/soluciones.png)

---

4. Prices

- **Cambios respecto al wireframe:**
  - Se implementaron tarjetas de precios con diseño diferenciado.
  - Inclusión de botones de acción para suscripción.
  - Mejora en la comparación entre planes.
  - Uso de colores para destacar el plan principal.

![alt text](assets/images/cap6/precio.png)

---

5. Success Stories

- **Cambios respecto al wireframe:**
  - Se añadieron testimonios con diseño visual.
  - Inclusión de imágenes o avatares de usuarios.
  - Mejora en la presentación para generar confianza.
  - Organización en bloques claros y legibles.

![alt text](assets/images/cap6/reseña.png)

---

6. Resources

- **Cambios respecto al wireframe:**
  - Se estructuraron los recursos en tarjetas visuales.
  - Inclusión de iconos para cada tipo de contenido.
  - Mejora en la accesibilidad a la información.
  - Optimización del diseño para navegación rápida.

![alt text](assets/images/cap6/recursos.png)

---

7. Register

- **Cambios respecto al wireframe:**
  - Mejora en el diseño del formulario de registro.
  - Aplicación de estilos a los campos de entrada.
  - Botón de registro visualmente destacado.
  - Optimización para dispositivos móviles.

![alt text](assets/images/cap6/register.png)

---

8. Login

- **Cambios respecto al wireframe:**
  - Simplificación del formulario de inicio de sesión.
  - Mejora en la visibilidad de los campos.
  - Inclusión de opción de recuperación de contraseña.
  - Diseño optimizado para acceso rápido.

## 6.4. Applications UX/UI Design

El diseño UX/UI de las aplicaciones que integran el ecosistema digital de Smart Stay traduce los requerimientos funcionales, arquitectónicos y de accesibilidad en interfaces eficientes y centradas en el usuario. A diferencia del enfoque informativo y de conversión de la Landing Page, estas soluciones están orientadas a la interacción recurrente y a la ejecución inmediata de tareas operativas y de autoservicio.

El alcance comprende tres soluciones diferenciadas según su contexto de uso y rol dentro del modelo de negocio:
1. **Aplicación Web Administrativa (Desktop):** Plataforma de gestión centralizada para directores de hotel y administradores de Smart Stay, orientada a la visualización analítica, auditoría de reservas, reportería financiera y parametrización de sedes.
2. **Aplicación Móvil Staff (Android Nativo):** Diseñada para el personal operativo (housekeeping, recepción, mantenimiento), priorizando la ergonomía táctil con una sola mano, accesibilidad inmediata a tareas pendientes y registro ágil de turnos.
3. **Aplicación Móvil Guest (Flutter):** Plataforma para el huésped enfocada en la autonomía de su estadía, integrando el control domótico/IoT de la habitación, solicitud directa de servicios complementarios y asistencia en tiempo real.

---

### 6.4.1. Applications Wireframes

Los wireframes representan la estructura monocromática de baja/media fidelidad de las aplicaciones. Se prescinde de elementos visuales secundarios, colores de acento e imágenes decorativas para concentrar la atención en la distribución del espacio, la navegación principal, la jerarquía visual de los datos y el cumplimiento de las zonas interactivas mínimas (48 × 48 dp en entornos móviles).

---

#### 6.4.1.1. Web Application Wireframes – Modo Administrador

La interfaz administrativa adopta un patrón clásico con barra lateral persistente (sidebar) a la izquierda, barra superior de control (top bar) con buscador global y notificaciones, y un área de trabajo central diseñada para optimizar la visualización de grandes volúmenes de datos.

*Dashboard administrativo y Gestión de Huéspedes*
![Wireframes Dashboard y Huéspedes](assets/images/cap6/wdashboard_huespedes.png)

1. **Dashboard:**
   - **Propósito:** Ofrecer una visión ejecutiva del desempeño del hotel en tiempo real.
   - **Elementos clave:** Indicadores clave de desempeño (ingresos generados vs. semana previa, ocupación total en gráfico de anillo con segmentación por tarde/noche), métricas de reservas diarias, calificación consolidada de servicios (IoT, alimentos, empaque) y ranking de sedes por rendimiento.
2. **Huéspedes (Guests):**
   - **Propósito:** Administrar la base de datos de clientes y reservas corporativas.
   - **Elementos clave:** Barra superior con motor de búsqueda y filtros multivariable (sede, rango de fecha), tabla estructurada con casillas de selección, datos del cliente (nombre, sede, estado de negociación/reserva), botones para exportación/importación y paginador interactivo.

*Gestión de Staff y Módulo de Hoteles / Habitaciones*
![Wireframes Staff y Hoteles](assets/images/cap6/wstaff_hoteles.png)

3. **Staff:**
   - **Propósito:** Supervisar al personal operativo y administrar sus niveles de acceso.
   - **Elementos clave:** Filtro por sede, controles de acción rápida (editar, eliminar, añadir usuario), tabla detallada con nombre, rol asignado (Admin, Restaurant Manager, Maintenance, Receptionist), teléfono, correo corporativo, último acceso y estado de activación (Active / Inactive).
4. **Hoteles y Habitaciones:**
   - **Propósito:** Parametrizar la infraestructura física y los activos tecnológicos de cada sucursal.
   - **Elementos clave:** Listado de sedes con capacidad total de habitaciones, panel lateral de detalle de la sede seleccionada (gestión de servicios y stock), buscador específico por número de habitación y ficha de detalle de habitación indicando tipo, comodidades, estado de ocupación y recursos tecnológicos vinculados.

*Gestión de Reservas y Reportes Financieros / Gastos*
![Wireframes Reservas y Gastos](assets/images/cap6/wreservas_gastos.png)

5. **Reservas (Booking):**
   - **Propósito:** Control visual y cronológico de la ocupación hotelera.
   - **Elementos clave:** Selector de vista (Día, Semana, Mes), selector de fecha (calendario desplegable), buscador de habitación, grilla matricial donde se grafican bloques de estadía con el nombre del huésped y estados de mantenimiento bloqueados.
6. **Pagos y Gastos (Payments):**
   - **Propósito:** Auditoría y conciliación de flujos de caja operativos e ingresos por servicios.
   - **Elementos clave:** Tablas de desglose para pagos recibidos (ingresos por cliente y método de pago), egresos a proveedores/personal y control de inventario de suministros operativos. Incluye gráficas comparativas de ingresos por sede, distribución porcentual de métodos de pago y evolución acumulada de ingresos.

*Servicios, Productos, Reseñas y Tickets de Soporte*
![Wireframes Servicios, Productos y Reseñas](assets/images/cap6/wservicio_producto_reseña.png)
![Wireframes Soporte](assets/images/cap6/wsoporte.png)

7. **Servicios y Productos:**
   - **Propósito:** Catálogo maestro y control del ciclo de vida de los dispositivos IoT y amenidades.
   - **Elementos clave:** Matriz de inventario con identificador, tipo de dispositivo (Smart TV, cerradura inteligente, sensor de movimiento, etc.), estado funcional, stock, sede física, habitación asignada, proveedor y fecha de garantía vigente.
8. **Reseñas:**
   - **Propósito:** Monitorear el índice de satisfacción de huéspedes y la retroalimentación del personal.
   - **Elementos clave:** Registro cronológico de comentarios con puntuación por estrellas, categorización por sede y gráficas de dispersión de calificaciones a lo largo de las semanas operativas.
9. **Soporte (Support):**
   - **Propósito:** Gestión interna de incidencias y solicitudes hacia el equipo técnico de Smart Stay.
   - **Elementos clave:** Formulario estructurado para generación de ticket (categoría de problema, nivel de severidad/prioridad, descripción), tabla de seguimiento de tickets emitidos y panel lateral con el historial de mensajes de resolución.

---

#### 6.4.1.2. Mobile Applications Wireframes – Modo Staff (Android Nativo)

La aplicación móvil para el personal del hotel está diseñada para operar con agilidad durante los recorridos operativos, destacando estados por medio de contraste y tipografía estructurada.

*Autenticación, Turnos y Tareas Operativas del Staff*
![Wireframes Staff Flujo 1](assets/images/cap6/wappstaff1.png)

1. **IntroApp & Login:**
   - **Propósito:** Autenticación segura del trabajador en el sistema del hotel.
   - **Elementos clave:** Pantalla inicial con isotipo de la marca y selector de sede; formulario de ingreso con campos para correo electrónico institucional, contraseña enmascarada y opción de recuperación de credenciales.
2. **Home / Dashboard Staff:**
   - **Propósito:** Centralizar el registro de asistencia del colaborador y las notificaciones prioritarias.
   - **Elementos clave:** Módulo de marcación de jornada con botones de un toque para *Entrada*, *Receso* y *Salida*; tabla de historial semanal con cómputo de horas trabajadas y resumen de avisos inmediatos.
3. **Tareas (Tasks):**
   - **Propósito:** Desplegar y actualizar el flujo diario de actividades operativas.
   - **Elementos clave:** Listado agrupado por número de habitación, tipo de tarea (limpieza regular, reposición de minibar, preparación para check-in), número de piso y estado de ejecución (Pendiente / Completado). Al concluir la carga diaria se presenta una retroalimentación de estado vacío amigable.

*Servicios a la Habitación, Reservas y Perfil del Colaborador*
![Wireframes Staff Flujo 2](assets/images/cap6/wappstaff2.png)

4. **Servicios y Entregas:**
   - **Propósito:** Gestionar y validar las órdenes realizadas por los huéspedes.
   - **Elementos clave:** Tabla con número de habitación destino, ítem solicitado (Room service, toallas adicionales, reposición de agua), cantidad requerida y control de estado de entrega.
5. **Reservas (Check-in / Check-out):**
   - **Propósito:** Facilitar la recepción y despedida de huéspedes directamente en piso.
   - **Elementos clave:** Buscador dinámico por nombre o habitación; tabla detallada con fecha de arribo, nombre del cliente, estado del check-in y estado del check-out.
6. **Perfil y Notificaciones Operativas:**
   - **Propósito:** Gestión de la cuenta del trabajador y recepción de alertas críticas.
   - **Elementos clave:** Vista de perfil con avatar, datos de contacto, opción de cambio de contraseña y cierre de sesión. Módulo de notificaciones desplegado como tarjetas flotantes con botón de confirmación de lectura rápida.

---

#### 6.4.1.3. Mobile Applications Wireframes – Modo Huésped (Flutter)

La interfaz del huésped se orienta al confort y al autoservicio, minimizando los pasos necesarios para controlar el ambiente físico o solicitar comodidades adicionales.

*Acceso, Hub de Estadía y Control IoT de Habitación*
![Wireframes Huésped Flujo 1](assets/images/cap6/waphuesped1.png)

1. **IntroApp & Home:**
   - **Propósito:** Recibir al usuario tras el escaneo del código QR de la reserva y concentrar los accesos directos de la estadía.
   - **Elementos clave:** Barra superior con saludo personalizado, buscador de servicios y acceso a alertas. En el cuerpo principal se destaca la tarjeta digital para activación de la cerradura electrónica (*Llave Digital*), accesos rápidos a *Ordenar* o *Asistencia*, y carrusel de promociones activas.
2. **Mi Habitación (IoT Control):**
   - **Propósito:** Control ambiental y domótico integral del cuarto asignado.
   - **Elementos clave:** Encabezado con número de habitación y estado de ocupación; controles deslizantes (sliders) para graduar la temperatura del aire acondicionado e intensidad lumínica; interruptores binarios (On/Off) para cortinas motorizadas y TV; accesos inferiores para solicitud inmediata de limpieza, snacks o botón de auxilio (*SOS Emergencia*).

*Catálogo de Servicios, Geolocalización y Datos Personales*
![Wireframes Huésped Flujo 2](assets/images/cap6/wapphuesped2.png)

3. **Servicios (Services):**
   - **Propósito:** Exploración y contratación de amenidades hoteleras complementarias.
   - **Elementos clave:** Bloque superior para restaurantes y room service; grilla de servicios fijos con íconos representativos (Parking, Piscina, Bares, Gimnasio, Zona Pet Friendly); y listado inferior de eventos programados en el hotel.
4. **Mapa (Wayfinding & Entorno):**
   - **Propósito:** Guiar al huésped dentro de las instalaciones y presentar puntos de interés turísticos externos.
   - **Elementos clave:** Buscador con filtros por categoría; visor de mapa interactivo con pines de ubicación y tarjeta flotante con descripción resumida de la atracción o servicio seleccionado.
5. **Perfil y Notificaciones:**
   - **Propósito:** Visualizar datos de la cuenta, métodos de pago y comunicaciones del hotel.
   - **Elementos clave:** Visualización de tarjetas de crédito/débito enlazadas con opción para registrar un nuevo método de pago (*Add New Card*). Superposición de avisos emergentes con confirmaciones de pedidos, recordatorios de check-out y mensajes del conserje.

---

### 6.4.2. Applications Wireflow Diagrams

Los diagramas de flujo basados en wireframes (*Wireflow Diagrams*) integran la distribución esquemática de las pantallas con las rutas de navegación e interacción del usuario dentro de cada aplicación de la solución. Permiten evaluar la arquitectura de transiciones, la accesibilidad de las acciones y la respuesta ante cambios de estado entre módulos.

---

#### 6.4.2.1. Web Application Wireflow – Modo Administrador

* **User Persona:** Administrador de Hotel Boutique / Director de Operaciones.
* **User Goal:** Monitorear el rendimiento general del hotel desde el panel de control, auditar las reservas activas y verificar la satisfacción del cliente en las distintas sedes.

![Wireflow Modo Administrador](assets/images/cap6/wireflow_admin.png)

**Estructura y comportamiento del flujo:**
1. **Punto de entrada:** El usuario accede a través de la pantalla **Intro / Acceso**, la cual valida la sesión administrativa y transfiere el control directamente al **Dashboard**.
2. **Navegación centralizada:** El **Dashboard** actúa como núcleo operativo. Desde sus tarjetas analíticas, botones de acción rápida permiten bifurcaciones directas hacia módulos clave:
   - Los indicadores de ingresos y ocupación enlazan a **Booking** y **Payments**.
   - Los accesos rápidos de incidencias y opiniones derivan a **Reviews** y **Support**.
3. **Barra de navegación persistente (Sidebar):** Permite el desplazamiento directo hacia cualquiera de las 9 secciones del sistema:
   - **Guests:** Consulta y gestión de perfiles de clientes. Se conecta de forma bidireccional con **Booking** para auditar el detalle de los huéspedes asignados a cada reserva.
   - **Staff:** Administración de cuentas, turnos y roles del personal.
   - **Hotels / Rooms:** Catálogo de sedes y parametrización de habitaciones.
   - **Booking:** Calendario interactivo matricial para el control de ocupación.
   - **Payments:** Conciliación contable de pagos de huéspedes y compras operativas.
   - **Services / Products:** Inventario y monitoreo de dispositivos IoT e insumos.
   - **Reviews:** Panel consolidado de calificaciones y retroalimentación. Se nutre de la información proveniente de **Staff**, **Guests** y **Hotels / Rooms**.
   - **Support:** Mesa de ayuda y seguimiento de tickets técnicos emitidos a Smart Stay.

---

#### 6.4.2.2. Mobile Application Wireflow – Modo Staff (Android Nativo)

* **User Persona:** Personal Operativo / Housekeeping / Mantenimiento.
* **User Goal:** Autenticar el inicio de jornada, consultar las actividades asignadas del día y registrar el cumplimiento de servicios o limpieza en habitaciones.

![Wireflow Modo Staff](assets/images/cap6/wireflow_staff.png)

**Estructura y comportamiento del flujo:**
1. **Autenticación obligatoria:** Dado el contexto de turnos rotativos, el flujo inicia en **01 - Intro**, avanzando hacia la pantalla de **Login**, donde el colaborador ingresa sus credenciales corporativas (correo y contraseña).
2. **Panel principal (Home):** Tras la autenticación, se presenta la vista **Home**, que contiene el módulo de registro de jornada (*Entrada*, *Receso*, *Salida*), el historial de horas acumuladas y el resumen de alertas inmediatas.
3. **Navegación inferior (Bottom Navigation Bar):** Proporciona acceso ergonómico con una sola mano hacia las áreas de trabajo:
   - **Tasks:** Lista priorizada de actividades del día (limpieza, reposición de minibar, preparación de cuartos). Al completar una tarea, el sistema actualiza el estado local y sincroniza el inventario con el sistema central.
   - **Services:** Registro y confirmación de entrega de pedidos solicitados por los huéspedes (room service, toallas adicionales).
   - **Booking:** Consulta del estado de llegadas (*Check-in*) y salidas (*Check-out*) en tiempo real.
   - **Profile:** Parámetros de la cuenta del trabajador, cambio de clave y cierre de sesión.
4. **Capa persistente de alertas:** El icono de **Notifications**, ubicado en la barra superior de todas las pantallas, despliega modales flotantes superpuestos con avisos urgentes sobre cambios de turno o incidencias prioritarias, sin perder el contexto de la tarea actual.

---

### 6.4.2. Applications Wireflow Diagrams

Los diagramas de flujo basados en wireframes (*Wireflow Diagrams*) integran la distribución esquemática de las pantallas con las rutas de navegación e interacción del usuario dentro de cada aplicación de la solución. Permiten evaluar la arquitectura de transiciones, la accesibilidad de las acciones y la respuesta ante cambios de estado entre módulos.

---

#### 6.4.2.1. Web Application Wireflow – Modo Administrador

* **User Persona:** Administrador de Hotel Boutique / Director de Operaciones.
* **User Goal:** Monitorear el rendimiento general del hotel desde el panel de control, auditar las reservas activas y verificar la satisfacción del cliente en las distintas sedes.

![Wireflow Modo Administrador](assets/images/cap6/webwireflowadmi.png)

**Estructura y comportamiento del flujo:**
1. **Punto de entrada:** El usuario accede a través de la pantalla **Intro / Acceso**, la cual valida la sesión administrativa y transfiere el control directamente al **Dashboard**.
2. **Navegación centralizada:** El **Dashboard** actúa como núcleo operativo. Desde sus tarjetas analíticas, botones de acción rápida permiten bifurcaciones directas hacia módulos clave:
   - Los indicadores de ingresos y ocupación enlazan a **Booking** y **Payments**.
   - Los accesos rápidos de incidencias y opiniones derivan a **Reviews** y **Support**.
3. **Barra de navegación persistente (Sidebar):** Permite el desplazamiento directo hacia cualquiera de las 9 secciones del sistema:
   - **Guests:** Consulta y gestión de perfiles de clientes. Se conecta de forma bidireccional con **Booking** para auditar el detalle de los huéspedes asignados a cada reserva.
   - **Staff:** Administración de cuentas, turnos y roles del personal.
   - **Hotels / Rooms:** Catálogo de sedes y parametrización de habitaciones.
   - **Booking:** Calendario interactivo matricial para el control de ocupación.
   - **Payments:** Conciliación contable de pagos de huéspedes y compras operativas.
   - **Services / Products:** Inventario y monitoreo de dispositivos IoT e insumos.
   - **Reviews:** Panel consolidado de calificaciones y retroalimentación. Se nutre de la información proveniente de **Staff**, **Guests** y **Hotels / Rooms**.
   - **Support:** Mesa de ayuda y seguimiento de tickets técnicos emitidos a Smart Stay.

---

#### 6.4.2.2. Mobile Application Wireflow – Modo Staff (Android Nativo)

* **User Persona:** Personal Operativo / Housekeeping / Mantenimiento.
* **User Goal:** Autenticar el inicio de jornada, consultar las actividades asignadas del día y registrar el cumplimiento de servicios o limpieza en habitaciones.

![Wireflow Modo Staff](assets/images/cap6/webwireflowstaff.png)

**Estructura y comportamiento del flujo:**
1. **Autenticación obligatoria:** Dado el contexto de turnos rotativos, el flujo inicia en **01 - Intro**, avanzando hacia la pantalla de **Login**, donde el colaborador ingresa sus credenciales corporativas (correo y contraseña).
2. **Panel principal (Home):** Tras la autenticación, se presenta la vista **Home**, que contiene el módulo de registro de jornada (*Entrada*, *Receso*, *Salida*), el historial de horas acumuladas y el resumen de alertas inmediatas.
3. **Navegación inferior (Bottom Navigation Bar):** Proporciona acceso ergonómico con una sola mano hacia las áreas de trabajo:
   - **Tasks:** Lista priorizada de actividades del día (limpieza, reposición de minibar, preparación de cuartos). Al completar una tarea, el sistema actualiza el estado local y sincroniza el inventario con el sistema central.
   - **Services:** Registro y confirmación de entrega de pedidos solicitados por los huéspedes (room service, toallas adicionales).
   - **Booking:** Consulta del estado de llegadas (*Check-in*) y salidas (*Check-out*) en tiempo real.
   - **Profile:** Parámetros de la cuenta del trabajador, cambio de clave y cierre de sesión.
4. **Capa persistente de alertas:** El icono de **Notifications**, ubicado en la barra superior de todas las pantallas, despliega modales flotantes superpuestos con avisos urgentes sobre cambios de turno o incidencias prioritarias, sin perder el contexto de la tarea actual.

---

#### 6.4.2.3. Mobile Application Wireflow – Modo Huésped (Flutter)

* **User Persona:** Huésped Turista / Viajero Corporativo.
* **User Goal:** Gestionar la comodidad de su estancia de manera autónoma, controlando los dispositivos domóticos de su habitación y explorando los servicios disponibles del hotel.

![Wireflow Modo Huésped](assets/images/cap6/webwireflowhuesped.png)

**Estructura y comportamiento del flujo:**
1. **Bienvenida e inducción:** Inicia en la vista **01 - Intro**, que da la bienvenida al usuario con la identidad del hotel tras escanear el código QR de registro, transicionando automáticamente a la pantalla principal **Home**.
2. **Hub de estancia (Home):** Concentra los accesos prioritarios: la tarjeta de activación de la cerradura electrónica (*Digital Key*), botones directos para llamadas de *Asistencia* y *Ordenar*, junto con un carrusel de promociones activas.
3. **Navegación inferior persistente:**
   - **My Room (Habitación):** Interfaz domótica central para el ajuste de actuadores y sensores IoT (graduación de temperatura, intensidad lumínica, apertura de cortinas y control de TV), además de accesos rápidos a limpieza y botón de emergencia (*SOS*).
   - **Services:** Catálogo de amenidades divididas en gastronomía (restaurantes), bienestar (gimnasio, piscina), comodidades (parking, pet friendly) y eventos programados.
   - **Map:** Visor interactivo con puntos de interés tanto internos (instalaciones del hotel) como turísticos en el entorno urbano.
   - **Profile:** Ficha con los datos de contacto del huésped y módulo de pasarela para el registro seguro de tarjetas de crédito/débito (*Add New Card*).
4. **Alertas y seguimiento:** El icono superior de **Notifications** permite consultar en cualquier momento la confirmación de solicitudes de servicio, recordatorios de estadía y avisos directos de recepción.

### 6.4.3. Applications Mock-ups

Los mock-ups de alta fidelidad representan la apariencia visual y estilística definitiva de los productos digitales que conforman la solución Smart Stay. A diferencia de los wireframes estructurales, en esta etapa se materializa el Design System establecido en la sección 6.1: aplicación de la paleta cromática (azul corporativo `#0D2A4A`, naranja de acento `#F26522`, neutros y colores semánticos), tipografía jerárquica (Cocomat Pro para títulos y Open Sans para cuerpo/acciones), iconografía vectorial con significado accesible y componentes táctiles de al menos 48 × 48 dp.

---

#### 6.4.3.1. Web Application Mock-ups – Modo Administrador

La interfaz de escritorio está optimizada para la supervisión analítica de los administradores y directores de cadenas hoteleras. El layout aplica una barra lateral fija en azul corporativo con contraste accesible, barra superior con identificación de usuario y un área de trabajo espaciosa con tarjetas elevadas y gráficos de lectura rápida.

*Módulos de Dashboard, Huéspedes, Staff y Hoteles/Habitaciones*
![Mockups Administrador Bloque 1](assets/images/cap6/mockupadmin1.png)

1. **Dashboard:**
   - Incorporación de los colores de marca en los gráficos analíticos: barras comparativas de ingresos en azul corporativo, indicadores clave en tarjetas blancas con sombras sutiles y gráfico de anillo de ocupación con resaltado del bloque horario vespertino en acento naranja.
   - Métricas de calificación consolidada por servicio (IoT, comida, amenities) con visualización porcentual de alta legibilidad.
2. **Huéspedes (Guests):**
   - Tabla interactiva con microinteracciones en casillas de selección, chips de estado semánticos (En Negociación, Reservación, Incidencia) y botones de acción rápida (*Add New*, *Import/Export*) con elevación visual.
   - Paginación estructurada y motor de búsqueda con iconos vectoriales en la cabecera.
3. **Staff:**
   - Visualización del equipo de trabajo mediante avatars, tipografía estructurada para roles institucionales (*Admin*, *Receptionist*, *Maintenance*) y botones tipo switch/chip para el estado de cuenta (*Active* / *Inactive*).
4. **Hoteles y Habitaciones:**
   - Tabla maestra de sucursales combinada con panel lateral de previsualización en naranja corporativo. Muestra la fotografía de la suite seleccionada, ficha técnica de servicios y recursos domóticos disponibles.

*Módulos de Reservas, Pagos, Servicios/Productos y Reseñas*
![Mockups Administrador Bloque 2](assets/images/cap6/mockupadmin2.png)

5. **Reservas (Booking):**
   - Calendario matricial con bloques cromáticos diferenciados para distinguir reservas confirmadas, períodos de mantenimiento técnico y asignación de huéspedes por suite.
6. **Pagos y Gastos (Payments):**
   - Panel de auditoría contable con gráficos de barras (ingresos vs. gastos por sede), gráfico de sectores para distribución de métodos de pago (Visa, Mastercard, Yape, Plin) y curva acumulada de facturación mensual.
7. **Servicios y Productos:**
   - Registro de inventario con tarjetas de resumen para stock disponible, fechas de mantenimiento técnico y garantía de hardware IoT con borde perimetral en naranja institucional.
8. **Reseñas (Reviews):**
   - Panel de comentarios con escala de estrellas doradas, desglose por sede hotelera y gráficos de barras horizontales que resumen la satisfacción acumulada por semana.

*Módulo de Soporte y Mesa de Ayuda*
![Mockups Administrador Bloque 3](assets/images/cap6/mockupadmin3.png)

9. **Soporte:**
   - Formulario de emisión de tickets en tarjeta destacada con botón primario *Generar ticket* en naranja corporativo.
   - Tabla de seguimiento con indicadores cromáticos de severidad (Alta en rojo, Media en amarillo) y panel lateral con hilo de conversación interactivo entre el hotel y el equipo técnico de Smart Stay.

---

#### 6.4.3.2. Mobile Application Mock-ups – Modo Staff (Android Nativo)

La aplicación móvil para el personal operativo adopta una interfaz con fondos en azul corporativo y tarjetas contrastadas, diseñada para facilitar la lectura en movimiento y evitar pulsaciones erróneas durante el trabajo de campo.

*Autenticación, Turno Diario y Lista de Tareas*
![Mockups Staff Bloque 1](assets/images/cap6/mockupstaff1.png)

1. **Intro & Login:**
   - Pantalla de bienvenida en azul corporativo con el isotipo oficial de Smart Stay e identificación de la sede operativa (*Hotel del Sur*).
   - Formulario de autenticación con campos de entrada accesibles, tipografía Open Sans y botón primario de acceso en azul contrastado.
2. **Home / Turnos:**
   - Panel central de marcación de jornada laboral con botones de acción directa en naranja corporativo (*Entrada*) y neutros (*Receso*, *Salida*), complementado por la tabla del historial semanal de horas.
3. **Tareas del Día (Tasks):**
   - Cabecera en naranja de acento que destaca el módulo activo.
   - Listado tabular de cuartos con etiquetas semánticas de estado: pendientes con indicador de atención y completadas con check de confirmación. Al concluir las labores, despliega una ilustración amigable de estado resuelto.

*Gestión de Entregas, Reservas en Piso y Perfil Operativo*
![Mockups Staff Bloque 2](assets/images/cap6/mockupstaff2.png)

4. **Servicios / Entregas:**
   - Lista de órdenes solicitadas por los huéspedes (room service, aguas, toallas) enmarcada en una tarjeta con acento visual, permitiendo validar la entrega de manera táctil.
5. **Reservas (Check-in / Check-out):**
   - Buscador rápido y listado con indicadores cromáticos de estado (semáforo de llegadas y salidas de huéspedes).
6. **Perfil y Notificaciones Operativas:**
   - Ficha del colaborador con fotografía, credenciales corporativas y botones de acción diferenciados (*Editar*, *Cambiar contraseña*, *Cerrar Sesión* en naranja).
   - Modales flotantes de notificaciones de alta prioridad con botones de confirmación *Ok* y cierre explícito.

---

#### 6.4.3.3. Mobile Application Mock-ups – Modo Huésped (Flutter)

La solución para el huésped ofrece una experiencia de autoservicio visualmente cálida y moderna. Emplea superficies claras, tarjetas con bordes redondeados y microinteracciones fluidas para el control domótico de la habitación.

*Acceso, Hub de Estadía y Control Domótico IoT*
![Mockups Huésped Bloque 1](assets/images/cap6/mockuphuesped1.png)

1. **Intro & Bienvenida:**
   - Vista de recepción con branding formal en azul corporativo y saludo inicial al huésped tras validar el acceso de su reserva.
2. **Home (Hub de Estadía):**
   - Saludo personalizado en cabecera junto con iconos de búsqueda y notificaciones.
   - Tarjeta central destacada en naranja corporativo que aloja la **Llave Digital** con iconografía de activación.
   - Accesos directos inferiores para *Ordenar* y *Asistencia*, seguidos de tarjetas de promociones activas.
3. **Mi Habitación (Control IoT):**
   - Panel de control ambiental con sliders táctiles para graduar la temperatura del climatizador y la intensidad de iluminación.
   - Controles tipo switch (On/Off) en azul corporativo para cortinas motorizadas y encendido del televisor.
   - Cuadrícula de accesos rápidos para solicitar limpieza, snacks a la habitación o accionar el botón de emergencia (*SOS*).

*Servicios Hoteleros, Geolocalización y Billetera Digital*
![Mockups Huésped Bloque 2](assets/images/cap6/mockuphuesped2.png)

4. **Nuestros Servicios:**
   - Tarjetas categorizadas por banners en azul oscuro para restaurantes y eventos, combinadas con una grilla de botones táctiles para servicios complementarios (Parking, Piscina, Bar, Gimnasio, Pet Friendly).
5. **Mapa (Wayfinding y Entorno):**
   - Mapa interactivo con pines de ubicación y tarjeta flotante con vista previa del destino, precio y porcentaje de descuento.
6. **Perfil y Métodos de Pago:**
   - Tarjeta virtual en degradado turquesa para la visualización de la tarjeta de crédito predeterminada y botón *+ Add New Card* para el registro de nuevos métodos de pago.
   - Capa de notificaciones superpuestas con avisos informativos sobre el estado de las solicitudes enviadas.

   ### Applications User Flow Diagrams

Los diagramas de flujo de usuario (*User Flow Diagrams*) modelan el recorrido lógico, secuencial y decisional que experimenta cada perfil de usuario al interactuar con las soluciones digitales de Smart Stay. Para cada segmento objetivo, se mapea tanto el camino ideal (*Happy Path*), donde las tareas se completan sin fricción, como las rutas alternativas o escenarios de error (*Unhappy Paths*), en los que se anticipan fallos de validación, interrupciones de conectividad o restricciones de disponibilidad operativa.

---

#### 1. Rol: Administrador del Hotel (Web Application)

* **User Persona:** Director de Operaciones / Administrador General.
* **User Goal:** Configurar los datos de la sede hotelera, parametrizar habitaciones/servicios y auditar métricas operativas y financieras desde el panel de control.
* **Enlace interactivo de alta resolución:** [Ver flujos del Administrador en Figma](https://shorturl.at/7UPcY)

**Happy Path (Camino Ideal):**
El usuario inicia en *Opens App*, selecciona *Login* e ingresa su correo y contraseña. Tras la validación afirmativa (*Credentials valid?* = Yes), accede al *Dashboard*. El sistema comprueba si el hotel ya fue creado (*Already hotels created?* = Yes) y despliega el menú operativo para: registrar cuentas de staff/huéspedes, añadir tarifas, auditar reservas y pagos, monitorear incidencias, revisar calificaciones y emitir códigos de acceso, concluyendo con *Logs out successfully*.

![Happy Path - Administrador](assets/images/cap6/happypathadmi.png)

**Unhappy Paths (Rutas Alternativas y Manejo de Errores):**
* *Fallo de autenticación:* Si las credenciales no son válidas (*Credentials valid?* = No), se despliega el aviso *"Incorrect credentials"*, derivando a *Forgot password* para recibir el enlace de restablecimiento vía correo electrónico.
* *Sede inexistente o perfil incompleto:* Si aún no se han registrado hoteles (*Already hotels created?* = No), el flujo fuerza el desvío a *Go to section Hotels*. Si faltan campos obligatorios (*Complete hotel profile?* = No), bloquea el acceso con la alerta *"Complete required fields"* hasta completar nombre, dirección y fotos.
* *Registro duplicado:* En la configuración de habitaciones o amenidades, si se intenta ingresar un identificador ya existente (*Duplicated entry?* = Yes), el sistema emite el mensaje *"Room/service already exists"* antes de reintentar el guardado.

![Unhappy Path - Administrador](assets/images/cap6/unhappypathadmi.png)

---

#### 2. Rol: Huésped del Hotel (Flutter Mobile App)

* **User Persona:** Huésped Turista / Viajero de Negocios.
* **User Goal:** Realizar el check-in digital de manera autónoma, operar los controles domóticos de la habitación y solicitar servicios complementarios durante su estadía.
* **Enlace interactivo de alta resolución:** [Ver flujos del Huésped en Figma](https://shorturl.at/7UPcY)

**Happy Path (Camino Ideal):**
El huésped abre la aplicación (*Opens App*), ingresa sus credenciales previamente creadas (*Already registered?* = Yes) y accede a la sección principal *Home*. El sistema detecta que el check-in está pendiente (*Already did check-in?* = No), permitiendo completar el *Digital check-in*. Una vez activo, el huésped desbloquea la llave digital y detalles de habitación, solicita servicios adicionales, consulta el mapa del hotel y eventos, registra métodos de pago (tarjeta, Yape, Plin), procesa el *Digital check-out* y califica su estancia antes de cerrar sesión.

![Happy Path - Huésped](assets/images/cap6/happypathhuesped.png)

**Unhappy Paths (Rutas Alternativas y Manejo de Errores):**
* *Código de reserva no válido:* En el registro de nuevos usuarios, si el código otorgado por el hotel expira o es erróneo (*Is code valid?* = No), se genera el error *"Error: Invalid or expired access code"*, guiando a solicitar un nuevo token de acceso.
* *Check-in anticipado no permitido:* Si el huésped intenta registrar su llegada antes del horario estipulado (*Check-in allowed?* = No), se notifica *"Check-in opens later"* y la aplicación pasa a estado de espera.
* *Indisponibilidad de servicios:* Al solicitar room service o amenities, si el catálogo marca agotado (*Service available?* = No), el sistema deriva a la pantalla *Wait for service available* en lugar de procesar cobros fallidos.

![Unhappy Path - Huésped](assets/images/cap6/unhappypathhuesped.png)

---

#### 3. Rol: Personal Operativo / Staff (Android Native App)

* **User Persona:** Personal de Limpieza / Housekeeping / Mantenimiento.
* **User Goal:** Registrar el ingreso de la jornada laboral, consultar las tareas asignadas en piso y confirmar el cierre operativo de servicios e incidencias.
* **Enlace interactivo de alta resolución:** [Ver flujos del Staff en Figma](https://shorturl.at/7UPcY)

**Happy Path (Camino Ideal):**
El colaborador inicia la app (*Opens App*), se autentica con sus credenciales institucionales y accede a la pantalla principal (*Access home section*). De inmediato puede: marcar su asistencia laboral (*Marks laboral check-in and check-out*), revisar el listado de actividades del día (*Views daily assigned tasks*), reportar incidencias directamente a administración, auditar su historial de desempeño o agregar servicios solicitados por los huéspedes. Para cada tarea completada, puede adjuntar evidencia fotográfica opcional (*Uploads photo evidence*) y sincronizar el estado.

![Happy Path - Staff](assets/images/cap6/happypathstaff.png)

**Unhappy Paths (Rutas Alternativas y Manejo de Errores):**
* *Código corporativo erróneo:* Si el código de activación del hotel es inválido durante el alta del trabajador (*Is code valid?* = No), se bloquea el proceso con *"Error: Invalid or expired access code"*.
* *Credenciales no coincidentes:* En caso de contraseña incorrecta, se despliega *"Incorrect Credentials"* con acceso al restablecimiento vía enlace por correo.
* *Pérdida de conectividad en piso:* Durante las labores de mantenimiento o limpieza, al marcar una tarea como completada, el sistema valida la red (*Internet connection available?* = No); si no hay cobertura, retiene la transacción y emite la alerta *"Status not updated, try later"*, regresando al listado local sin pérdida de datos.

![Unhappy Path - Staff](assets/images/cap6/unhappypathstaff.png)

### 6.4.5. Applications Prototyping

El prototipado interactivo de las aplicaciones de Smart Stay tiene como propósito simular el comportamiento visual y de navegación del sistema antes de su implementación en código, permitiendo evaluar la usabilidad, la carga cognitiva y la consistencia de los flujos definidos en los User Flow Diagrams. 

Los prototipos fueron construidos sobre **Figma**, articulando las pantallas de alta fidelidad (mock-ups) mediante microinteracciones, transiciones dinámicas entre contenedores y respuestas de estado ante eventos de entrada.

#### Criterios y Características de Interacción

- **Navegación ergonómica y persistente:** Implementación de barras inferiores de navegación (*Bottom Navigation Bar*) en las interfaces móviles para garantizar el alcance táctil con una sola mano, y menús laterales persistentes (*Sidebar*) en la plataforma web administrativa.
- **Microinteracciones y feedback de estado:** Simulación de pulsaciones en botones primarios, interruptores para dispositivos domóticos (iluminación, aire acondicionado, cortinas), apertura de modales de confirmación y capas superpuestas de notificación.
- **Recorridos funcionales completos:** Cobertura de las rutas críticas (*happy path*) y rutas alternas (*unhappy paths*) para cada uno de los tres perfiles del sistema.

#### Recorridos Cubiertos en el Prototipo

1. **Huésped (Flutter Mobile App):**
   - Recepción e inducción inicial (Intro / QR de estadía).
   - Desbloqueo y operación de la *Llave Digital*.
   - Ajuste ambiental domótico en *Mi Habitación* (temperatura, luces, TV).
   - Exploración del catálogo de servicios hoteleros y navegación por el mapa interactivo.
   - Registro de métodos de pago en el perfil y gestión de check-out.

2. **Personal Operativo / Staff (Android Native App):**
   - Autenticación institucional segura (Login).
   - Marcación de jornada laboral (*Entrada*, *Receso*, *Salida*) en el Home.
   - Consulta, atención y actualización de tareas operativas diarias en piso.
   - Validación y entrega de pedidos a habitaciones en el módulo de *Servicios*.

3. **Administrador del Hotel (Web Application):**
   - Visualización analítica del *Dashboard* general (métricas de ocupación, ingresos y reseñas).
   - Gestión y auditoría matricial del calendario de reservas (*Booking*).
   - Control de inventario de suministros y hardware IoT (*Services & Products*).
   - Supervisión y asignación de roles al personal (*Staff*).

---

#### Evidencias y Enlaces del Prototipo

- **Enlace al Prototipo Interactivo en Figma:**  
  [Abrir Prototipo Interactivo Smart Stay](https://www.figma.com/make/lML4HR5vLsAGMUq3CoqvcS/Minimalist-Photo-Portfolio?t=7b0vXYUcbQwt6eOT-1&preview-route=%2Fguest%2Flogin)