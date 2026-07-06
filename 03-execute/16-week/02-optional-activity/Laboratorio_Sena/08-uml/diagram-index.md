# Índice de Diagramas UML

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Tabla de diagramas

| ID | Tipo | Nombre | Archivo fuente | Exportación | Estado |
|----|------|--------|---------------|-------------|--------|
| D-001 | Clases | Modelo de dominio principal | `diagrams/source/D-001-domain-classes.puml` | `diagrams/exports/D-001-domain-classes.png` | 🔴 Pendiente |
| D-002 | Secuencia | Flujo: Crear horario | `diagrams/source/D-002-crear-horario-seq.puml` | `diagrams/exports/D-002-crear-horario-seq.png` | 🔴 Pendiente |
| D-003 | Secuencia | Flujo: Autenticación (login) | `diagrams/source/D-003-login-seq.puml` | `diagrams/exports/D-003-login-seq.png` | 🔴 Pendiente |
| D-004 | Secuencia | Flujo: Notificación por email | `diagrams/source/D-004-notificacion-seq.puml` | `diagrams/exports/D-004-notificacion-seq.png` | 🔴 Pendiente |
| D-005 | Casos de uso | Sistema de horarios completo | `diagrams/source/D-005-use-cases.puml` | `diagrams/exports/D-005-use-cases.png` | 🔴 Pendiente |
| D-006 | Actividad | Proceso de asignación de horario | `diagrams/source/D-006-asignacion-actividad.puml` | `diagrams/exports/D-006-asignacion-actividad.png` | 🔴 Pendiente |
| D-007 | Estado | Estados de un Horario | `diagrams/source/D-007-horario-states.puml` | `diagrams/exports/D-007-horario-states.png` | 🔴 Pendiente |
| D-008 | Componentes | Arquitectura de microservicios | `diagrams/source/D-008-component-diagram.puml` | `diagrams/exports/D-008-component-diagram.png` | 🔴 Pendiente |

---

## Convenciones

- **Archivos fuente:** Formato PlantUML (`.puml`). Los archivos deben poder renderizarse con PlantUML CLI o la extensión de VS Code.
- **Exportaciones:** PNG de alta resolución (mínimo 1200px de ancho) y SVG cuando sea posible.
- **Nomenclatura:** `D-{NNN}-{nombre-descriptivo}.{ext}` (número de 3 dígitos, nombre en kebab-case).
- **Idioma:** Los diagramas se documentan en español; los identificadores de código en inglés.

---

## Herramientas recomendadas

| Herramienta | Uso |
|------------|-----|
| [PlantUML](https://plantuml.com/) | Crear y editar diagramas `.puml` |
| [draw.io / diagrams.net](https://diagrams.net/) | Alternativa visual para diagramas complejos |
| VS Code + extensión PlantUML | Previsualización en tiempo real |
| `plantuml.jar` CLI | Exportar PNG/SVG en el pipeline CI/CD |

---

## Estado de los diagramas del MVP

Los diagramas marcados como 🔴 Pendiente deben crearse durante las iteraciones de desarrollo. Se prioriza:

1. **D-007** (Estados de Horario) — Fundamental para entender el dominio.
2. **D-002** (Crear horario) — Flujo más crítico del sistema.
3. **D-005** (Casos de uso) — Para comunicar alcance al cliente.
