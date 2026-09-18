<div style="page-break-before: always;"></div>

# Capítulo IV: Strategic-Level Software Design.

## 4.1. Strategic-Level Attribute-Driven Design.

### 4.1.1. Design Purpose.

### 4.1.2. Attribute-Driven Design Inputs.

#### 4.1.2.1. Primary Functionality (Primary User Stories).

#### 4.1.2.2. Quality Attribute Scenarios.

#### 4.1.2.3. Constraints.

#### 4.1.3. Architectural Drivers Backlog.

En el presente punto se define el Architectural Drivers Backlog de SmartStay, el cual consolida las Primary User Stories, los Quality Attribute Scenarios y los Constraints priorizados mediante la metodología Quality Attribute Workshop (QAW) en función de su importancia para los stakeholders y su impacto en la complejidad técnica. Este marco articula Functional Drivers clave (como reservas, check-in digital, control ambiental IoT, pagos y notificaciones) que demandan consistencia transaccional y comunicación física/reactiva, junto con Quality Attribute Drivers que imponen metas estrictas de seguridad (JWT/RBAC), rendimiento (500 req/s, latencia IoT < 500 ms), resiliencia (Circuit Breakers) y disponibilidad (recuperación < 10 s). Todos estos componentes se alinean de manera prioritaria (High/High) con restricciones técnicas no negociables como el diseño guiado por el dominio (DDD/Bounded Contexts), arquitectura Cloud Native en contenedores, interfaces API con OpenAPI 3.0 e integración asíncrona para IoT. 

| Driver ID | Título de Driver | Descripción | Importancia para Stakeholders | Impacto en Architecture Technical Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **FD-01** | Gestión centralizada de reservas y disponibilidad | SmartStay debe gestionar reservas y disponibilidad de habitaciones de manera centralizada, validando la disponibilidad y actualizando el inventario de forma atómica para evitar overbooking y mantener consistencia entre los componentes involucrados. | High | High |
| **FD-02** | Check-in digital y acceso automatizado | El sistema debe permitir que el huésped realice el check-in digital desde su dispositivo móvil y, después de validar identidad y pago, actualice el estado de la habitación, notifique al staff y genere las credenciales de acceso digital. | High | High |
| **FD-03** | Control ambiental IoT de la habitación | SmartStay debe permitir controlar temperatura e iluminación desde la aplicación móvil, validando la sesión del huésped y enviando los comandos mediante el backend hacia el broker o gateway IoT y los actuadores correspondientes. | High | High |
| **FD-04** | Procesamiento transaccional de pagos | El sistema debe procesar pagos y autorizaciones mediante pasarelas externas, utilizando comunicación cifrada, controles de seguridad y mecanismos que eviten bloquear los procesos principales de la aplicación. | High | High |
| **FD-05** | Despacho reactivo de notificaciones | La solución debe procesar eventos operativos, como check-out o incidencias de mantenimiento, y generar notificaciones automáticas al personal asignado para facilitar una respuesta oportuna. | High | Medium |
| **QA-01** | Seguridad y control de acceso | SmartStay debe proteger los datos y funcionalidades mediante autenticación, autorización basada en roles y validación de tokens, rechazando y auditando solicitudes no autorizadas y protegiendo también el acceso a actuadores IoT. | High | High |
| **QA-02** | Fiabilidad y resiliencia | El sistema debe aislar fallos de red o de servicios externos mediante Circuit Breaker, colas de reintento y mecanismos de degradación controlada, evitando errores en cascada y preservando la consistencia transaccional. | High | High |
| **QA-03** | Rendimiento y procesamiento en tiempo real | La arquitectura debe soportar cargas concurrentes de huéspedes y staff, consultas de disponibilidad, check-ins y telemetría IoT manteniendo los tiempos de respuesta definidos por los escenarios de calidad. | High | High |
| **QA-04** | Disponibilidad continua | SmartStay debe operar de manera continua y recuperarse ante fallos de instancias o nodos utilizando réplicas saludables, health checks, balanceo de carga y mecanismos automáticos de failover. | High | High |
| **QA-05** | Mantenibilidad y evolución | La arquitectura debe permitir incorporar nuevas integraciones tecnológicas, como nuevos sensores IoT o conectores externos, sin modificar ni detener los microservicios existentes y manteniendo una evolución controlada. | Medium | High |
| **C-01** | Domain-Driven Design y Bounded Contexts | La solución debe estructurarse bajo principios de DDD, separando los contextos IAM, Bookings, Accommodations, Payments e IoT, con límites claros para entidades, repositorios y reglas y sin compartir esquemas de datos directamente. | High | High |
| **C-02** | Cloud Native y contenedorización | Los servicios backend, APIs y componentes correspondientes deben empaquetarse en contenedores Docker y desplegarse en una plataforma Cloud/PaaS, manteniendo el servicio disponible y accesible mediante HTTPS. | High | High |
| **C-03** | Ecosistema móvil y web | SmartStay debe mantener una interacción consistente entre la Landing Page, la aplicación web administrativa y las aplicaciones móviles para huésped y staff, utilizando los servicios RESTful como mecanismo de integración. | High | Medium |
| **C-04** | Contratos API estandarizados con OpenAPI 3.0 | Los servicios expuestos deben adoptar un enfoque API-First y estar documentados mediante OpenAPI 3.0 y Swagger UI, incluyendo esquemas de request/response, parámetros y autenticación Bearer JWT. | Medium | High |
| **C-05** | Integración IoT y mensajería asíncrona | La arquitectura debe contemplar la recepción de telemetría y la emisión de comandos hacia sensores y actuadores mediante brokers de eventos/mensajería, como ActiveMQ o MQTT, o mediante emuladores de hardware. | High | High |

---

#### 4.1.4. Architectural Design Decisions.

En el presente punto se documentan las decisiones de diseño arquitectónico de SmartStay, las cuales derivan de los Architectural Drivers y se estructuran iterativamente bajo el enfoque del Quality Attribute Workshop (QAW). La selección de alternativas aborda las necesidades de este sistema distribuido y multicomponente, garantizando operación continua, procesamiento en tiempo real, seguridad avanzada, evolución independiente de sus módulos e integración eficiente con servicios externos y dispositivos IoT. 

| Driver ID | Título de Driver | Circuit Breaker (Pro) | Circuit Breaker (Con) | Retry + Message Queue (Pro) | Retry + Message Queue (Con) | Bulkhead (Pro) | Bulkhead (Con) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **AD-01** | Fiabilidad / Resiliencia | Aísla fallos de servicios externos y evita que se propaguen al resto del sistema. | Requiere configurar estados, umbrales y mecanismos de recuperación. | Permite reintentar operaciones fallidas y procesarlas posteriormente. | Puede generar duplicados y añade complejidad. | Aísla recursos para evitar que la saturación se propague. | Requiere mayor configuración y segmentación. |
| **AD-02** | Eficiencia / Rendimiento | Centraliza el acceso a los servicios y permite controlar y distribuir el tráfico. | Añade un componente adicional que debe mantenerse y monitorearse. | Reduce la latencia de consultas frecuentes y disminuye la carga sobre los servicios y la base de datos. | Requiere estrategias de actualización e invalidación de caché. | Permite procesamiento asíncrono y evita bloquear operaciones ante eventos y picos de carga. | Aumenta la complejidad de trazabilidad y gestión de eventos. |
| **AD-03** | Seguridad | Restringe las funcionalidades según el rol del usuario y permite una autorización diferenciada. | Requiere mantener correctamente los roles y permisos. | Permite autenticación basada en tokens y evita mantener sesiones centralizadas en el servidor. | Requiere gestionar expiración, almacenamiento y revocación de tokens. | Centraliza las validaciones de autenticación y autorización antes de acceder a los servicios internos. | Puede convertirse en un punto crítico si no dispone de mecanismos de alta disponibilidad. |
| **AD-04** | Mantenibilidad / Evolución | Delimita responsabilidades y reglas de negocio, reduciendo el acoplamiento entre dominios. | Requiere un modelado correcto del dominio y disciplina arquitectónica. | Separa la lógica de negocio de infraestructura y frameworks, facilitando mantenimiento y pruebas. | Introduce mayor número de capas y abstracciones. | Estandariza contratos y facilita incorporar nuevos clientes e integraciones. | Requiere mantener los contratos documentados y sincronizados. |
| **AD-05** | Disponibilidad | Distribuye el tráfico entre instancias y evita depender de un único nodo. | Requiere infraestructura y configuración adicional. | Detecta instancias no saludables y permite redirigir el tráfico hacia instancias disponibles. | Necesita monitoreo continuo y una estrategia correcta de recuperación. | Facilita despliegues reproducibles, escalamiento y recuperación de servicios. | Depende de una infraestructura cloud correctamente configurada. |

---

#### 4.1.5. Quality Attribute Scenario Refinements.

##### Scenario Refinement 1: Fiabilidad / Resiliencia

| Atributo | Descripción |
| :--- | :--- |
| **Scenario(s)** | Ante una falla de red o la indisponibilidad temporal de un servicio externo, como una OTA o una pasarela de pagos, una solicitud de sincronización o procesamiento no recibe respuesta dentro del tiempo esperado. |
| **Business Goals** | Garantizar la continuidad de las operaciones hoteleras y evitar que la indisponibilidad de un servicio externo provoque interrupciones en cadena, pérdida de información o inconsistencias en las transacciones. Esto permite mantener una operación confiable y reducir el impacto de fallos sobre reservas, pagos e integraciones externas. |
| **Relevant Quality Attributes** | Fiabilidad, resiliencia, disponibilidad y consistencia transaccional. |
| **Stimulus** | Una petición de sincronización con una OTA o una operación de pago permanece sin respuesta o alcanza un timeout prolongado debido a una falla de red o a la caída del servicio externo. |
| **Stimulus Source** | Servicio externo de integración, OTA o pasarela de pagos. |
| **Environment** | Operación normal del sistema SmartStay en producción, con usuarios y servicios activos. |
| **Artifact (if known)** | Microservicio de Integración, Billing y API Gateway. |
| **Response** | El sistema detecta la falla y activa el patrón Circuit Breaker para aislar el servicio afectado. La operación pendiente se almacena en una cola de reintento para su procesamiento posterior y el sistema proporciona una respuesta de degradación controlada, evitando que el fallo se propague hacia otros microservicios. La información transaccional debe conservar su consistencia. |
| **Response Measure** | El circuito debe abrirse en menos de 100 ms, sin pérdida de consistencia transaccional. Las operaciones recuperables deben permanecer registradas para permitir su posterior procesamiento. |
| **Questions** | ¿Cómo se determina el número máximo de reintentos antes de considerar una operación como fallida definitivamente? ¿Qué comportamiento tendrá el sistema cuando la dependencia externa permanezca indisponible durante un periodo prolongado? |
| **Issues** | Una estrategia de reintentos mal configurada podría generar saturación, duplicidad de operaciones o sobrecarga de los servicios externos. También debe controlarse que la recuperación de una transacción no produzca inconsistencias o procesamiento duplicado. |

<br>

##### Scenario Refinement 2: Eficiencia / Rendimiento

| Atributo | Descripción |
| :--- | :--- |
| **Scenario(s)** | Durante una hora punta, múltiples huéspedes y miembros del staff realizan simultáneamente consultas de disponibilidad, operaciones de check-in y consultas relacionadas con telemetría IoT. |
| **Business Goals** | Mantener una experiencia fluida para huéspedes y personal del hotel, incluso durante periodos de alta demanda, garantizando que las operaciones críticas puedan ejecutarse sin degradaciones significativas del servicio. |
| **Relevant Quality Attributes** | Rendimiento, escalabilidad, eficiencia y capacidad de respuesta. |
| **Stimulus** | Se generan peticiones concurrentes masivas relacionadas con disponibilidad de habitaciones, check-in y telemetría IoT, alcanzando aproximadamente 500 solicitudes por segundo. |
| **Stimulus Source** | Huéspedes, personal operativo y dispositivos o servicios IoT conectados al ecosistema SmartStay. |
| **Environment** | Picos de alta demanda en el entorno de producción. |
| **Artifact (if known)** | API Gateway, caché distribuida Redis y microservicios Core. |
| **Response** | El API Gateway distribuye el tráfico hacia los servicios correspondientes. Las consultas frecuentes se atienden mediante la capa de caché distribuida para reducir el acceso directo a los servicios Core, mientras que las operaciones apropiadas se procesan mediante mecanismos asíncronos y desacoplados. |
| **Response Measure** | El sistema debe mantener un tiempo de respuesta promedio de 1.5 segundos por petición HTTP, mientras que la latencia de procesamiento de la telemetría IoT debe mantenerse por debajo de 500 ms. |
| **Questions** | ¿Qué comportamiento tendrá el sistema cuando la carga supere las 500 solicitudes por segundo? ¿Qué información debe permanecer en caché y durante cuánto tiempo para evitar datos obsoletos de disponibilidad o estados de habitaciones? |
| **Issues** | Una capacidad insuficiente de caché o un crecimiento inesperado de la carga podría incrementar la latencia. Además, el uso de caché sobre información sensible al tiempo, como disponibilidad de habitaciones, puede generar inconsistencias si no se aplican mecanismos adecuados de actualización o invalidación. |

<br>

##### Scenario Refinement 3: Seguridad

| Atributo | Descripción |
| :--- | :--- |
| **Scenario(s)** | Un actor no autenticado o una solicitud manipulada intenta acceder a información de huéspedes, modificar operaciones del hotel o controlar actuadores IoT sin contar con los permisos requeridos. |
| **Business Goals** | Proteger la información de huéspedes y operaciones del hotel, evitar accesos no autorizados y garantizar que cada usuario solo pueda ejecutar las acciones correspondientes a su rol y contexto organizacional. |
| **Relevant Quality Attributes** | Seguridad, autenticación, autorización, trazabilidad e integridad. |
| **Stimulus** | Se recibe una solicitud que contiene un intento de inyección, escalada de privilegios o acceso no autorizado a datos o dispositivos IoT. |
| **Stimulus Source** | Actor externo o usuario autenticado que intenta realizar una operación fuera de sus permisos. |
| **Environment** | Operación continua del sistema bajo exposición pública mediante aplicaciones móviles y APIs. |
| **Artifact (if known)** | Módulo IAM y API Gateway. |
| **Response** | El sistema valida el token JWT y verifica las autorizaciones correspondientes mediante el modelo RBAC. Si la solicitud no cumple con las políticas de acceso, esta es rechazada y la operación queda registrada en la bitácora de auditoría. El control debe cubrir tanto el acceso a datos como las acciones sobre recursos y dispositivos IoT. |
| **Response Measure** | El 100 % de las peticiones no autorizadas debe ser rechazado mediante respuestas HTTP 401 o 403, acompañado por un registro de auditoría. |
| **Questions** | ¿Cómo se gestiona la revocación de tokens comprometidos? ¿Cómo se garantiza que un usuario con permisos administrativos de un hotel no pueda acceder a información de otra instancia o tenant? |
| **Issues** | Un error en las reglas RBAC o en el aislamiento por hotel podría provocar exposición de información entre tenants. También existe el riesgo de que una credencial válida comprometida permita ejecutar operaciones legítimas desde un origen no confiable, por lo que la autorización debe evaluarse en cada operación protegida. |

<br>

##### Scenario Refinement 4: Mantenibilidad / Evolución

| Atributo | Descripción |
| :--- | :--- |
| **Scenario(s)** | El equipo de ingeniería necesita incorporar una nueva integración tecnológica, como una nueva red de sensores IoT o un nuevo conector tecnológico, sin modificar ni detener los servicios existentes. |
| **Business Goals** | Permitir que SmartStay evolucione de manera continua y pueda incorporar nuevas tecnologías o integraciones sin generar cambios de alto impacto en el núcleo del sistema ni interrupciones para los hoteles usuarios. |
| **Relevant Quality Attributes** | Mantenibilidad, modificabilidad, extensibilidad, interoperabilidad y despliegue continuo. |
| **Stimulus** | El equipo de ingeniería recibe el requerimiento de incorporar un nuevo servicio o integración tecnológica. |
| **Stimulus Source** | Equipo de ingeniería y evolución del producto. |
| **Environment** | Entorno de integración y despliegue continuo mediante CI/CD. |
| **Artifact (if known)** | Bounded Contexts, contratos OpenAPI y microservicios asociados a la nueva integración. |
| **Response** | La separación de dominios mediante Domain-Driven Design permite desarrollar el nuevo componente de forma independiente. Los contratos definidos mediante OpenAPI facilitan la comunicación entre servicios y reducen el acoplamiento. El nuevo servicio puede ser construido, probado y desplegado sin modificar ni detener innecesariamente los microservicios existentes. |
| **Response Measure** | El tiempo de incorporación y despliegue del nuevo servicio debe ser inferior a 30 minutos, manteniendo zero-downtime a nivel global. |
| **Questions** | ¿Qué nivel de compatibilidad debe conservar un nuevo servicio con los contratos existentes? ¿Cómo se gestionarán los cambios incompatibles en las APIs sin afectar a las aplicaciones móviles actualmente desplegadas? |
| **Issues** | Una evolución descontrolada de contratos puede generar incompatibilidades entre versiones. Asimismo, una mala delimitación de los Bounded Contexts podría provocar dependencias excesivas y aumentar el costo de mantenimiento. |

## 4.2. Strategic-Level Domain-Driven Design.

### 4.2.1. EventStorming.

### 4.2.2. Candidate Context Discovery.

### 4.2.3. Domain Message Flows Modeling.

### 4.2.4. Bounded Context Canvases.

### 4.2.5. Context Mapping.

## 4.3. Software Architecture.

### 4.3.1. Software Architecture System Landscape Diagram.

### 4.3.2. Software Architecture Context Level Diagrams.

### 4.3.3. Software Architecture Container Level Diagrams.

### 4.3.4. Software Architecture Deployment Diagrams.
