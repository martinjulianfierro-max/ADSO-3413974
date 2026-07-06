# Mapa del Dominio

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Bounded Contexts

El sistema de horarios SENA se divide en **4 contextos acotados (bounded contexts)** bien definidos. Cada contexto tiene su propio modelo de dominio y se comunica con los demás a través de eventos o contratos de API.

```
┌────────────────────────────────────────────────────────────────────────┐
│                    SISTEMA DE HORARIOS SENA                            │
│                                                                        │
│  ┌─────────────────────┐        ┌─────────────────────────────────┐   │
│  │  Gestión de Fichas  │──────▶ │     Gestión de Horarios         │   │
│  │  (fichas-service)   │        │     (horarios-service)          │   │
│  │                     │        │                                 │   │
│  │  • Ficha            │        │  • Horario                      │   │
│  │  • Programa         │        │  • Bloque                       │   │
│  │  • Jornada          │        │  • Conflicto                    │   │
│  └─────────────────────┘        └─────────────────────────────────┘   │
│           │                                      │                     │
│           │                                      │                     │
│           ▼                                      ▼                     │
│  ┌─────────────────────┐        ┌─────────────────────────────────┐   │
│  │  Gestión de         │        │     Notificaciones              │   │
│  │  Usuarios/Roles     │──────▶ │     (notificaciones-service)    │   │
│  │  (usuarios-service) │        │                                 │   │
│  │                     │        │  • Notificación                 │   │
│  │  • Instructor       │        │  • Canal (Email)                │   │
│  │  • Coordinador      │        │  • Plantilla                    │   │
│  │  • Aprendiz         │        │                                 │   │
│  │  • Rol / Permiso    │        │                                 │   │
│  └─────────────────────┘        └─────────────────────────────────┘   │
│                                                                        │
└────────────────────────────────────────────────────────────────────────┘
```

---

## Descripción de cada contexto

### 1. Gestión de Fichas (`fichas-service`)

**Responsabilidad:** Mantener el catálogo de fichas activas del SENA. Es la fuente de verdad de qué grupos existen, a qué programa pertenecen y en qué jornada operan.

**Entidades principales:** `Ficha`, `Programa`, `Jornada`

**Eventos que publica:** `FichaRegistrada`, `FichaActualizada`, `FichaInactivada`

**Dependencias:** Ninguna (es un contexto raíz).

---

### 2. Gestión de Usuarios/Roles (`usuarios-service`)

**Responsabilidad:** Gestionar los actores del sistema: quiénes son, qué roles tienen y cuándo están disponibles. Incluye autenticación (emisión de JWT) y autorización.

**Entidades principales:** `Usuario`, `Instructor`, `Coordinador`, `Aprendiz`, `Rol`, `Disponibilidad`

**Eventos que publica:** `InstructorRegistrado`, `DisponibilidadActualizada`

**Dependencias:** Ninguna (es un contexto raíz).

---

### 3. Gestión de Horarios (`horarios-service`)

**Responsabilidad:** Núcleo del sistema. Gestiona la asignación de fichas, instructores y ambientes en bloques de tiempo. Detecta conflictos y mantiene el historial de cambios.

**Entidades principales:** `Horario`, `Bloque`, `Ambiente`, `HistorialCambio`

**Eventos que publica:** `HorarioCreado`, `HorarioModificado`, `HorarioCancelado`, `ConflictoDetectado`

**Dependencias:** Consume datos de `fichas-service` y `usuarios-service`.

---

### 4. Notificaciones (`notificaciones-service`)

**Responsabilidad:** Escuchar eventos de los otros servicios y disparar las notificaciones correspondientes (correo electrónico) a los actores afectados.

**Entidades principales:** `Notificacion`, `Plantilla`, `Canal`

**Eventos que publica:** `NotificacionEnviada`, `NotificacionFallida`

**Dependencias:** Consume eventos de `horarios-service` y `fichas-service`.

---

## Relaciones entre contextos

| Upstream (publica) | Downstream (consume) | Mecanismo | Dato compartido |
|--------------------|----------------------|-----------|-----------------|
| `fichas-service` | `horarios-service` | Evento / API | `fichaId`, datos de la ficha |
| `usuarios-service` | `horarios-service` | Evento / API | `instructorId`, disponibilidad |
| `horarios-service` | `notificaciones-service` | Evento | Cambios en horarios |
| `fichas-service` | `notificaciones-service` | Evento | Cambios en fichas |
