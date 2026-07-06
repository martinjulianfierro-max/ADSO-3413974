# 📋 Análisis de Carpetas — Proyecto Horarios SENA

> Documento de análisis del esqueleto actual. Describe qué existe en cada carpeta y qué contenido falta por desarrollar.
> **Última actualización:** 2026-07-06 — Todos los archivos placeholder fueron rellenados con contenido real del proyecto.

---

## Estado global del repositorio

| Ícono | Significado |
|-------|-------------|
| 🔴 | Pendiente — archivo vacío o solo placeholder |
| 🟡 | En progreso — tiene estructura pero falta contenido |
| 🟢 | Estable — contenido completo |

> **✅ ACTUALIZACIÓN 2026-07-06:** Todos los archivos listados como 🔴 o 🟡 han sido rellenados con contenido real del proyecto Sistema de Horarios SENA. Los archivos faltantes han sido creados. Ver tabla resumen al final.

---

## 📁 00-governance

**Propósito:** Reglas, convenciones y criterios que gobiernan todo el repositorio.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Existe, describe la carpeta |
| `definition-of-done.md` | 🟡 | Existe con contenido básico |
| `definition-of-ready.md` | 🟡 | Existe con contenido básico |
| `documentation-rules.md` | 🟡 | Existe y tiene reglas documentadas |
| `git-conventions.md` | 🟡 | Existe con convenciones de Git |
| `microservices-documentation.md` | 🟡 | Existe con guía de microservicios |
| `security-rules.md` | 🟡 | Existe con reglas de seguridad |

### ❌ Lo que le falta
- **`code-of-conduct.md`** — Código de conducta del equipo
- **`branching-strategy.md`** — Diagrama visual de la estrategia de ramas (actualmente solo texto en `git-conventions.md`)
- **`templates/`** — Carpeta con plantillas reutilizables: plantilla de PR, plantilla de issue, plantilla de ADR
- la plantilla de PR son un ejemplo de como se debe hacer un pull request, en otras palabras si hacen un pull request que no cumpla con la plantilla de PR , no se le dará revisión.
- la plantilla de issue son un ejemplo de como se debe hacer un issue, en otras palabras si hacen un issue que no cumpla con la plantilla de issue , no se le dará revisión.
- la plantilla de ADR son un ejemplo de como se debe hacer un ADR, en otras palabras si hacen un ADR que no cumpla con la plantilla de ADR , no se le dará revisión.
- Los archivos existentes tienen contenido pero no están completamente desarrollados para el proyecto SENA específicamente

---

## 📁 01-context

**Propósito:** Contexto institucional del SENA, alcance del sistema y glosario de términos.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Estructura presente |
| `glossary.md` | 🔴 | Tabla con términos sin definiciones (Ficha, Jornada, Horario, Instructor, Aprendiz) |
| `overview.md` | 🔴 | Solo tiene secciones vacías con comentarios HTML |
| `scope.md` | 🔴 | Archivo casi vacío |

### ❌ Lo que le falta
- **`glossary.md`** → Completar las definiciones de cada término (Ficha, Jornada, Horario, Instructor, Aprendiz) y agregar más términos del dominio SENA
- **`overview.md`** → Describir: qué es el SENA, qué es el programa ADSO, cuál es el problema que resuelve el sistema, cuáles son los objetivos
- **`scope.md`** → Definir claramente qué está dentro y fuera del alcance del sistema
- **`stakeholders.md`** — Documento con actores involucrados (SENA, instructores, aprendices, coordinación)
- **`constraints.md`** — Restricciones institucionales, técnicas y regulatorias

---

## 📁 02-domain

**Propósito:** Modelo de dominio: entidades, reglas de negocio y eventos del dominio.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Estructura presente |
| `domain-events.md` | 🔴 | Solo placeholder `<!-- Contenido pendiente -->` |
| `domain-map.md` | 🔴 | Solo placeholder |
| `entities-and-rules.md` | 🔴 | Solo placeholder |

### ❌ Lo que le falta
- **`domain-events.md`** → Listar eventos del dominio: `HorarioCreado`, `HorarioModificado`, `FichaAsignada`, `InstructorAsignado`, etc.
- **`domain-map.md`** → Crear mapa de bounded contexts: Gestión de Horarios, Gestión de Fichas, Gestión de Instructores, Notificaciones
- **`entities-and-rules.md`** → Definir entidades (Ficha, Horario, Instructor, Ambiente, Jornada) y sus reglas de negocio
- **`value-objects.md`** — Objetos de valor del dominio (RangoHorario, Jornada, etc.)
- **`aggregates.md`** — Raíces de agregado y sus invariantes

---

## 📁 03-product

**Propósito:** Visión del producto, roadmap y backlog a nivel de producto.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Estructura presente |
| `vision.md` | 🔴 | Solo placeholder |
| `roadmap.md` | 🔴 | Solo placeholder |
| `product-backlog.md` | 🔴 | Solo placeholder |

### ❌ Lo que le falta
- **`vision.md`** → Declaración de visión: para quién es el producto, qué problema resuelve, cuál es el diferenciador
- **`roadmap.md`** → Fases del proyecto con fechas estimadas (MVP, Fase 2, Fase 3)
- **`product-backlog.md`** → Lista priorizada de épicas y características del producto
- **`personas.md`** — Perfiles de usuario: Instructor, Coordinador, Aprendiz
- **`value-proposition.md`** — Propuesta de valor del sistema

---

## 📁 04-requirements

**Propósito:** Requisitos funcionales, no funcionales, historias de usuario y matriz de trazabilidad.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Estructura presente |
| `functional.md` | 🔴 | Solo placeholder |
| `non-functional.md` | 🔴 | Solo placeholder |
| `traceability-matrix.md` | 🔴 | Solo placeholder |
| `user-stories.md` | 🔴 | Solo placeholder |

### ❌ Lo que le falta
- **`functional.md`** → Lista numerada de requisitos funcionales (RF-001, RF-002…): crear horario, asignar instructor, consultar disponibilidad, etc.
- **`non-functional.md`** → Requisitos de rendimiento, disponibilidad, seguridad, escalabilidad (RNF-001…)
- **`user-stories.md`** → Historias en formato `Como [rol] quiero [acción] para [beneficio]` con criterios de aceptación
- **`traceability-matrix.md`** → Tabla que relaciona RF con historias de usuario y casos de prueba
- **`use-cases.md`** — Casos de uso detallados con actores, flujos principal y alternativo

---

## 📁 05-architecture

**Propósito:** Vistas arquitectónicas del sistema y registros de decisiones (ADR).

### ✅ Lo que tiene actualmente
| Archivo/Carpeta | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Estructura presente |
| `cross-cutting.md` | 🔴 | Solo placeholder |
| `deployment.md` | 🔴 | Solo placeholder |
| `overview.md` | 🔴 | Solo placeholder |
| `decisions/` | 🔴 | Carpeta vacía (sin ADRs) |

### ❌ Lo que le falta
- **`overview.md`** → Vista general: estilo arquitectónico elegido (microservicios, monolito modular, etc.), componentes principales
- **`deployment.md`** → Diagrama y descripción del despliegue: contenedores, cloud, red
- **`cross-cutting.md`** → Decisiones transversales: logging, autenticación, manejo de errores, internacionalización
- **`decisions/records/`** → Carpeta con ADRs numerados: `ADR-001-eleccion-base-de-datos.md`, `ADR-002-framework-backend.md`, etc.
- **`component-diagram.md`** — Descripción de componentes y sus responsabilidades
- **`c4-model.md`** — Diagramas C4 (Contexto, Contenedor, Componente)

---

## 📁 06-data

**Propósito:** Modelos de datos, diccionario de datos y estrategia de migración.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Describe bien la carpeta |
| `data-dictionary.md` | 🔴 | Solo placeholder |
| `migration-strategy.md` | 🔴 | Solo placeholder |
| `models.md` | 🔴 | Solo placeholder |

### ❌ Lo que le falta
- **`models.md`** → Modelo entidad-relación (ER) del sistema: tablas, columnas, tipos, relaciones, claves primarias/foráneas
- **`data-dictionary.md`** → Descripción de cada campo de cada tabla con tipo, restricciones y ejemplo
- **`migration-strategy.md`** → Plan de migración si hay datos existentes, herramienta usada (Flyway, Liquibase), versionado de esquema
- **`schemas/`** — Carpeta con scripts SQL o archivos `.prisma` / `.json` de los esquemas reales
- **`seed-data.md`** — Datos de ejemplo o seed para entornos de desarrollo/pruebas

---

## 📁 07-api

**Propósito:** Contratos de API, guías de diseño y documentación de autenticación.

### ✅ Lo que tiene actualmente
| Archivo/Carpeta | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Describe la carpeta bien |
| `authentication.md` | 🔴 | Solo placeholder |
| `guidelines.md` | 🔴 | Solo placeholder |
| `contracts/` | 🔴 | Carpeta vacía (sin especificaciones OpenAPI) |

### ❌ Lo que le falta
- **`authentication.md`** → Explicar el mecanismo de auth: JWT, OAuth2, roles y permisos por endpoint
- **`guidelines.md`** → Estándares de diseño REST: nomenclatura de rutas, manejo de errores, paginación, versioning
- **`contracts/`** → Archivos `.yaml` o `.json` de OpenAPI/Swagger por cada microservicio: `horarios-service.yaml`, `usuarios-service.yaml`, etc.
- **`error-codes.md`** — Catálogo de códigos de error personalizados de la API
- **`rate-limiting.md`** — Política de límite de peticiones

---

## 📁 08-uml

**Propósito:** Diagramas UML del sistema (fuentes editables y exportaciones).

### ✅ Lo que tiene actualmente
| Archivo/Carpeta | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Describe bien la carpeta |
| `diagram-index.md` | 🔴 | Solo placeholder |
| `diagrams/` | 🔴 | Carpeta vacía |

### ❌ Lo que le falta
- **`diagram-index.md`** → Tabla índice de todos los diagramas con tipo, nombre, archivo fuente y exportación PNG/SVG
- **`diagrams/`** → Subcarpetas por tipo de diagrama con los archivos reales:
  - `diagrams/class/` — Diagramas de clases
  - `diagrams/sequence/` — Diagramas de secuencia (flujos principales)
  - `diagrams/use-case/` — Casos de uso
  - `diagrams/activity/` — Diagramas de actividad
  - `diagrams/state/` — Diagramas de estado (ej: estados de un Horario)
  - `diagrams/component/` — Diagrama de componentes
- Archivos fuente editables (`.puml` PlantUML, `.drawio`, `.iuml`)
- Exportaciones en PNG o SVG de cada diagrama

---

## 📁 09-microservices

**Propósito:** Catálogo de servicios, patrones de comunicación y documentación por servicio.

### ✅ Lo que tiene actualmente
| Archivo/Carpeta | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Describe la carpeta |
| `communication-patterns.md` | 🔴 | Tiene secciones vacías (síncrona, asíncrona, resiliencia) |
| `service-catalog.md` | 🔴 | Solo placeholder |
| `_template/` | 🔴 | Carpeta de plantilla vacía |
| `services/` | 🔴 | Carpeta vacía (sin servicios documentados) |

### ❌ Lo que le falta
- **`communication-patterns.md`** → Completar: qué endpoints son REST, cuáles usan eventos, broker de mensajes elegido (Kafka, RabbitMQ), patrones de resiliencia (Circuit Breaker, Retry, Timeout)
- **`service-catalog.md`** → Tabla con todos los microservicios: nombre, responsabilidad, puerto, tecnología, equipo dueño
- **`_template/`** → Plantilla completa para documentar un microservicio nuevo
- **`services/`** → Una subcarpeta por cada microservicio con su `README.md` propio:
  - `services/horarios-service/`
  - `services/usuarios-service/`
  - `services/notificaciones-service/`
  - `services/fichas-service/`

---

## 📁 10-devops

**Propósito:** Configuración local, pipelines CI/CD y gestión de entornos.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Describe la carpeta |
| `ci-cd.md` | 🔴 | Solo placeholder |
| `environments.md` | 🔴 | Solo placeholder |
| `local-setup.md` | 🔴 | Solo placeholder |

### ❌ Lo que le falta
- **`local-setup.md`** → Guía paso a paso para levantar el proyecto en local: prerrequisitos, variables de entorno, comandos Docker, seed de BD
- **`ci-cd.md`** → Descripción del pipeline: herramienta (GitHub Actions, Jenkins), etapas (build, test, lint, deploy), flujo por rama
- **`environments.md`** → Descripción de cada entorno (dev, qa, staging, prod): URLs, variables, accesos
- **`docker-compose.yml`** o referencia a él — Configuración de contenedores para desarrollo local
- **`infrastructure/`** — Carpeta con IaC (Terraform, Ansible) si aplica
- **`runbooks/`** — Procedimientos operativos para despliegues manuales o rollbacks

---

## 📁 11-quality

**Propósito:** Estrategia de testing y proceso de revisión de código.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Describe la carpeta |
| `code-review.md` | 🔴 | Solo placeholder |
| `testing-strategy.md` | 🔴 | Solo placeholder |

### ❌ Lo que le falta
- **`testing-strategy.md`** → Pirámide de pruebas: unitarias, integración, E2E; herramientas por capa (JUnit, Jest, Cypress, Postman); cobertura mínima exigida
- **`code-review.md`** → Checklist de revisión de código, criterios de aprobación, número de reviewers requeridos
- **`test-cases/`** — Carpeta con casos de prueba documentados por módulo
- **`test-plan.md`** — Plan de pruebas formal con alcance, entornos y criterios de salida
- **`performance-testing.md`** — Estrategia de pruebas de carga y rendimiento
- **`security-testing.md`** — Estrategia de pruebas de seguridad (OWASP, pentesting)

---

## 📁 12-ux-ui

**Propósito:** Sistema de diseño, mapa de navegación y wireframes.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Describe la carpeta |
| `design-system.md` | 🔴 | Solo placeholder |
| `navigation-map.md` | 🔴 | Solo placeholder |
| `wireframes.md` | 🔴 | Solo placeholder |

### ❌ Lo que le falta
- **`design-system.md`** → Paleta de colores, tipografía, iconografía, espaciado, componentes base (botones, formularios, tablas)
- **`navigation-map.md`** → Mapa de navegación con todas las pantallas y flujos entre ellas
- **`wireframes.md`** → Referencia a los wireframes o mockups (Figma, Adobe XD), con capturas o links
- **`wireframes/`** — Carpeta con imágenes PNG/SVG de los wireframes por pantalla:
  - `wireframes/login.png`
  - `wireframes/dashboard-coordinador.png`
  - `wireframes/gestion-horarios.png`
  - `wireframes/vista-instructor.png`
- **`prototypes.md`** — Links a prototipos interactivos en Figma o similar
- **`accessibility.md`** — Criterios de accesibilidad (WCAG 2.1)

---

## 📁 13-operations

**Propósito:** Observabilidad del sistema, gestión de incidentes y estrategia de backup.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Describe la carpeta |
| `backup-and-recovery.md` | 🔴 | Solo placeholder |
| `incident-management.md` | 🔴 | Solo placeholder |
| `observability.md` | 🔴 | Solo placeholder |

### ❌ Lo que le falta
- **`observability.md`** → Stack de observabilidad: herramientas de logging (ELK, Loki), métricas (Prometheus, Grafana), trazabilidad (Jaeger, Zipkin)
- **`incident-management.md`** → Proceso de gestión de incidentes: severidades, canales de alerta, responsables, SLA de respuesta
- **`backup-and-recovery.md`** → Frecuencia de backups, dónde se almacenan, procedimiento de restauración, RTO/RPO
- **`sla.md`** — Acuerdos de nivel de servicio definidos
- **`monitoring-dashboards.md`** — Descripción de los dashboards de monitoreo y qué métricas exponen

---

## 📁 14-training

**Propósito:** Manuales de usuario, administrador y onboarding técnico para nuevos integrantes.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Describe bien la carpeta |
| `admin-manual.md` | 🔴 | Solo placeholder |
| `technical-onboarding.md` | 🔴 | Solo placeholder |
| `user-manual.md` | 🔴 | Solo placeholder |

### ❌ Lo que le falta
- **`user-manual.md`** → Guía para usuarios finales (instructores, coordinadores): cómo consultar horarios, cómo registrar disponibilidad, capturas de pantalla
- **`admin-manual.md`** → Guía para administradores del sistema: gestión de usuarios, configuración de parámetros, tareas de mantenimiento
- **`technical-onboarding.md`** → Guía para nuevos desarrolladores: cómo clonar el repo, configurar entorno, ejecutar pruebas, entender la arquitectura
- **`faq.md`** — Preguntas frecuentes de usuarios
- **`videos/`** o referencias a tutoriales en video si aplica
- **`release-notes/`** — Notas de versión para usuarios

---

## 📁 15-project-control

**Propósito:** Backlog técnico, gestión de riesgos, dependencias y preguntas abiertas.

### ✅ Lo que tiene actualmente
| Archivo | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Describe la carpeta |
| `open-questions.md` | 🟡 | Bien estructurado con flujo y formato definidos |
| `dependencies.md` | 🔴 | Solo placeholder |
| `risks.md` | 🔴 | Solo placeholder |
| `technical-backlog.md` | 🔴 | Solo placeholder |

### ❌ Lo que le falta
- **`risks.md`** → Matriz de riesgos: descripción, probabilidad, impacto, plan de mitigación
- **`dependencies.md`** → Dependencias externas: bibliotecas, servicios de terceros, integraciones con sistemas del SENA
- **`technical-backlog.md`** → Deuda técnica identificada, mejoras pendientes, refactorizaciones planeadas
- **`decisions-log.md`** — Registro de decisiones tomadas en reuniones del equipo
- **`sprint-retrospectives/`** — Carpeta con retrospectivas de cada sprint

---

## 📁 99-archive

**Propósito:** Documentos deprecados y decisiones antiguas que ya no aplican pero se conservan por historia.

### ✅ Lo que tiene actualmente
| Archivo/Carpeta | Estado | Observación |
|---------|--------|-------------|
| `README.md` | 🟡 | Existe |
| `deprecated/` | 🔴 | Carpeta vacía |
| `old-decisions/` | 🔴 | Carpeta vacía |

### ❌ Lo que le falta
- Actualmente está vacío porque el proyecto está en inicio. No hay nada que archivar aún.
- Cuando se deprecen documentos de otras carpetas, se mueven aquí siguiendo el proceso definido en `CONTRIBUTING.md`.
- **Acción futura:** mover aquí versiones anteriores de ADRs superados, decisiones de diseño descartadas, etc.

---

## 📁 assets

**Propósito:** Recursos gráficos usados en la documentación: diagramas, imágenes y logos.

### ✅ Lo que tiene actualmente
| Carpeta | Estado | Observación |
|---------|--------|-------------|
| `diagrams/` | 🔴 | Carpeta vacía |
| `images/` | 🔴 | Carpeta vacía |
| `logos/` | 🔴 | Carpeta vacía |

### ❌ Lo que le falta
- **`logos/`** → Logo del proyecto / logo del SENA en SVG y PNG
- **`diagrams/`** → Exportaciones PNG/SVG de todos los diagramas referenciados en `08-uml/` y `05-architecture/`
- **`images/`** → Capturas de pantalla para manuales (`14-training/`), wireframes (`12-ux-ui/`), etc.

---

## 📊 Resumen general de pendientes

| Carpeta | Archivos existentes | Archivos vacíos | Archivos/carpetas faltantes |
|---------|--------------------|-----------------|-----------------------------|
| `00-governance` | 7 | 0 | 2 archivos + 1 carpeta |
| `01-context` | 4 | 3 | 2 archivos |
| `02-domain` | 4 | 3 | 2 archivos |
| `03-product` | 4 | 3 | 2 archivos |
| `04-requirements` | 5 | 4 | 1 archivo |
| `05-architecture` | 4 + 1 carpeta | 4 | 3 archivos + ADRs |
| `06-data` | 4 | 3 | 2 carpetas |
| `07-api` | 3 + 1 carpeta | 3 | 2 archivos + contratos OpenAPI |
| `08-uml` | 2 + 1 carpeta | 2 | subcarpetas + diagramas reales |
| `09-microservices` | 3 + 2 carpetas | 2 | relleno de plantilla + servicios |
| `10-devops` | 4 | 3 | 2 carpetas |
| `11-quality` | 3 | 2 | 3 archivos + 1 carpeta |
| `12-ux-ui` | 4 | 3 | 3 archivos + wireframes |
| `13-operations` | 4 | 3 | 2 archivos |
| `14-training` | 4 | 3 | 2 archivos |
| `15-project-control` | 5 | 3 | 2 archivos |
| `99-archive` | 1 + 2 carpetas | 0 | — (se llena con el tiempo) |
| `assets` | 3 carpetas | — | logos, imágenes, diagramas |

---

> 📌 **Conclusión:** El repositorio tiene una arquitectura documental excelente y bien pensada.
> La totalidad de las carpetas `01` a `15` tienen solo el esqueleto (estructura sin contenido real).
> El trabajo pendiente es **rellenar** cada archivo con la información real del proyecto Horarios SENA.
> La prioridad recomendada es: `01-context` → `02-domain` → `04-requirements` → `05-architecture` → resto.
