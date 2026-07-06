# Matriz de Trazabilidad

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

La matriz de trazabilidad relaciona los requisitos funcionales con las historias de usuario y los casos de prueba asociados. Permite verificar que todo requisito tiene al menos una historia de usuario que lo implementa y al menos un caso de prueba que lo valida.

---

## Matriz RF → HU → Caso de prueba

| Requisito Funcional | Historia de Usuario | Caso de Prueba (referencia) | Estado |
|--------------------|---------------------|----------------------------|--------|
| RF-001 — Login/logout | HU-001, HU-002 | CP-001, CP-002 | 🔴 Sin prueba aún |
| RF-002 — Roles y permisos | HU-001 (indirecto) | CP-003 | 🔴 Sin prueba aún |
| RF-003 — Gestión de fichas | HU-003, HU-004 | CP-010, CP-011, CP-012 | 🔴 Sin prueba aún |
| RF-004 — Gestión de instructores | HU-005, HU-006 | CP-020, CP-021 | 🔴 Sin prueba aún |
| RF-005 — Gestión de ambientes | HU-007 | CP-030 | 🔴 Sin prueba aún |
| RF-006 — Creación de horarios | HU-008 | CP-040, CP-041 | 🔴 Sin prueba aún |
| RF-007 — Detección de conflictos | HU-008, HU-009 | CP-042, CP-043 | 🔴 Sin prueba aún |
| RF-008 — Modificar/cancelar | HU-009, HU-010 | CP-050, CP-051, CP-052 | 🔴 Sin prueba aún |
| RF-009 — Consulta por rol | HU-011, HU-012 | CP-060, CP-061 | 🔴 Sin prueba aún |
| RF-010 — Historial de cambios | HU-013 | CP-070 | 🔴 Sin prueba aún |
| RF-011 — Notificaciones email | HU-008 (automático), HU-009, HU-010 | CP-080 | 🔴 Sin prueba aún |
| RF-012 — Gestión de usuarios | — (HU pendiente) | CP-090 | 🔴 Sin prueba aún |

---

## Cobertura de requisitos

| Total RF | Con al menos 1 HU | Con al menos 1 caso de prueba |
|----------|-------------------|-------------------------------|
| 12 | 11 (92%) | 0 (0%) — pruebas pendientes |

> 📌 **Nota:** Los casos de prueba (CP-XXX) se documentarán en `11-quality/test-cases/` una vez se inicien las fases de desarrollo y testing.

---

## Trazabilidad inversa: HU → RF

| Historia de Usuario | Requisito Funcional que satisface |
|--------------------|-----------------------------------|
| HU-001 | RF-001 |
| HU-002 | RF-001 |
| HU-003 | RF-003 |
| HU-004 | RF-003 |
| HU-005 | RF-004 |
| HU-006 | RF-004 |
| HU-007 | RF-005 |
| HU-008 | RF-006, RF-007 |
| HU-009 | RF-007, RF-008 |
| HU-010 | RF-008 |
| HU-011 | RF-009 |
| HU-012 | RF-009 |
| HU-013 | RF-010 |
