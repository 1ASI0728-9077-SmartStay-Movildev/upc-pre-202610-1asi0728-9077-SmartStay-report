# Capítulo IV: Strategic-Level Software Design

## 4.1. Strategic-Level Attribute-Driven Design

### 4.1.1. Design Purpose
El objetivo fundamental del diseño arquitectónico para SmartStay consiste en estructurar una solución de software empresarial distribuida que impulse la evolución tecnológica dentro de la hotelería boutique. Hemos identificado que la problemática central radica en la fragmentación de las operaciones, la excesiva carga de procesos manuales que derivan en errores críticos y la falta de canales digitales autónomos para los huéspedes.

Con el fin de mitigar estas deficiencias, la arquitectura estratégica se enfoca en:
* **Optimización de objetivos de negocio y operativos:** Desarrollar un ecosistema reactivo y multicomponente que permita la sincronización inmediata de estados de ocupación, flujos de limpieza (*housekeeping*) y gestión de incidencias, reduciendo ineficiencias en los recursos del hotel.
* **Autonomía del huésped mediante innovación digital:** Proveer una experiencia de usuario fluida a través de registros de entrada y salida automatizados, así como el control domótico (IoT) del ambiente de la habitación mediante aplicaciones móviles integradas.
* **Aseguramiento de atributos de calidad en sistemas complejos:** Implementar una base técnica desacoplada bajo enfoques de Domain-Driven Design (DDD) y eventos, garantizando una operatividad constante (24/7), rapidez en la respuesta bajo alta concurrencia, resiliencia operativa y flexibilidad para despliegues en la nube.

---

### 4.1.2. Attribute-Driven Design Inputs
Bajo el marco de la metodología Attribute-Driven Design (ADD), establecemos un diseño arquitectónico estratégico que prioriza rigurosamente tres dimensiones fundamentales (*Inputs*): los flujos funcionales de mayor impacto, escenarios de calidad cuantificables y las limitaciones técnicas o comerciales ineludibles.

#### 4.1.2.1. Primary Functionality (Primary User Stories)
Se han seleccionado aquellas épicas e historias de usuario cuyo procesamiento, volumen de transacciones o naturaleza distribuida condicionan directamente las decisiones estructurales del sistema (aislamiento de datos, procesamiento asíncrono, integración IoT y pasarelas externas).

<table>
  <thead>
    <tr>
      <th>Epic / User Story ID</th>
      <th>Título</th>
      <th>Descripción</th>
      <th>Criterios de Aceptación</th>
      <th>Relacionado con (Epic ID)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>US-07</strong></td>
      <td>Gestión centralizada de reservas y disponibilidad</td>
      <td>Como administrador, quiero gestionar todas las reservas y disponibilidad en tiempo real para evitar overbooking y optimizar la ocupación física.</td>
      <td>Dado que se procesa una nueva reserva o modificación, cuando el servicio valida las fechas y la habitación, entonces el inventario se actualiza de forma atómica y consistente, emitiendo un evento al bus de mensajería para notificar a los demás contextos.</td>
      <td>EP-02</td>
    </tr>
    <tr>
      <td><strong>US-08</strong></td>
      <td>Check-in digital automatizado con entrega de credencial digital</td>
      <td>Como huésped, quiero realizar mi check-in digitalmente desde mi móvil para acceder de inmediato a la habitación sin pasar por recepción física.</td>
      <td>Dado que el huésped valida su identidad y pago previo, cuando confirma su check-in en la app, entonces el sistema cambia el estado de la habitación a ocupada, notifica a housekeeping y genera las credenciales de acceso digital/IoT en menos de 3 minutos.</td>
      <td>EP-02</td>
    </tr>
    <tr>
      <td><strong>US-11</strong></td>
      <td>Control ambiental y domótico IoT de habitación</td>
      <td>Como huésped, quiero controlar la climatización e iluminación de mi habitación desde la aplicación móvil para personalizar mi estancia.</td>
      <td>Dado que el huésped autenticado ajusta la temperatura o iluminación desde la app, cuando envía el comando, entonces el backend valida la sesión activa y publica la orden al broker/gateway IoT hacia los microcontroladores/actuadores en menos de 5 segundos.</td>
      <td>EP-05</td>
    </tr>
    <tr>
      <td><strong>US-23</strong></td>
      <td>Procesamiento transaccional de pagos digitales</td>
      <td>Como huésped y administrador, quiero procesar cobros y autorizaciones de manera segura con pasarelas externas para asegurar transacciones financieras fluidas.</td>
      <td>Dado que se solicita el pago de una estancia o servicio adicional, cuando se transfieren los datos mediante comunicación cifrada, entonces el sistema procesa la transacción con el proveedor externo, aplicando máscaras PCI-DSS y registrando el comprobante sin bloquear el hilo principal.</td>
      <td>EP-03</td>
    </tr>
    <tr>
      <td><strong>US-35</strong></td>
      <td>Despacho reactivo de notificaciones al personal</td>
      <td>Como miembro del staff operativo, quiero recibir alertas automáticas inmediatas sobre habitaciones liberadas o incidencias para atenderlas con prontitud.</td>
      <td>Dado que se emite un evento de check-out o falla de mantenimiento, cuando el motor de eventos procesa la regla de negocio, entonces se envía una notificación push al dispositivo móvil del personal asignado de manera instantánea.</td>
      <td>EP-07</td>
    </tr>
  </tbody>
</table>

#### 4.1.2.2. Quality Attribute Scenarios
Los siguientes escenarios formalizan los requisitos no funcionales prioritarios para el ecosistema distribuido de SmartStay, siguiendo la estructura estándar de 6 partes del Software Engineering Institute (SEI).

<table>
  <thead>
    <tr>
      <th>Atributo</th>
      <th>Fuente</th>
      <th>Estímulo</th>
      <th>Artefacto</th>
      <th>Entorno</th>
      <th>Respuesta</th>
      <th>Medida</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Fiabilidad / Resiliencia</strong></td>
      <td>Falla de red o caída de servicio externo (OTA / Pasarela de Pagos)</td>
      <td>Petición de sincronización o pago queda sin respuesta o timeout prolongado</td>
      <td>Microservicio de Integración / Billing / API Gateway</td>
      <td>Operación normal en producción</td>
      <td>El sistema activa el patrón Circuit Breaker, aísla la falla, almacena el evento en colas de reintento y responde con degradación elegante sin propagar errores en cascada.</td>
      <td>Tiempo de apertura de circuito &lt; 100 ms; cero pérdida de consistencia transaccional.</td>
    </tr>
    <tr>
      <td><strong>Eficiencia / Rendimiento</strong></td>
      <td>Carga concurrente de huéspedes y staff</td>
      <td>Peticiones concurrentes masivas de consulta de disponibilidad, telemetría IoT y check-ins durante hora punta</td>
      <td>API Gateway, Caché distribuida (Redis) y Microservicios Core</td>
      <td>Picos de alta demanda (hasta 500 req/s concurrentes)</td>
      <td>El API Gateway balancea el tráfico, sirviendo lecturas frecuentes desde la capa de caché y procesando eventos asíncronos.</td>
      <td>Tiempo de respuesta promedio ≤ 1.5 segundos por petición HTTP; latencia de telemetría IoT &lt; 500 ms.</td>
    </tr>
    <tr>
      <td><strong>Seguridad</strong></td>
      <td>Actor no autenticado o solicitud manipulada</td>
      <td>Intento de inyección, escalada de privilegios o acceso no autorizado a actuadores IoT y datos de huéspedes</td>
      <td>Módulo IAM / API Gateway</td>
      <td>Operación continua bajo exposición pública</td>
      <td>Valida estrictamente tokens JWT firmados criptográficamente y restringe el acceso según el modelo RBAC, rechazando y auditando la petición.</td>
      <td>100% de peticiones no autorizadas rechazadas (HTTP 401/403) con registro en bitácora de auditoría.</td>
    </tr>
    <tr>
      <td><strong>Mantenibilidad / Evolución</strong></td>
      <td>Equipo de ingeniería</td>
      <td>Requerimiento de incorporar una nueva integración tecnológica (ej. red de sensores IoT o conector Web3)</td>
      <td>Arquitectura de Bounded Contexts y Contratos OpenAPI</td>
      <td>Entorno de integración y despliegue continuo (CI/CD)</td>
      <td>La separación de dominios (DDD) permite desarrollar, probar y desplegar el nuevo componente sin modificar ni detener los microservicios existentes.</td>
      <td>Tiempo de incorporación y despliegue del nuevo servicio &lt; 30 minutos sin tiempo de inactividad global (zero-downtime).</td>
    </tr>
    <tr>
      <td><strong>Disponibilidad</strong></td>
      <td>Caída repentina de una instancia de servicio o nodo de datos</td>
      <td>Falla crítica del contenedor de ejecución en nube</td>
      <td>Orquestador de Contenedores y Load Balancer (Cloud Native / PaaS)</td>
      <td>Operación continua 24/7</td>
      <td>El balanceador redirige el tráfico hacia instancias réplica saludables mediante Health Checks automáticos y activa el failover.</td>
      <td>Recuperación del servicio y reencaminamiento del tráfico en menos de 10 segundos.</td>
    </tr>
  </tbody>
</table>

#### 4.1.2.3. Constraints
Se definen las restricciones de diseño innegociables impuestas por el negocio, el entorno académico y el ecosistema tecnológico de despliegue.

<table>
  <thead>
    <tr>
      <th>Technical Story ID</th>
      <th>Título</th>
      <th>Descripción</th>
      <th>Criterios de Aceptación</th>
      <th>Relacionado con (Epic ID)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>TS-01</strong></td>
      <td>Arquitectura orientada a dominios y desacoplamiento</td>
      <td>La solución debe estructurarse obligatoriamente bajo los principios de Domain-Driven Design (DDD), garantizando la separación lógica y técnica en Bounded Contexts (IAM, Bookings, Accommodations, Payments, IoT).</td>
      <td>Dado el diseño del backend, cuando se implementa la solución, entonces cada contexto delimita sus entidades, repositorios y reglas sin compartir esquemas de datos directos con otros módulos.</td>
      <td>EP-02, EP-04</td>
    </tr>
    <tr>
      <td><strong>TS-02</strong></td>
      <td>Estrategia de despliegue Cloud Native y contenedorización</td>
      <td>Todos los servicios de backend, APIs y bases de datos deben empaquetarse en contenedores Docker y desplegarse sobre plataformas Cloud/PaaS garantizando disponibilidad 24/7.</td>
      <td>Dado el código fuente en la rama principal, cuando se ejecuta el pipeline de CI/CD, entonces se compila y publica una imagen de contenedor operable y accesible vía HTTPS.</td>
      <td>EP-02, EP-06</td>
    </tr>
    <tr>
      <td><strong>TS-03</strong></td>
      <td>Ecosistema multicomponente con cliente móvil y web</td>
      <td>La solución debe proveer interacción consistente a través de una Landing Page (HTML5/JS), una aplicación web administrativa y una aplicación móvil para el huésped/staff.</td>
      <td>Dado el catálogo de servicios RESTful, cuando los clientes Web y Móvil consumen los endpoints, entonces la experiencia de usuario y la lógica de negocio se mantienen sincronizadas y conformes a los lineamientos de diseño.</td>
      <td>EP-01, EP-05</td>
    </tr>
    <tr>
      <td><strong>TS-04</strong></td>
      <td>Estandarización de contratos de API mediante OpenAPI (OAS 3.0)</td>
      <td>Todos los servicios expuestos internamente o hacia clientes deben adoptar el enfoque API-First y estar completamente documentados bajo el estándar OpenAPI 3.0 mediante Swagger UI.</td>
      <td>Dado cualquier endpoint desplegado, cuando se consulta /swagger, entonces se exponen con exactitud los esquemas tipados de Request/Response, parámetros de ruta y esquemas de autenticación Bearer JWT.</td>
      <td>EP-03, EP-04</td>
    </tr>
    <tr>
      <td><strong>TS-05</strong></td>
      <td>Integración y emulación de tecnologías IoT / Mensajería Asíncrona</td>
      <td>La arquitectura debe contemplar la recepción de telemetría y emisión de comandos domóticos hacia actuadores y sensores mediante brokers de eventos / mensajería (ActiveMQ/MQTT) o emuladores de hardware.</td>
      <td>Dado un cambio en el estado del sensor ambiental de una habitación, cuando se emite la telemetría, entonces el backend procesa el evento y sincroniza el estado en el módulo analítico y de control.</td>
      <td>EP-05, EP-06</td>
    </tr>
  </tbody>
</table>

---

### 4.1.3. Architectural Drivers Backlog
El Architectural Drivers Backlog de SmartStay consolida los requerimientos funcionales críticos, escenarios de calidad y restricciones tecnológicas, priorizados según su valor de negocio y su complejidad arquitectónica técnica.

<table>
  <thead>
    <tr>
      <th>Driver ID</th>
      <th>Título de Driver</th>
      <th>Descripción</th>
      <th>Importancia para Stakeholders</th>
      <th>Impacto en Architecture Technical Complexity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>FD-01</strong></td>
      <td>Gestión centralizada de reservas y disponibilidad</td>
      <td>SmartStay debe gestionar reservas y disponibilidad de habitaciones de manera centralizada, validando la disponibilidad y actualizando el inventario de forma atómica para evitar overbooking y mantener consistencia entre los componentes involucrados.</td>
      <td>High</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>FD-02</strong></td>
      <td>Check-in digital y acceso automatizado</td>
      <td>El sistema debe permitir que el huésped realice el check-in digital desde su dispositivo móvil y, después de validar identidad y pago, actualice el estado de la habitación, notifique al staff y genere las credenciales de acceso digital.</td>
      <td>High</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>FD-03</strong></td>
      <td>Control ambiental IoT de la habitación</td>
      <td>SmartStay debe permitir controlar temperatura e iluminación desde la aplicación móvil, validando la sesión del huésped y enviando los comandos mediante el backend hacia el broker o gateway IoT y los actuadores correspondientes.</td>
      <td>High</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>FD-04</strong></td>
      <td>Procesamiento transaccional de pagos</td>
      <td>El sistema debe procesar pagos y autorizaciones mediante pasarelas externas, utilizando comunicación cifrada, controles de seguridad y mecanismos que eviten bloquear los procesos principales de la aplicación.</td>
      <td>High</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>FD-05</strong></td>
      <td>Despacho reactivo de notificaciones</td>
      <td>La solución debe procesar eventos operativos, como check-out o incidencias de mantenimiento, y generar notificaciones automáticas al personal asignado para facilitar una respuesta oportuna.</td>
      <td>High</td>
      <td>Medium</td>
    </tr>
    <tr>
      <td><strong>QA-01</strong></td>
      <td>Seguridad y control de acceso</td>
      <td>SmartStay debe proteger los datos y funcionalidades mediante autenticación, autorización basada en roles y validación de tokens, rechazando y auditando solicitudes no autorizadas y protegiendo también el acceso a actuadores IoT.</td>
      <td>High</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>QA-02</strong></td>
      <td>Fiabilidad y resiliencia</td>
      <td>El sistema debe aislar fallos de red o de servicios externos mediante Circuit Breaker, colas de reintento y mecanismos de degradación controlada, evitando errores en cascada y preservando la consistencia transaccional.</td>
      <td>High</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>QA-03</strong></td>
      <td>Rendimiento y procesamiento en tiempo real</td>
      <td>La arquitectura debe soportar cargas concurrentes de huéspedes y staff, consultas de disponibilidad, check-ins y telemetría IoT manteniendo los tiempos de respuesta definidos por los escenarios de calidad.</td>
      <td>High</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>QA-04</strong></td>
      <td>Disponibilidad continua</td>
      <td>SmartStay debe operar de manera continua y recuperarse ante fallos de instancias o nodos utilizando réplicas saludables, health checks, balanceo de carga y mecanismos automáticos de failover.</td>
      <td>High</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>QA-05</strong></td>
      <td>Mantenibilidad y evolución</td>
      <td>La arquitectura debe permitir incorporar nuevas integraciones tecnológicas, como nuevos sensores IoT o conectores externos, sin modificar ni detener los microservicios existentes y manteniendo una evolución controlada.</td>
      <td>Medium</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>C-01</strong></td>
      <td>Domain-Driven Design y Bounded Contexts</td>
      <td>La solución debe estructurarse bajo principios de DDD, separando los contextos IAM, Bookings, Accommodations, Payments e IoT, con límites claros para entidades, repositorios y reglas y sin compartir esquemas de datos directamente.</td>
      <td>High</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>C-02</strong></td>
      <td>Cloud Native y contenedorización</td>
      <td>Los servicios backend, APIs y componentes correspondientes deben empaquetarse en contenedores Docker y desplegarse en una plataforma Cloud/PaaS, manteniendo el servicio disponible y accesible mediante HTTPS.</td>
      <td>High</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>C-03</strong></td>
      <td>Ecosistema móvil y web</td>
      <td>SmartStay debe mantener una interacción consistente entre la Landing Page, la aplicación web administrativa y las aplicaciones móviles para huésped y staff, utilizando los servicios RESTful como mecanismo de integración.</td>
      <td>High</td>
      <td>Medium</td>
    </tr>
    <tr>
      <td><strong>C-04</strong></td>
      <td>Contratos API estandarizados con OpenAPI 3.0</td>
      <td>Los servicios expuestos deben adoptar un enfoque API-First y estar documentados mediante OpenAPI 3.0 y Swagger UI, incluyendo esquemas de request/response, parámetros y autenticación Bearer JWT.</td>
      <td>Medium</td>
      <td>High</td>
    </tr>
    <tr>
      <td><strong>C-05</strong></td>
      <td>Integración IoT y mensajería asíncrona</td>
      <td>La arquitectura debe contemplar la recepción de telemetría y la emisión de comandos hacia sensores y actuadores mediante brokers de eventos/mensajería, como ActiveMQ o MQTT, o mediante emuladores de hardware.</td>
      <td>High</td>
      <td>High</td>
    </tr>
  </tbody>
</table>

---

### 4.1.4. Architectural Design Decisions
Para dar respuesta a los Architectural Drivers, se evaluaron tácticas y patrones arquitectónicos específicos para cada requerimiento clave, analizando ventajas (*Pro*) y desventajas (*Con*).

<table>
  <thead>
    <tr>
      <th>Driver ID</th>
      <th>Driver Asociado</th>
      <th>Táctica / Patrón 1 (Seleccionado)</th>
      <th>Pro 1 / Con 1</th>
      <th>Táctica / Patrón 2 (Alternativa)</th>
      <th>Pro 2 / Con 2</th>
      <th>Táctica / Patrón 3 (Complemento)</th>
      <th>Pro 3 / Con 3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>AD-01</strong></td>
      <td>Fiabilidad / Resiliencia (QA-02)</td>
      <td><strong>Circuit Breaker</strong></td>
      <td><strong>Pro:</strong> Aísla fallos de servicios externos y evita caídas en cascada.<br><strong>Con:</strong> Requiere configurar umbrales de apertura y fallback precisos.</td>
      <td><strong>Retry + Dead Letter Queue</strong></td>
      <td><strong>Pro:</strong> Reintenta transacciones transitorias y audita fallos irrecuperables.<br><strong>Con:</strong> Puede saturar endpoints si el fallo no es transitorio.</td>
      <td><strong>Bulkhead</strong></td>
      <td><strong>Pro:</strong> Aísla pools de hilos/recursos por servicio crítico.<br><strong>Con:</strong> Aumenta la complejidad en la parametrización de memoria/hilos.</td>
    </tr>
    <tr>
      <td><strong>AD-02</strong></td>
      <td>Eficiencia / Rendimiento (QA-03)</td>
      <td><strong>Distributed Cache (Redis)</strong></td>
      <td><strong>Pro:</strong> Reduce latencia en consultas repetitivas de disponibilidad de habitaciones.<br><strong>Con:</strong> Exige políticas estrictas de invalidación de caché.</td>
      <td><strong>API Gateway Throttling</strong></td>
      <td><strong>Pro:</strong> Controla y protege la infraestructura ante picos repentinos de tráfico.<br><strong>Con:</strong> Puede rechazar solicitudes legítimas bajo mala calibración.</td>
      <td><strong>Event-Driven Broker (MQTT/AMQP)</strong></td>
      <td><strong>Pro:</strong> Desacopla la ingesta masiva de telemetría IoT del hilo HTTP.<br><strong>Con:</strong> Requiere monitoreo continuo de lag en colas de eventos.</td>
    </tr>
    <tr>
      <td><strong>AD-03</strong></td>
      <td>Seguridad (QA-01)</td>
      <td><strong>Stateless JWT Authentication</strong></td>
      <td><strong>Pro:</strong> Autenticación distribuida sin consultar una base de datos central en cada petición.<br><strong>Con:</strong> Complejidad en la invalidación inmediata de tokens emitidos.</td>
      <td><strong>Role-Based Access Control (RBAC)</strong></td>
      <td><strong>Pro:</strong> Restringe estrictamente acciones entre Huéspedes, Staff y Administradores.<br><strong>Con:</strong> Requiere mantenimiento continuo de matrices de permisos.</td>
      <td><strong>API Gateway Edge Validation</strong></td>
      <td><strong>Pro:</strong> Centraliza la validación criptográfica antes de ingresar a la red interna.<br><strong>Con:</strong> Punto único de fallo si no cuenta con alta redundancia.</td>
    </tr>
    <tr>
      <td><strong>AD-04</strong></td>
      <td>Mantenibilidad / Evolución (QA-05 / C-01)</td>
      <td><strong>DDD Bounded Contexts</strong></td>
      <td><strong>Pro:</strong> Aislamiento de modelos, reglas de negocio y esquemas de persistencia.<br><strong>Con:</strong> Demanda alto rigor técnico y comunicación inter-contexto.</td>
      <td><strong>Hexagonal / Clean Architecture</strong></td>
      <td><strong>Pro:</strong> Independiza las entidades del framework, base de datos e interfaces.<br><strong>Con:</strong> Introduce mayor número de interfaces, mappers y capas.</td>
      <td><strong>API-First con OpenAPI 3.0</strong></td>
      <td><strong>Pro:</strong> Garantiza contratos formales y tipados entre frontend y backend.<br><strong>Con:</strong> Requiere sincronización disciplinada entre contrato y código.</td>
    </tr>
    <tr>
      <td><strong>AD-05</strong></td>
      <td>Disponibilidad (QA-04 / C-02)</td>
      <td><strong>Container Orchestration & Auto-failover</strong></td>
      <td><strong>Pro:</strong> Reinicio automático y sustitución de contenedores degradados en segundos.<br><strong>Con:</strong> Dependencia operativa de la infraestructura del proveedor Cloud.</td>
      <td><strong>Automated Health Checks</strong></td>
      <td><strong>Pro:</strong> Detección temprana de nodos enfermos antes de recibir tráfico de usuarios.<br><strong>Con:</strong> Consumo continuo de peticiones de sonda internas.</td>
      <td><strong>Multi-instance Load Balancing</strong></td>
      <td><strong>Pro:</strong> Distribuye el tráfico homogéneamente eliminando puntos únicos de falla.<br><strong>Con:</strong> Costos de infraestructura adicionales por replicación.</td>
    </tr>
  </tbody>
</table>

---

### 4.1.5. Quality Attribute Scenario Refinements

##### Scenario Refinement 1: Fiabilidad / Resiliencia
<table>
  <tbody>
    <tr><td><strong>Scenario(s)</strong></td><td>Ante una falla de red o la indisponibilidad temporal de un servicio externo (OTA o pasarela de pagos), una solicitud de sincronización o procesamiento no recibe respuesta dentro del tiempo esperado.</td></tr>
    <tr><td><strong>Business Goals</strong></td><td>Garantizar la continuidad de las operaciones hoteleras y evitar que la indisponibilidad de un servicio externo provoque interrupciones en cadena, pérdida de información o inconsistencias en las transacciones.</td></tr>
    <tr><td><strong>Relevant Quality Attributes</strong></td><td>Fiabilidad, resiliencia, disponibilidad y consistencia transaccional.</td></tr>
    <tr><td><strong>Stimulus</strong></td><td>Una petición de sincronización con una OTA o una operación de pago permanece sin respuesta o alcanza un timeout prolongado.</td></tr>
    <tr><td><strong>Stimulus Source</strong></td><td>Servicio externo de integración, OTA o pasarela de pagos.</td></tr>
    <tr><td><strong>Environment</strong></td><td>Operación normal del sistema SmartStay en producción, con usuarios y servicios activos.</td></tr>
    <tr><td><strong>Artifact</strong></td><td>Microservicio de Integración, Billing y API Gateway.</td></tr>
    <tr><td><strong>Response</strong></td><td>El sistema activa el Circuit Breaker para aislar el servicio, encola la transacción para reintento asíncrono y devuelve una respuesta de degradación controlada al cliente.</td></tr>
    <tr><td><strong>Response Measure</strong></td><td>Apertura del circuito en &lt; 100 ms; 0% de pérdida de consistencia transaccional.</td></tr>
    <tr><td><strong>Questions</strong></td><td>¿Cuál es el umbral de reintentos antes de derivar a Dead Letter Queue? ¿Cómo se notifica al usuario si la pasarela no se restablece?</td></tr>
    <tr><td><strong>Issues</strong></td><td>Riesgo de operaciones duplicadas si el timeout ocurrió tras haberse procesado el débito en la pasarela externa.</td></tr>
  </tbody>
</table>

##### Scenario Refinement 2: Eficiencia / Rendimiento
<table>
  <tbody>
    <tr><td><strong>Scenario(s)</strong></td><td>Durante la hora punta de check-ins y consultas de disponibilidad, cientos de usuarios y dispositivos IoT saturan la plataforma simultáneamente.</td></tr>
    <tr><td><strong>Business Goals</strong></td><td>Mantener una experiencia de usuario ágil y sin demoras en la interacción domótica ni en la reserva de habitaciones.</td></tr>
    <tr><td><strong>Relevant Quality Attributes</strong></td><td>Rendimiento, escalabilidad, latencia y concurrencia.</td></tr>
    <tr><td><strong>Stimulus</strong></td><td>Tráfico masivo concurrente que alcanza las 500 peticiones HTTP/s y ráfagas continuas de telemetría IoT.</td></tr>
    <tr><td><strong>Stimulus Source</strong></td><td>Huéspedes móviles, administradores web y microcontroladores IoT de habitaciones.</td></tr>
    <tr><td><strong>Environment</strong></td><td>Entorno de producción durante picos estacionales o eventos hoteleros de alta demanda.</td></tr>
    <tr><td><strong>Artifact</strong></td><td>API Gateway, Clúster de Redis Caché y Microservicios de Alojamiento y Reservas.</td></tr>
    <tr><td><strong>Response</strong></td><td>El Gateway despacha lecturas desde la caché distribuida, mientras que la telemetría IoT es ingerida por colas de mensajería desacopladas.</td></tr>
    <tr><td><strong>Response Measure</strong></td><td>Tiempo de respuesta HTTP ≤ 1.5 s; latencia de procesamiento y comando IoT &lt; 500 ms.</td></tr>
    <tr><td><strong>Questions</strong></td><td>¿Qué estrategia de invalidación de caché (TTL vs. Event-driven invalidation) se usará para evitar sobreventa?</td></tr>
    <tr><td><strong>Issues</strong></td><td>Consumo de memoria RAM en el clúster de caché bajo retención prolongada de llaves de búsqueda.</td></tr>
  </tbody>
</table>

##### Scenario Refinement 3: Seguridad
<table>
  <tbody>
    <tr><td><strong>Scenario(s)</strong></td><td>Un atacante externo intenta forzar el acceso a actuadores de apertura de puertas de habitaciones o extraer datos sensibles de tarjetas de huéspedes.</td></tr>
    <tr><td><strong>Business Goals</strong></td><td>Proteger la integridad física de los huéspedes, resguardar información confidencial y cumplir con las normativas de protección de datos personales y PCI-DSS.</td></tr>
    <tr><td><strong>Relevant Quality Attributes</strong></td><td>Confidencialidad, integridad, autenticación, autorización y no repudio.</td></tr>
    <tr><td><strong>Stimulus</strong></td><td>Peticiones con inyección de código, suplantación de identidad o tokens JWT manipulados/expirados.</td></tr>
    <tr><td><strong>Stimulus Source</strong></td><td>Actor malicioso externo o usuario interno con privilegios insuficientes.</td></tr>
    <tr><td><strong>Environment</strong></td><td>Operación continua del sistema expuesto a Internet mediante endpoints públicos.</td></tr>
    <tr><td><strong>Artifact</strong></td><td>API Gateway, Módulo IAM y Middleware de autorización RBAC.</td></tr>
    <tr><td><strong>Response</strong></td><td>Validación criptográfica de firma de token; rechazo inmediato de peticiones no autorizadas y registro del evento con IP en logs de auditoría.</td></tr>
    <tr><td><strong>Response Measure</strong></td><td>100% de solicitudes ilegítimas bloqueadas con código HTTP 401/403 en menos de 50 ms.</td></tr>
    <tr><td><strong>Questions</strong></td><td>¿Cómo se gestiona el ciclo de vida de la rotación de claves criptográficas de los actuadores IoT?</td></tr>
    <tr><td><strong>Issues</strong></td><td>Ataques de denegación de servicio distribuidos (DDoS) intentando saturar la capa de validación criptográfica.</td></tr>
  </tbody>
</table>

##### Scenario Refinement 4: Mantenibilidad / Evolución
<table>
  <tbody>
    <tr><td><strong>Scenario(s)</strong></td><td>El equipo de desarrollo necesita integrar un nuevo fabricante de cerraduras inteligentes IoT sin interrumpir el servicio de reservas ni el check-in actual.</td></tr>
    <tr><td><strong>Business Goals</strong></td><td>Evolucionar la oferta tecnológica del hotel rápidamente sin generar tiempo de inactividad operativa ni costos elevados de refactorización.</td></tr>
    <tr><td><strong>Relevant Quality Attributes</strong></td><td>Modificabilidad, desacoplamiento, extensibilidad y desplegabilidad.</td></tr>
    <tr><td><strong>Stimulus</strong></td><td>Requerimiento de nueva integración con APIs de un fabricante externo de hardware.</td></tr>
    <tr><td><strong>Stimulus Source</strong></td><td>Evolución del negocio y equipo de ingeniería.</td></tr>
    <tr><td><strong>Environment</strong></td><td>Pipeline automatizado de CI/CD hacia entorno de producción.</td></tr>
    <tr><td><strong>Artifact</strong></td><td>Bounded Context de IoT Stay & Experience, Contratos OpenAPI e interfaces del Adaptador de Hardware.</td></tr>
    <tr><td><strong>Response</strong></td><td>Implementación de un nuevo adaptador según el patrón de Puertos y Adaptadores (Hexagonal) sin modificar el núcleo de dominio de reservas.</td></tr>
    <tr><td><strong>Response Measure</strong></td><td>Despliegue del nuevo adaptador en &lt; 30 minutos sin tiempo de inactividad global (Zero-downtime).</td></tr>
    <tr><td><strong>Questions</strong></td><td>¿Qué versiones de contratos API se deben mantener activas simultáneamente en el Gateway?</td></tr>
    <tr><td><strong>Issues</strong></td><td>Riesgo de rotura de compatibilidad hacia atrás si los contratos OpenAPI no aplican versionamiento semántico estricto.</td></tr>
  </tbody>
</table>

##### Scenario Refinement 5: Disponibilidad
<table>
  <tbody>
    <tr><td><strong>Scenario(s)</strong></td><td>Una instancia crítica del backend o el nodo del contenedor donde se aloja el servicio de reservas sufre una falla de memoria y colapsa inesperadamente.</td></tr>
    <tr><td><strong>Business Goals</strong></td><td>Asegurar la continuidad del negocio hotelero 24/7, garantizando que huéspedes y staff puedan continuar operando sin interrupciones perceptibles.</td></tr>
    <tr><td><strong>Relevant Quality Attributes</strong></td><td>Disponibilidad, tolerancia a fallos y tiempo de recuperación (*MTTR*).</td></tr>
    <tr><td><strong>Stimulus</strong></td><td>Caída súbita del contenedor de ejecución o fallo de conectividad interna del nodo.</td></tr>
    <tr><td><strong>Stimulus Source</strong></td><td>Falla de infraestructura en la plataforma en la nube.</td></tr>
    <tr><td><strong>Environment</strong></td><td>Entorno de producción bajo tráfico habitual de operaciones hoteleras.</td></tr>
    <tr><td><strong>Artifact</strong></td><td>Orquestador de Contenedores, Balanceador de Carga y Sondas de Health Check.</td></tr>
    <tr><td><strong>Response</strong></td><td>El balanceador detecta la pérdida del heartbeat mediante el health check, retira el nodo insalubre del enrutamiento y aprovisiona/promueve un nodo réplica en caliente.</td></tr>
    <tr><td><strong>Response Measure</strong></td><td>Reencaminamiento del tráfico hacia instancias saludables en menos de 10 segundos, sin errores visibles 5xx al usuario final.</td></tr>
    <tr><td><strong>Questions</strong></td><td>¿Existe persistencia externa que permita a las nuevas réplicas levantarse de forma totalmente *stateless*?</td></tr>
    <tr><td><strong>Issues</strong></td><td>Sincronización de sesiones de usuario si existiera estado local no externalizado en Redis.</td></tr>
  </tbody>
</table>

---

## 4.2. Strategic-Level Domain-Driven Design

### 4.2.1. EventStorming
Para modelar el comportamiento del sistema y descubrir los límites del dominio, el equipo condujo un taller colaborativo de **EventStorming**. Mediante un enfoque iterativo estructurado en 10 pasos, se plasmaron los eventos de negocio, comandos, políticas, modelos de lectura y agrupaciones lógicas.


[DIAGRAMA: Tablero General de EventStorming de SmartStay]
Ubicación del artefacto: Tablero colaborativo Miro/Mural (Link: [https://tinyurl.com/8529395x](https://tinyurl.com/8529395x?utm_source=gemini))
Descripción visual: Muro horizontal secuencial con código de colores normalizado que contiene:

* Naranja: Domain Events (verbos en pasado participio).
* Azul: Commands (acciones disparadas por actores).
* Amarillo: Agregados / Entidades del dominio.
* Lila/Rosa: Políticas de negocio (Whenever... Then...).
* Verde: Read Models (vistas y proyecciones de datos).
* Rosa/Rojo: Pain Points (fricciones operativas identificadas).
* Rosa Claro: External Systems (Pasarelas de Pago, Brokers IoT, OTAs).


* **Step 1: Unstructured Exploration:** Los participantes propusieron eventos de negocio en notas naranjas escritas en tiempo pasado, capturando todo lo que sucede en el ciclo hotelero sin preocuparse por el orden inicial (ej. `RoomReserved`, `PaymentAccepted`, `DoorUnlocked`, `RoomCleaned`).
* **Step 2: Timelines:** Se ordenaron cronológicamente los eventos de izquierda a derecha, estableciendo ramas divergentes para flujos concurrentes (flujo del huésped vs. flujo de operaciones del personal).
* **Step 3: Pain Points:** Se identificaron fricciones críticas (en color rojo): overbooking manual, demoras de recepción, falta de verificación del estado de limpieza antes del acceso y llaves físicas extraviadas.
* **Step 4: Pivotal Events:** Se marcaron los eventos de inflexión que delimitan fases del negocio: `UserRegistered`, `HotelConfigured`, `ReservationConfirmed`, `DigitalCheckInCompleted`, `RoomAccessGranted`, `MaintenanceTaskFinished`.
* **Step 5: Commands:** Se ubicaron notas azules previas a los eventos, representando las intenciones y órdenes directas ejecutadas por los usuarios (ej. `RegisterHotel`, `ConfirmBooking`, `UnlockDoor`, `ReportIncident`).
* **Step 6: Policies:** Se incorporaron notas lilas que formalizan reglas reactivas automáticas: *Whenever `DigitalCheckInCompleted` Then `GenerateDigitalKey`*, *Whenever `CheckOutCompleted` Then `CreateCleaningTask`*.
* **Step 7: Read Models:** Se asociaron pantallas y proyecciones verdes que los usuarios consultan para tomar decisiones antes de disparar un comando (ej. `AvailableRoomsView`, `AssignedTasksDashboard`).
* **Step 8: External Systems:** Se incorporaron sistemas externos en notas rectangulares: Pasarela de Pago (Stripe/Culqi), Proveedor de Mensajería Push (Firebase) y Broker MQTT de Dispositivos IoT.
* **Step 9: Aggregates:** Se identificaron las fronteras de consistencia transaccional (notas amarillas) que encapsulan entidades y reglas: `Booking`, `Room`, `GuestProfile`, `SmartLock`, `OperationalTask`.
* **Step 10: Bounded Contexts:** Se trazaron fronteras delimitadas finales sobre los agregados, identificando los 7 Bounded Contexts que conforman la solución SmartStay.

---

### 4.2.2. Candidate Context Discovery
Aplicando la técnica *Look-for-pivotal-events*, se identificaron las fronteras naturales donde el lenguaje ubicuo cambia de significado y donde ocurren transiciones transaccionales determinantes.


[DIAGRAMA: Candidate Context Discovery Map]
Descripción visual: Diagrama conceptual que agrupa los Pivotal Events identificados a lo largo de la línea temporal del negocio hotelero dentro de cápsulas funcionales preliminares, evidenciando las transiciones de responsabilidad.

* **Fase de Identificación de Pivotal Events:**
  1. `User Mode Selected` / `Identity Verified`: Transición de navegación anónima a contexto de seguridad.
  2. `Hotel Setup Completed`: Transición de configuración a operatividad de planta física.
  3. `Reservation Confirmed & Paid`: Transición del proceso comercial a la espera de estancia.
  4. `Digital Check-in Completed`: Habilitación del entorno domótico y operacional para el huésped.
  5. `Task Closed & Inspected`: Cierre del ciclo operativo interno.

<table>
  <thead>
    <tr>
      <th>Bounded Context</th>
      <th>Descripción de Responsabilidad</th>
      <th>Eventos Clave Asociados</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>IAM (Identity & Access Management)</strong></td>
      <td>Gestiona la seguridad, emisión de credenciales, autenticación y autorización transversal para todos los roles (Admin, Staff, Huésped).</td>
      <td>UserRegistered, AuthenticationSucceeded, AccessRevoked, TokenRefreshed.</td>
    </tr>
    <tr>
      <td><strong>Profiles</strong></td>
      <td>Administra la información de identidad extendida, datos personales, preferencias de los huéspedes y legajos del personal.</td>
      <td>ProfileCreated, PersonalDataUpdated, GuestPreferencesRecorded.</td>
    </tr>
    <tr>
      <td><strong>Properties Management</strong></td>
      <td>Encargado del catálogo físico del hotel: configuración de propiedades, plantas, tipología de habitaciones, comodidades y tarifas.</td>
      <td>HotelCreated, RoomAdded, RoomStatusChanged, RoomAmenityConfigured.</td>
    </tr>
    <tr>
      <td><strong>Bookings & Payments</strong></td>
      <td>Controla el ciclo comercial de reservas, cálculo de tarifas, procesamiento de pagos con pasarelas externas y balance financiero.</td>
      <td>ReservationCreated, PaymentCaptured, BookingConfirmed, BookingCancelled.</td>
    </tr>
    <tr>
      <td><strong>Operational Tasks</strong></td>
      <td>Coordina las operaciones internas del hotel: órdenes de limpieza (*housekeeping*), mantenimiento técnico y resolución de incidencias.</td>
      <td>CleaningTaskGenerated, MaintenanceTaskAssigned, IncidentReported, TaskCompleted.</td>
    </tr>
    <tr>
      <td><strong>IoT Stay & Experience</strong></td>
      <td>Núcleo de la experiencia del huésped: habilitación de credenciales digitales y comunicación bidireccional con cerraduras y sensores de la habitación.</td>
      <td>DigitalKeyIssued, DigitalKeyRevoked, RoomTemperatureSet, LightingModeChanged.</td>
    </tr>
    <tr>
      <td><strong>Analytics</strong></td>
      <td>Agrega eventos transaccionales para generar métricas de ocupación, ingresos (*RevPAR*), eficiencia del staff y satisfacción del cliente.</td>
      <td>OccupancyMetricCalculated, StaffEfficiencyLogged, FinancialReportGenerated.</td>
    </tr>
  </tbody>
</table>

---

### 4.2.3. Domain Message Flows Modeling
El modelado de flujos de mensajes del dominio representa la coreografía y orquestación de comandos, eventos y consultas entre los diferentes Bounded Contexts.


[DIAGRAMA: Domain Message Flow - Flujo Transaccional de Reserva y Pago]
Descripción visual: Diagrama de secuencia de mensajes de dominio que muestra al Huésped enviando el comando CreateBooking a Bookings & Payments, la validación de inventario con Properties Management, la invocación de la Pasarela Externa de Pagos, la persistencia del agregado y la publicación del evento de dominio BookingConfirmed al Message Bus.

[DIAGRAMA: Domain Message Flow - Check-in Digital y Activación IoT]
Descripción visual: Diagrama que modela la interacción reactiva iniciada por el comando ExecuteDigitalCheckIn. Bookings & Payments emite DigitalCheckInCompleted, el cual es consumido por IoT Stay & Experience para invocar GenerateDigitalKey y por Operational Tasks para emitir alertas al staff.



#### Detalle de los Flujos de Mensajes Principales:
1. **Flujo de Reserva y Pago:**
   * El cliente ejecuta el comando `SubmitBooking(hotelId, roomId, dates, paymentMethod)`.
   * El contexto **Bookings & Payments** consulta el Read Model de disponibilidad de **Properties Management**.
   * Tras validar el inventario, solicita el cargo mediante la pasarela de pagos externa.
   * Al recibir la confirmación bancaria, el agregado `Booking` transiciona a estado `Confirmed` y emite el evento de dominio `BookingConfirmedEvent`.
   * **Properties Management** escucha dicho evento y bloquea definitivamente las fechas de la habitación mediante el comando interno `BlockRoomDates`.

2. **Flujo de Check-In Digital y Concesión de Acceso IoT:**
   * El huésped ejecuta `PerformDigitalCheckIn(bookingId, guestIdentityDoc)` desde la aplicación móvil.
   * **Bookings & Payments** valida la vigencia de la reserva y emite el evento `DigitalCheckInCompletedEvent`.
   * **IoT Stay & Experience** consume el evento, genera el token de acceso digital y despacha el comando `ActivateLockKey` hacia el broker MQTT que conecta con la cerradura electrónica de la habitación.
   * Paralelamente, **Operational Tasks** verifica que la habitación posea el estado `CleanedAndInspected`; de lo contrario, genera una alerta prioritaria de preparación.

3. **Flujo de Check-Out e Higienización:**
   * El huésped o el administrador dispara el comando `CompleteCheckOut(bookingId)`.
   * El contexto **Bookings & Payments** emite `CheckOutCompletedEvent`.
   * **IoT Stay & Experience** revoca la llave virtual asociada de forma inmediata (`RevokeDigitalKey`).
   * **Operational Tasks** intercepta el evento y ejecuta la política: *Whenever `CheckOutCompleted` Then `CreateHousekeepingTask`*, asignando automáticamente la limpieza de la habitación al personal de turno.

---

### 4.2.4. Bounded Context Canvases
A continuación se formalizan los Bounded Context Canvases para los dominios estructurales de la arquitectura SmartStay.

#### Canvas 1: Bookings & Payments Context
<table>
  <tbody>
    <tr><td colspan="2"><strong>Nombre del Contexto:</strong> Bookings & Payments</td></tr>
    <tr><td colspan="2"><strong>Propósito de Negocio:</strong> Gestionar el ciclo de vida de las reservas, garantizar la consistencia en la venta de habitaciones y procesar las liquidaciones económicas.</td></tr>
    <tr>
      <td style="width: 50%;"><strong>Inbound Messages (Comandos / Eventos Entrantes):</strong><br>
      • Command: <code>CreateReservation</code><br>
      • Command: <code>CancelReservation</code><br>
      • Command: <code>ProcessPayment</code><br>
      • Event: <code>RoomPricedCalculated</code> (desde Properties)</td>
      <td style="width: 50%;"><strong>Outbound Messages (Eventos Publicados):</strong><br>
      • Event: <code>BookingCreatedEvent</code><br>
      • Event: <code>BookingConfirmedEvent</code><br>
      • Event: <code>PaymentCapturedEvent</code><br>
      • Event: <code>DigitalCheckInCompletedEvent</code></td>
    </tr>
    <tr>
      <td><strong>Lenguaje Ubicuo:</strong><br>
      • <em>Folio:</em> Registro transaccional contable asociado a la estancia.<br>
      • <em>Overbooking:</em> Condición de sobreventa prevenida por concurrencia pesimista/optimista.<br>
      • <em>Rate Plan:</em> Esquema tarifario aplicable a la reserva.</td>
      <td><strong>Agregados y Entidades:</strong><br>
      • <strong>Aggregate Root:</strong> <code>Booking</code> (Entidades internas: <code>GuestSnapshot</code>, <code>StayPeriod</code>).<br>
      • <strong>Aggregate Root:</strong> <code>PaymentTransaction</code> (Value Objects: <code>Money</code>, <code>PaymentReceipt</code>).</td>
    </tr>
  </tbody>
</table>

<br>

#### Canvas 2: IoT Stay & Experience Context
<table>
  <tbody>
    <tr><td colspan="2"><strong>Nombre del Contexto:</strong> IoT Stay & Experience</td></tr>
    <tr><td colspan="2"><strong>Propósito de Negocio:</strong> Proveer autonomía de acceso al huésped y control del confort ambiental dentro de la habitación mediante dispositivos inteligentes.</td></tr>
    <tr>
      <td style="width: 50%;"><strong>Inbound Messages (Comandos / Eventos Entrantes):</strong><br>
      • Event: <code>DigitalCheckInCompletedEvent</code> (desde Bookings)<br>
      • Command: <code>UnlockDoorCommand</code><br>
      • Command: <code>UpdateClimateCommand</code><br>
      • Event: <code>TelemetryReceivedEvent</code> (desde MQTT Broker)</td>
      <td style="width: 50%;"><strong>Outbound Messages (Eventos Publicados):</strong><br>
      • Event: <code>DigitalKeyIssuedEvent</code><br>
      • Event: <code>DigitalKeyRevokedEvent</code><br>
      • Event: <code>RoomEnvironmentAdjustedEvent</code><br>
      • Event: <code>LockHardwareAnomalyDetectedEvent</code></td>
    </tr>
    <tr>
      <td><strong>Lenguaje Ubicuo:</strong><br>
      • <em>Virtual Key:</em> Credencial temporal cifrada para control de acceso físico.<br>
      • <em>Actuator:</em> Dispositivo electrónico que ejecuta cambios de estado físico.<br>
      • <em>Telemetry:</em> Muestreo continuo de sensores de temperatura, presencia y luz.</td>
      <td><strong>Agregados y Entidades:</strong><br>
      • <strong>Aggregate Root:</strong> <code>DigitalKey</code> (Value Objects: <code>PasscodeToken</code>, <code>KeyValidityPeriod</code>).<br>
      • <strong>Aggregate Root:</strong> <code>RoomEnvironmentController</code> (Entidades: <code>SensorNode</code>, <code>ActuatorNode</code>).</td>
    </tr>
  </tbody>
</table>

<br>

#### Canvas 3: Operational Tasks Context
<table>
  <tbody>
    <tr><td colspan="2"><strong>Nombre del Contexto:</strong> Operational Tasks</td></tr>
    <tr><td colspan="2"><strong>Propósito de Negocio:</strong> Orquestar y fiscalizar el trabajo del personal de campo (limpieza, mantenimiento e inspección de habitaciones).</td></tr>
    <tr>
      <td style="width: 50%;"><strong>Inbound Messages (Comandos / Eventos Entrantes):</strong><br>
      • Event: <code>CheckOutCompletedEvent</code> (desde Bookings)<br>
      • Command: <code>AssignTaskCommand</code><br>
      • Command: <code>ReportIncidentCommand</code><br>
      • Command: <code>CompleteTaskCommand</code></td>
      <td style="width: 50%;"><strong>Outbound Messages (Eventos Publicados):</strong><br>
      • Event: <code>CleaningTaskCompletedEvent</code><br>
      • Event: <code>RoomMarkedAsCleanEvent</code><br>
      • Event: <code>MaintenanceIncidentEscalatedEvent</code></td>
    </tr>
    <tr>
      <td><strong>Lenguaje Ubicuo:</strong><br>
      • <em>Housekeeping:</em> Protocolo de higienización y orden de habitaciones.<br>
      • <em>Incident Ticket:</em> Reporte de avería física de equipamiento en habitación.<br>
      • <em>Turnaround Time:</em> Tiempo transcurrido entre check-out y habitación lista.</td>
      <td><strong>Agregados y Entidades:</strong><br>
      • <strong>Aggregate Root:</strong> <code>OperationalTask</code> (Value Objects: <code>TaskType</code>, <code>Priority</code>, <code>TaskState</code>).<br>
      • <strong>Aggregate Root:</strong> <code>MaintenanceIncident</code> (Entidades: <code>IncidentLog</code>, <code>EvidenceAttachment</code>).</td>
    </tr>
  </tbody>
</table>

---

### 4.2.5. Context Mapping
El Context Mapping define las relaciones semánticas, técnicas y organizacionales entre los Bounded Contexts de SmartStay.




[DIAGRAMA: Context Map Estratégico de SmartStay]
Descripción visual: Mapa formal de Bounded Contexts que representa a los 7 dominios mediante elipses, explicitando las relaciones Upstream (U) / Downstream (D) y los patrones de integración utilizados:

* IAM (U) -> [ACL] -> Profiles (D)
* Profiles (U) -> [Conformist] -> Bookings & Payments (D)
* Properties Management (U) -> [Customer/Supplier] -> Bookings & Payments (D)
* Properties Management (U) -> [Customer/Supplier] -> Operational Tasks (D)
* Bookings & Payments (U) -> [Customer/Supplier] -> Operational Tasks (D)
* Bookings & Payments (U) -> [Customer/Supplier] -> IoT Stay & Experience (D)
* Bookings & Payments (U) -> [ACL] -> Analytics (D)

<table>
  <thead>
    <tr>
      <th>Relación de Contextos</th>
      <th>Upstream (U) / Downstream (D)</th>
      <th>Patrón DDD de Integración</th>
      <th>Justificación Técnica y de Dominio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>IAM → Profiles</strong></td>
      <td>IAM (U) / Profiles (D)</td>
      <td>Anti-Corruption Layer (ACL)</td>
      <td>IAM provee credenciales y tokens JWT de acceso. Profiles utiliza una capa ACL para traducir identidades a perfiles de usuario sin acoplar su modelo a los mecanismos de seguridad o esquemas del Identity Provider.</td>
    </tr>
    <tr>
      <td><strong>Profiles → Bookings & Payments</strong></td>
      <td>Profiles (U) / Bookings & Payments (D)</td>
      <td>Conformist (CF)</td>
      <td>El motor de reservas y cobros adopta directamente los identificadores y esquemas básicos de usuario y cliente provistos por Profiles para simplificar el enlace de folios comerciales.</td>
    </tr>
    <tr>
      <td><strong>Properties Management → Bookings & Payments</strong></td>
      <td>Properties Management (U) / Bookings & Payments (D)</td>
      <td>Customer / Supplier (C/S)</td>
      <td>Properties provee el catálogo, metadatos y tarifas base de las habitaciones. Bookings actúa como cliente negociando que la disponibilidad sea expuesta eficientemente para evitar bloqueos en reservas concurrentes.</td>
    </tr>
    <tr>
      <td><strong>Properties Management → Operational Tasks</strong></td>
      <td>Properties Management (U) / Operational Tasks (D)</td>
      <td>Customer / Supplier (C/S)</td>
      <td>Operational Tasks necesita conocer la topología de plantas y habitaciones del hotel para asignar cuadrillas de limpieza e inventariar activos de mantenimiento.</td>
    </tr>
    <tr>
      <td><strong>Bookings & Payments → Operational Tasks</strong></td>
      <td>Bookings & Payments (U) / Operational Tasks (D)</td>
      <td>Customer / Supplier (C/S)</td>
      <td>La ejecución de reservas, check-ins y check-outs condiciona directamente la generación y prioridad de órdenes de limpieza y revisión física de habitaciones.</td>
    </tr>
    <tr>
      <td><strong>Bookings & Payments → IoT Stay & Experience</strong></td>
      <td>Bookings & Payments (U) / IoT Stay & Experience (D)</td>
      <td>Customer / Supplier (C/S)</td>
      <td>El acceso digital y el control domótico solo se habilitan ante contratos de reserva válidos y check-in verificado, actuando IoT como consumidor de dichos eventos de ciclo de vida.</td>
    </tr>
    <tr>
      <td><strong>Bookings & Payments → Analytics</strong></td>
      <td>Bookings & Payments (U) / Analytics (D)</td>
      <td>Anti-Corruption Layer (ACL)</td>
      <td>Analytics ingiere métricas transaccionales (ingresos, ocupación, cancelaciones) mediante una capa anticorrupción que traduce esquemas relacionales/OLTP a modelos multidimensionales OLAP.</td>
    </tr>
  </tbody>
</table>

---

## 4.3. Software Architecture

### 4.3.1. Software Architecture System Landscape Diagram
El System Landscape Diagram contextualiza a SmartStay dentro del ecosistema global del negocio hotelero, ilustrando cómo los usuarios humanos, el personal de campo, los dispositivos físicos y los proveedores de nube interactúan con la plataforma central y sus sistemas periféricos.




[DIAGRAMA: C4 - System Landscape Diagram de SmartStay]
Descripción visual: Diagrama C4 a nivel corporativo que sitúa al Enterprise System SmartStay en el centro, delimitado por una frontera empresarial.

* Actores Externos: Huéspedes (Guest), Personal Operativo de Limpieza y Mantenimiento (Staff), Administrador Hotelero (Hotel Manager).
* Sistemas Internos: SmartStay Core Platform (Web Admin, Mobile Apps, Backend Services, IoT Broker).
* Sistemas Externos Integrados:
* Pasarelas de Pago (Stripe/Culqi API vía HTTPS).
* Online Travel Agencies - OTAs (Channel Manager / Booking.com vía APIs de sincronización).
* Servicios de Mensajería Push (Firebase Cloud Messaging).
* Dispositivos Físicos IoT (Cerraduras inteligentes y sensores ambientales en habitaciones).





---

### 4.3.2. Software Architecture Context Level Diagrams
El diagrama de contexto (Nivel 1 de C4) define las fronteras directas del sistema de software SmartStay, sus interfaces con los diferentes tipos de usuarios y los sistemas externos que complementan el flujo de trabajo.




[DIAGRAMA: C4 - System Context Diagram (Nivel 1)]
Descripción visual: Representación centrada en la caja de software "SmartStay System":

* Huésped: Consulta disponibilidad, reserva, realiza check-in digital y controla el entorno IoT de su habitación vía Smartphone.
* Personal de Staff: Recibe y reporta el estado de tareas de limpieza e incidencias operativas vía Smartphone.
* Administrador: Supervisa el estado de ocupación, gestiona tarifas y revisa analíticas financieras vía Navegador Web.
* Pasarela de Pagos Externa: Recibe solicitudes de cobro y tokenización de tarjetas vía HTTPS/REST.
* Plataformas OTA: Envía reservas externas y recibe actualizaciones de cupos de habitaciones.
* Hardware IoT de Habitación: Recibe órdenes de apertura (MQTT) y envía telemetría de temperatura/iluminación.



---

### 4.3.3. Software Architecture Container Level Diagrams
El diagrama de contenedores (Nivel 2 de C4) descompone el sistema SmartStay en sus unidades ejecutables y de almacenamiento independientes, detallando las tecnologías elegidas y los protocolos de comunicación entre ellas.




[DIAGRAMA: C4 - Container Diagram (Nivel 2)]
Descripción visual: Mapeo de contenedores lógicos y de datos interconectados:

1. Single Page Application (Web Admin): Vue.js/TypeScript ejecutándose en el navegador del administrador.
2. Mobile Application: Flutter/Dart compilado de forma nativa en iOS/Android para Huéspedes y Staff.
3. API Gateway / Reverse Proxy (Nginx / Ocelot): Punto de entrada único HTTPS, enrutamiento y limitador de tasa.
4. Identity & Access Microservice (.NET Web API): Emisión y validación de tokens JWT y RBAC.
5. Bookings & Payments Microservice (.NET Web API): Lógica transaccional de reservas y liquidaciones financieras.
6. Operational Tasks Microservice (.NET Web API): Gestión reactiva de tareas de limpieza e incidentes.
7. IoT Engine & Telemetry Service (.NET / Node.js Worker): Conexión bidireccional con actuadores.
8. Message Broker (RabbitMQ / MQTT Broker): Bus de mensajería para eventos de dominio y telemetría de sensores.
9. Distributed Cache (Redis): Almacenamiento en memoria para sesiones y catálogo de disponibilidad.
10. Relational Databases (PostgreSQL): Bases de datos aisladas por Bounded Context según el patrón Database-per-Service.



---

### 4.3.4. Software Architecture Deployment Diagrams
El diagrama de despliegue representa la topología de infraestructura física y virtualizada sobre la cual se instancian los contenedores de software de SmartStay en la nube, asegurando alta disponibilidad, seguridad de red y escalabilidad elástica.




[DIAGRAMA: C4 - Deployment Diagram (Nivel de Infraestructura Cloud)]
Descripción visual: Despliegue sobre arquitectura PaaS/Cloud Native con zonas de red diferenciadas:

1. Client Tier:
* Dispositivos Móviles (Android/iOS) ejecutando SmartStay Mobile App.
* Navegadores Web consumiendo la SPA administrativa servida desde un CDN (Cloudflare / AWS S3 + CloudFront).


2. DMZ / Ingress Network Tier:
* Cloud Load Balancer gestionando terminación TLS/HTTPS y balanceo de carga entre nodos.
* API Gateway Container ejecutándose en clúster gestionado con réplicas mínimas activas.


3. Application Tier (Private Subnet):
* Microservicios de Negocio empaquetados en contenedores Docker (IAM, Bookings, Operations, IoT Engine) orquestados con reinicio automático y sondeo de salud (Health Checks).
* Message Broker Cluster (RabbitMQ/MQTT) en alta disponibilidad para el intercambio de eventos asíncronos.


4. Data Tier (Secure Private Subnet):
* Redis Cluster gestionado para soporte de caché y estado volátil.
* Managed Relational Database (PostgreSQL Multi-AZ) con replicación sincrónica y copias de seguridad continuas.


5. Edge / On-Premise IoT Tier:
* Gateway IoT físico del hotel conectado vía VPN segura / TLS a los microcontroladores de cerraduras y sensores de habitaciones boutique.

