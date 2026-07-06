# Eventos del Dominio

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

Los eventos del dominio representan hechos relevantes que **ya ocurrieron** dentro del sistema. Son la base del modelo de comunicación entre microservicios (arquitectura orientada a eventos).

---

## Catálogo de eventos

### Dominio: Gestión de Horarios

| Evento | Publicado por | Consumido por | Descripción |
|--------|---------------|---------------|-------------|
| `HorarioCreado` | `horarios-service` | `notificaciones-service` | Se registró una nueva asignación de horario (ficha + instructor + ambiente + bloque) |
| `HorarioModificado` | `horarios-service` | `notificaciones-service` | Se editó al menos un campo de un horario existente |
| `HorarioCancelado` | `horarios-service` | `notificaciones-service` | Un horario fue eliminado o marcado como cancelado |
| `ConflictoDetectado` | `horarios-service` | `horarios-service` (interno) | El sistema detectó solapamiento de instructor o ambiente al intentar crear/editar |

### Dominio: Gestión de Fichas

| Evento | Publicado por | Consumido por | Descripción |
|--------|---------------|---------------|-------------|
| `FichaRegistrada` | `fichas-service` | `horarios-service` | Una nueva ficha fue dada de alta en el sistema |
| `FichaActualizada` | `fichas-service` | `horarios-service` | Los datos de una ficha existente fueron modificados |
| `FichaInactivada` | `fichas-service` | `horarios-service`, `notificaciones-service` | Una ficha fue marcada como inactiva (fin de formación) |

### Dominio: Gestión de Instructores

| Evento | Publicado por | Consumido por | Descripción |
|--------|---------------|---------------|-------------|
| `InstructorRegistrado` | `usuarios-service` | `horarios-service` | Un nuevo instructor fue registrado en el sistema |
| `InstructorAsignado` | `horarios-service` | `notificaciones-service` | Un instructor fue asignado a un bloque de horario |
| `InstructorDesasignado` | `horarios-service` | `notificaciones-service` | Un instructor fue removido de un bloque de horario |
| `DisponibilidadActualizada` | `usuarios-service` | `horarios-service` | Un instructor actualizó su disponibilidad semanal |

### Dominio: Notificaciones

| Evento | Publicado por | Consumido por | Descripción |
|--------|---------------|---------------|-------------|
| `NotificacionEnviada` | `notificaciones-service` | — (solo log) | El sistema envió una notificación por correo |
| `NotificacionFallida` | `notificaciones-service` | `notificaciones-service` (reintento) | El envío de una notificación falló; se reintenta |

---

## Estructura de un evento

Todos los eventos siguen esta estructura JSON:

```json
{
  "eventId": "uuid-v4",
  "eventType": "HorarioCreado",
  "aggregateId": "uuid-del-horario",
  "aggregateType": "Horario",
  "occurredAt": "2026-07-06T14:30:00Z",
  "version": 1,
  "payload": {
    // datos específicos del evento
  }
}
```

---

## Ejemplo: HorarioCreado

```json
{
  "eventId": "a1b2c3d4-...",
  "eventType": "HorarioCreado",
  "aggregateId": "horario-001",
  "aggregateType": "Horario",
  "occurredAt": "2026-07-06T08:00:00Z",
  "version": 1,
  "payload": {
    "fichaId": "2879723",
    "instructorId": "usr-045",
    "ambienteId": "amb-12",
    "competencia": "Construcción de Software",
    "bloqueInicio": "2026-07-07T08:00:00-05:00",
    "bloqueFin": "2026-07-07T10:00:00-05:00",
    "creadoPor": "coord-001"
  }
}
```
