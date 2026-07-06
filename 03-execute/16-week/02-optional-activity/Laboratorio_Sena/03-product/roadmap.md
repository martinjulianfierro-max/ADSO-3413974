# Roadmap del Producto

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Fases del proyecto

### Fase 0 — Fundamentos (Semanas 1-3) ✅ En curso

**Objetivo:** Establecer la infraestructura documental, el entorno de desarrollo y las convenciones del equipo.

| Entregable | Estado |
|-----------|--------|
| Repositorio con estructura de carpetas completa | ✅ |
| Convenciones de Git y flujo de trabajo definidos | ✅ |
| Glosario, contexto y alcance documentados | ✅ |
| Modelo de dominio inicial (entidades y reglas) | ✅ |
| Entorno local con Docker Compose funcional | 🔴 |

---

### Fase 1 — MVP: Core de horarios (Semanas 4-10) 🔴 Pendiente

**Objetivo:** Sistema funcional básico con CRUD de horarios, detección de conflictos y autenticación.

| Épica | Funcionalidades incluidas |
|-------|--------------------------|
| E-01: Autenticación | Login/logout, JWT, roles básicos (coordinador, instructor, aprendiz) |
| E-02: Gestión de fichas | CRUD de fichas, validación de código SENA |
| E-03: Gestión de instructores | CRUD de instructores, declaración de disponibilidad |
| E-04: Gestión de ambientes | CRUD de ambientes con estado y capacidad |
| E-05: Gestión de horarios | Crear/editar/cancelar horarios; detección de conflictos en tiempo real |
| E-06: Consulta por rol | Vista coordinador (todo), vista instructor (propio), vista aprendiz (su ficha) |

**Criterio de éxito:** Un coordinador puede crear un horario semanal completo para una ficha sin conflictos.

---

### Fase 2 — Notificaciones y trazabilidad (Semanas 11-15) 🔴 Pendiente

**Objetivo:** Agregar el microservicio de notificaciones y el historial de cambios.

| Épica | Funcionalidades incluidas |
|-------|--------------------------|
| E-07: Notificaciones | Email automático al crear/modificar/cancelar horario |
| E-08: Historial de cambios | Registro de modificaciones; vista de auditoría para coordinador |
| E-09: Reportes básicos | Reporte de ocupación de ambientes; reporte de carga de instructor |

**Criterio de éxito:** Instructores reciben notificación en < 5 minutos tras un cambio en su horario.

---

### Fase 3 — Calidad y operaciones (Semanas 16-20) 🔴 Pendiente

**Objetivo:** Cobertura de pruebas, monitoreo y documentación para despliegue en producción.

| Épica | Funcionalidades incluidas |
|-------|--------------------------|
| E-10: Testing | Pruebas unitarias (≥ 80% cobertura), integración y E2E |
| E-11: Observabilidad | Logging centralizado, métricas básicas (Prometheus/Grafana) |
| E-12: Seguridad | Revisión OWASP, HTTPS obligatorio, sanitización de inputs |
| E-13: Documentación de usuario | Manual de usuario, onboarding técnico |

**Criterio de éxito:** El sistema pasa revisión técnica de calidad y puede ser entregado al centro CBA.

---

## Línea de tiempo visual

```
Sem 1   Sem 3   Sem 4        Sem 10   Sem 11     Sem 15   Sem 16       Sem 20
  |-------|-------|------------|--------|-----------|--------|------------|
  [Fase 0]       [   Fase 1 — MVP Core            ]
                              [  Fase 2 — Notif+Audit ]
                                                   [ Fase 3 — Calidad  ]
```
