<div style="text-align: center;">

<img src="assets/images/readme/upc-logo.png" style="width: 150px;"/>

Universidad Peruana De Ciencias Aplicadas

Carrera de Ingeniería de Software

**1ASI0728**

**Arquitecturas de Software Emergentes**

NRC  
**9077**

**Informe del Trabajo Final**

Docente  
**Jara Palacios, Marino Humberto**

Equipo  
**Movildev**

Proyecto  
**SmartStay**

**Integrantes**

<table style="margin: 0 auto; border-collapse: collapse; text-align: left;">
  <thead>
    <tr>
      <th style="padding: 8px 16px;">Código</th>
      <th style="padding: 8px 16px;">Apellidos y Nombres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding: 8px 16px;">U202117377</td>
      <td style="padding: 8px 16px;">Arévalo Meza, John Telesforo</td>
    </tr>
    <tr>
      <td style="padding: 8px 16px;">U202222275</td>
      <td style="padding: 8px 16px;">Howard Robles, Guillermo Arturo</td>
    </tr>
    <tr>
      <td style="padding: 8px 16px;">U202310988</td>
      <td style="padding: 8px 16px;;">Santur Tello, Andrea Elizabeth</td>
    </tr>
    <tr>
      <td style="padding: 8px 16px;">U20221E617</td>
      <td style="padding: 8px 16px;">Verona Flores, Ítalo Sebastián</td>
    </tr>
  </tbody>
</table>

**Período 202620**

**Agosto 2026**

</div>

<div style="page-break-after: always;"></div>

## Registro de Versiones del Informe

| Versión |   Fecha    | Autor                                  | Descripción de modificación                                                           |
|:-------:|:----------:|----------------------------------------|---------------------------------------------------------------------------------------|
|   0.1   | 15/09/2026 | Howard Robles, Guillermo Arturo        | Creacion del reporte inicial y el startup profile.                                    | 
|   0.2    | 15/09/2026 | Howard Robles, Guillermo Arturo        | Creación del solution profile                                                         | 
|   0.3     | 16/09/2026    | Santur Tello, Andrea Elizabeth | Creación del competitive analysis and competitors   |
|   0.4 | 17/09/2026 | Howard Robles, Guillermo Arturo | Creacion del registro de versiones | 
| 0.5 | 17/09/2026 | Arévalo Meza, John Telesforo | Creación del capítulo de Introduction |
|1.1 | 02/10/2026 | Howard Robles, Guillermo Arturo | Creacion del capitulo bounded context Profiles | 
 | 1.2 | 03/10/2026 | Howard Robles, Guillermo Arturo | Creacion del bounded context profiles |
|1.3 | 03/10/2026 | Howard Robles, Guillermo Arturo | Creacion del bounded context iam |
|1.4 | 03/10/2026 | Howard Robles, Guillermo Arturo | Creacion del bounded context properties management |
|1.5 | 04/10/2026 | Howard Robles, Guillermo Arturo | Creacion del bounded context Bookings & Payments  |

---

<div style="page-break-after: always;"></div>

## Project Report Collaboration Insights

Esta sección detalla cómo el equipo colaboró para construir el **Final Project Documentation Report** del sistema SmartStay, mostrando evidencia de trabajo conjunto mediante commits, revisiones, herramientas de organización y resultados integrados en el informe final. Se refleja la contribución de cada integrante en la planificación, desarrollo, documentación y presentación de la solución.

**Repositorio del informe del proyecto:**  
[https://github.com/1ASI0728-9077-SmartStay-Movildev/upc-pre-202610-1asi0728-9077-SmartStay-report](https://github.com/1ASI0728-9077-SmartStay-Movildev/upc-pre-202610-1asi0728-9077-SmartStay-report)

## Tabla de contenido

- [Chapter I: Introduction](#chapter-i-introduction)
 - [1.1. Startup Profile](#11-startup-profile)
  - [1.1.1 Descripción de la Startup](#111-descripción-de-la-startup)
  - [1.1.2 Perfiles de integrantes del equipo](#112-perfiles-de-integrantes-del-equipo)
 - [1.2 Solution Profile](#12-solution-profile)
  - [1.2.1 Antecedentes y problemática](#121-antecedentes-y-problemática)
  - [1.2.2 Lean UX Process](#122-lean-ux-process)
   - [1.2.2.1. Lean UX Problem Statements](#1221-lean-ux-problem-statements)
   - [1.2.2.2. Lean UX Assumptions](#1222-lean-ux-assumptions)
   - [1.2.2.3. Lean UX Hypothesis Statements](#1223-lean-ux-hypothesis-statements)
   - [1.2.2.4. Lean UX Canvas](#1224-lean-ux-canvas)
 - [1.3. Segmentos Objetivo](#13-segmentos-objetivo)
- [Chapter II: Requirements Elicitation \& Analysis](#chapter-ii-requirements-elicitation--analysis)
 - [2.1. Competidores](#21-competidores)
  - [2.1.1. Análisis competitivo](#211-análisis-competitivo)
  - [2.1.2. Estrategias y tácticas frente a competidores](#212-estrategias-y-tácticas-frente-a-competidores)
 - [2.2. Entrevistas](#22-entrevistas)
  - [2.2.1. Diseño de entrevistas](#221-diseño-de-entrevistas)
  - [2.2.2. Registro de entrevistas](#222-registro-de-entrevistas)
  - [2.2.3. Análisis de entrevistas](#223-análisis-de-entrevistas)
 - [2.3. Needfinding](#23-needfinding)
  - [2.3.1 User Personas](#231-user-personas)
  - [2.3.2 User Task Matrix](#232-user-task-matrix)
  - [2.3.3 Empathy Mapping](#233-empathy-mapping)
  - [2.3.4 As-is Scenario Mapping](#234-as-is-scenario-mapping)
  - [2.4. Ubiquitous Language](#24-ubiquitous-language)
- [Chapter III: Requirements Specification](#chapter-iii-requirements-specification)
 - [3.1. To-Be Scenario Mapping](#31-to-be-scenario-mapping)
 - [3.2. User Stories](#32-user-stories)
 - [3.3. Impact Mapping](#33-impact-mapping)
 - [3.4. Product Backlog](#34-product-backlog)
- [Capítulo IV: Strategic-Level Software Design](#capítulo-iv-strategic-level-software-design)
 - [4.1. Strategic-Level Attribute-Driven Design](#41-strategic-level-attribute-driven-design)
  - [4.1.1. Design Purpose](#411-design-purpose)
  - [4.1.2. Attribute-Driven Design Inputs](#412-attribute-driven-design-inputs)
   - [4.1.2.1. Primary Functionality (Primary User Stories)](#4121-primary-functionality-primary-user-stories)
   - [4.1.2.2. Quality Attribute Scenarios](#4122-quality-attribute-scenarios)
   - [4.1.2.3. Constraints](#4123-constraints)
  - [4.1.3. Architectural Drivers Backlog](#413-architectural-drivers-backlog)
  - [4.1.4. Architectural Design Decisions](#414-architectural-design-decisions)
  - [4.1.5. Quality Attribute Scenario Refinements](#415-quality-attribute-scenario-refinements)
 - [4.2. Strategic-Level Domain-Driven Design](#42-strategic-level-domain-driven-design)
  - [4.2.1. EventStorming](#421-eventstorming)
  - [4.2.2. Candidate Context Discovery](#422-candidate-context-discovery)
  - [4.2.3. Domain Message Flows Modeling](#423-domain-message-flows-modeling)
  - [4.2.4. Bounded Context Canvases](#424-bounded-context-canvases)
  - [4.2.5. Context Mapping](#425-context-mapping)
 - [4.3. Software Architecture](#43-software-architecture)
  - [4.3.1. Software Architecture System Landscape Diagram](#431-software-architecture-system-landscape-diagram)
  - [4.3.2. Software Architecture Context Level Diagrams](#432-software-architecture-context-level-diagrams)
  - [4.3.3. Software Architecture Container Level Diagrams](#433-software-architecture-container-level-diagrams)
  - [4.3.4. Software Architecture Deployment Diagrams](#434-software-architecture-deployment-diagrams)
- [Capítulo V: Tactical-Level Software Design.](#capítulo-v-tactical-level-software-design)
 - [5.1. Bounded Context: Profiles](#51-bounded-context-profiles)
  - [5.1.1. Domain Layer.](#511-domain-layer)
  - [5.1.2. Interface Layer.](#512-interface-layer)
  - [5.1.3. Application Layer.](#513-application-layer)
  - [5.1.4. Infrastructure Layer.](#514-infrastructure-layer)
  - [5.1.5. Bounded Context Software Architecture Component Level Diagrams.](#515-bounded-context-software-architecture-component-level-diagrams)
  - [5.1.6. Bounded Context Software Architecture Code Level Diagrams.](#516-bounded-context-software-architecture-code-level-diagrams)
   - [5.1.6.1. Bounded Context Domain Layer Class Diagrams.](#5161-bounded-context-domain-layer-class-diagrams)
   - [5.1.6.2. Bounded Context Database Design Diagram.](#5162-bounded-context-database-design-diagram)
 - [5.2. Bounded Context: IAM](#52-bounded-context-iam)
  - [5.2.1. Domain Layer.](#521-domain-layer)
  - [5.2.2. Interface Layer.](#522-interface-layer)
  - [5.2.3. Application Layer.](#523-application-layer)
  - [5.2.4. Infrastructure Layer.](#524-infrastructure-layer)
  - [5.2.5. Bounded Context Software Architecture Component Level Diagrams.](#525-bounded-context-software-architecture-component-level-diagrams)
  - [5.2.6. Bounded Context Software Architecture Code Level Diagrams.](#526-bounded-context-software-architecture-code-level-diagrams)
   - [5.2.6.1. Bounded Context Domain Layer Class Diagrams.](#5261-bounded-context-domain-layer-class-diagrams)
   - [5.2.6.2. Bounded Context Database Design Diagram.](#5262-bounded-context-database-design-diagram)
 - [5.3. Bounded Context: Properties Management](#53-bounded-context-properties-management)
  - [5.3.1. Domain Layer.](#531-domain-layer)
  - [5.3.2. Interface Layer.](#532-interface-layer)
  - [5.3.3. Application Layer.](#533-application-layer)
  - [5.3.4. Infrastructure Layer.](#534-infrastructure-layer)
  - [5.3.5. Bounded Context Software Architecture Component Level Diagrams.](#535-bounded-context-software-architecture-component-level-diagrams)
  - [5.3.6. Bounded Context Software Architecture Code Level Diagrams.](#536-bounded-context-software-architecture-code-level-diagrams)
   - [5.3.6.1. Bounded Context Domain Layer Class Diagrams.](#5361-bounded-context-domain-layer-class-diagrams)
   - [5.3.6.2. Bounded Context Database Design Diagram.](#5362-bounded-context-database-design-diagram)
 - [5.X. Bounded Context: ](#5x-bounded-context-)
  - [5.X.1. Domain Layer.](#5x1-domain-layer)
  - [5.X.2. Interface Layer.](#5x2-interface-layer)
  - [5.X.3. Application Layer.](#5x3-application-layer)
  - [5.X.4. Infrastructure Layer.](#5x4-infrastructure-layer)
  - [5.X.5. Bounded Context Software Architecture Component Level Diagrams.](#5x5-bounded-context-software-architecture-component-level-diagrams)
  - [5.X.6. Bounded Context Software Architecture Code Level Diagrams.](#5x6-bounded-context-software-architecture-code-level-diagrams)
   - [5.X.6.1. Bounded Context Domain Layer Class Diagrams.](#5x61-bounded-context-domain-layer-class-diagrams)
   - [5.X.6.2. Bounded Context Database Design Diagram.](#5x62-bounded-context-database-design-diagram)
- [Capítulo VI: Solution UI/UX Design](#capítulo-vi-solution-uiux-design)
 - [6.1 Style Guidelines](#61-style-guidelines)
  - [6.1.1 General Style Guidelines](#611-general-style-guidelines)
  - [6.1.2. Web, Mobile \& Devices Style Guidelines](#612-web-mobile--devices-style-guidelines)
 - [6.2 Information Architecture](#62-information-architecture)
  - [6.2.1 Organization Systems](#621-organization-systems)
  - [6.2.2 Labeling Systems](#622-labeling-systems)
  - [6.2.3 Searching Systems](#623-searching-systems)
  - [6.2.4 SEO Tags, Meta Tags y ASO Elements](#624-seo-tags-meta-tags-y-aso-elements)
  - [6.2.5 Navigation Systems](#625-navigation-systems)
 - [6.3 Landing Page UI Design](#63-landing-page-ui-design)
  - [6.3.1 Landing Page Wireframe](#631-landing-page-wireframe)
  - [6.3.2 Landing Page Mock-up](#632-landing-page-mock-up)
- [Capitulo VII: Product Implementation, Validation, and Deployment.](#capitulo-vii-product-implementation-validation-and-deployment)
- [Conclusiones](#conclusiones)
- [Bibliografía](#bibliografía)
- [Anexos](#anexos)

<div style="page-break-after: always;"></div>

## Student Outcome 3

**Criterio:** Capacidad de comunicarse efectivamente con un rango de audiencias. En el siguiente cuadro se describe las acciones realizadas y enunciados de conclusiones por parte del grupo, que permiten sustentar el haber alcanzado el logro del ABET – EAC - Student Outcome 3.

<table border="1" style="width: 100%; border-collapse: collapse;">
<thead>
    <tr>
        <th style="padding: 20px; text-align: left; width: 18%;">Criterio específico</th>
        <th style="padding: 20px; text-align: left; width: 50%;">Acciones realizadas</th>
        <th style="padding: 20px; text-align: left; width: 32%;">Conclusiones</th>
    </tr>
</thead>
<tbody>
    <tr>
        <td style="padding: 15px; text-align: left; vertical-align: top; font-weight: bold;">Comunica oralmente sus ideas y/o resultados con objetividad a público de diferentes especialidades y niveles jerarquicos, en el marco del desarrollo de un proyecto en ingeniería.</td>
        <td style="padding: 15px; text-align: left; vertical-align: top;">
            <strong>Arévalo Meza, John Telesforo</strong><br>
            <strong>AV1:</strong> Comunico<br>
            <strong>Howard Robles, Guillermo Arturo</strong><br>
            <strong>AV1:</strong> Comunico<br>
            <strong>Santur Tello, Andrea Elizabeth</strong><br>
            <strong>AV1:</strong> Comunico<br>
            <strong>Verona Flores, Ítalo Sebastián</strong><br>
            <strong>AV1:</strong> Sustentación y explicación técnica de las decisiones de diseño arquitectónico estratégico basadas en Attribute-Driven Design (ADD) y EventStorming ante el equipo de desarrollo, pares académicos y el docente del curso.<br>
        </td>
        <td style="padding: 15px; text-align: left; vertical-align: top;">
            <strong>AV1:</strong> Se definió la visión del producto y objetivos mediante la participación del Product Owner y el equipo. Se elaboraron historias de usuario, análisis de competidores y needfinding. Se aplicó event storming y se diseñaron interfaces UX. Demostró la capacidad de transmitir conceptos complejos de arquitectura de software y diseño orientado a dominios (DDD) de manera clara y objetiva.<br><br>
        </td>
    </tr>
    <tr>
        <td style="padding: 15px; text-align: left; vertical-align: top; font-weight: bold;">Comunica en forma escrita ideas y/o resultados con objetividad a público de diferentes especialidades y niveles jerarquicos, en el marco del desarrollo de un proyecto en ingeniería..</td>
        <td style="padding: 15px; text-align: left; vertical-align: top;">
            <strong>Arévalo Meza, John Telesforo</strong><br>
            <strong>AV1:</strong> Comunico<br>
            <strong>Howard Robles, Guillermo Arturo</strong><br>
            <strong>AV1:</strong> Comunico<br>
            <strong>Santur Tello, Andrea Elizabeth</strong><br>
            <strong>AV1:</strong> Comunico<br>
            <strong>Verona Flores, Ítalo Sebastián</strong><br>
            <strong>AV1:</strong> Redacción, estructuración y refinamiento técnico de los capítulos correspondientes al diseño a nivel estratégico de software, incluyendo el Attribute-Driven Design Inputs, la definición del Architectural Drivers Backlog, y las decisiones de diseño arquitectónico (Architectural Design Decisions).<br>
        </td>
        <td style="padding: 15px; text-align: left; vertical-align: top;">
            <strong>AV1:</strong> Se estableció un flujo de trabajo basado en Gitflow y conventional commits. Se definieron metas semanales y se promovió la participación equitativa. El equipo cumplió con los objetivos del hito, evidenciando competencia para redactar documentación de ingeniería clara, estructurada y rigurosa.<br><br>
        </td>
    </tr>
</tbody>
</table>

