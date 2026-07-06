# Registro de Decisiones del Equipo

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

Este documento registra las decisiones tomadas en reuniones del equipo que no son decisiones de arquitectura formal (las ADRs van en `05-architecture/decisions/records/`), pero sí son relevantes para la historia del proyecto.

---

## Formato de entrada

```
## DEC-{NNN} — {Título de la decisión}
**Fecha:** YYYY-MM-DD
**Participantes:** [nombres o roles]
**Contexto:** Descripción breve de por qué se tomó la decisión.
**Decisión:** Qué se decidió exactamente.
**Consecuencias:** Qué cambia como resultado.
```

---

## DEC-001 — Adopción de Markdown para toda la documentación

**Fecha:** 2026-06-16
**Participantes:** Equipo completo (kick-off)
**Contexto:** El equipo necesitaba un formato de documentación que pudiera versionarse con Git, ser legible sin herramientas especiales y compatible con GitHub.
**Decisión:** Toda la documentación del repositorio se escribe en Markdown (`.md`). No se usan formatos binarios (Word, PDF) como fuente de verdad.
**Consecuencias:** La documentación es portable, versionable y colaborativa. Los diagramas que requieren herramientas visuales (Figma, draw.io) se referencian con links, no se incrustan como binarios.

---

## DEC-002 — Idioma del proyecto

**Fecha:** 2026-06-16
**Participantes:** Equipo completo
**Contexto:** El equipo es 100% hispanohablante y el cliente (SENA) opera en español.
**Decisión:** El contenido de la documentación y la UI están en español. Los identificadores de código (nombres de clases, métodos, variables, ramas, commits) están en inglés. Los mensajes de commit siguen el formato Conventional Commits en inglés.
**Consecuencias:** Coherencia entre el lenguaje del cliente y la documentación; estándares de código alineados con la industria.

---

## DEC-003 — Prioridad del MVP

**Fecha:** 2026-07-06
**Participantes:** Líder técnico + coordinador académico (cliente)
**Contexto:** El equipo tiene un plazo de ~6 meses y debe entregar algo funcional. Se discutió qué funcionalidades son imprescindibles para el lanzamiento.
**Decisión:** El MVP incluye: autenticación, CRUD de fichas/instructores/ambientes, creación y edición de horarios con detección de conflictos, y vista de horario por rol. Quedan fuera del MVP: notificaciones, reportes, historial completo de auditoría.
**Consecuencias:** El equipo puede enfocarse en el valor central. Las funcionalidades excluidas se agregan en Fase 2. Ver `03-product/roadmap.md`.

---

## DEC-004 — Uso de Docker Compose para desarrollo local

**Fecha:** 2026-07-06
**Participantes:** Equipo Backend + DevOps
**Contexto:** El equipo necesita una forma estándar de levantar todos los servicios localmente sin conflictos entre máquinas.
**Decisión:** Docker Compose es el único método soportado para levantar el entorno completo en local. No se soporta ni documenta el inicio de servicios "sin Docker" en producción.
**Consecuencias:** Curva de aprendizaje para quienes no conocen Docker. A cambio, se elimina el "en mi máquina funciona" y se garantiza paridad con los ambientes dev/qa.
