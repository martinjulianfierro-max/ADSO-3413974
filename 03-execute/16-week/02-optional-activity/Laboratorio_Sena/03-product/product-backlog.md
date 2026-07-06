# Product Backlog

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Épicas y características priorizadas

El backlog está ordenado por prioridad (1 = más alto). Los ítems de Fase 1 están detallados; los de Fase 2 y 3 se refinan progresivamente.

---

### Fase 1 — MVP

| ID | Épica | Prioridad | Esfuerzo estimado | Estado |
|----|-------|-----------|-------------------|--------|
| E-01 | Autenticación y roles | 1 | L | 🔴 Pendiente |
| E-02 | Gestión de fichas | 2 | M | 🔴 Pendiente |
| E-03 | Gestión de instructores | 3 | M | 🔴 Pendiente |
| E-04 | Gestión de ambientes | 4 | S | 🔴 Pendiente |
| E-05 | Gestión de horarios (CRUD + conflictos) | 5 | XL | 🔴 Pendiente |
| E-06 | Vistas diferenciadas por rol | 6 | L | 🔴 Pendiente |

---

### Fase 2 — Notificaciones y trazabilidad

| ID | Épica | Prioridad | Esfuerzo estimado | Estado |
|----|-------|-----------|-------------------|--------|
| E-07 | Notificaciones por email | 7 | L | 🔴 Pendiente |
| E-08 | Historial de cambios y auditoría | 8 | M | 🔴 Pendiente |
| E-09 | Reportes básicos | 9 | M | 🔴 Pendiente |

---

### Fase 3 — Calidad y operaciones

| ID | Épica | Prioridad | Esfuerzo estimado | Estado |
|----|-------|-----------|-------------------|--------|
| E-10 | Suite de pruebas | 10 | XL | 🔴 Pendiente |
| E-11 | Observabilidad y monitoreo | 11 | L | 🔴 Pendiente |
| E-12 | Seguridad y hardening | 12 | M | 🔴 Pendiente |
| E-13 | Documentación de usuario y operaciones | 13 | M | 🔴 Pendiente |

---

## Detalle de épica E-01: Autenticación y roles

| ID | Historia de usuario | Criterios de aceptación |
|----|---------------------|------------------------|
| HU-001 | Como coordinador, quiero hacer login con mi email y contraseña para acceder al sistema. | JWT emitido en login; sesión caduca en 8h; contraseña con bcrypt |
| HU-002 | Como sistema, quiero proteger los endpoints según el rol del usuario para evitar accesos no autorizados. | Coordinador puede CRUD; Instructor solo lectura de su horario; Aprendiz solo lectura de su ficha |
| HU-003 | Como administrador, quiero crear y desactivar cuentas de usuario para gestionar el acceso al sistema. | CRUD de usuarios; rol asignable; cuentas desactivadas no pueden hacer login |

---

## Detalle de épica E-05: Gestión de horarios

| ID | Historia de usuario | Criterios de aceptación |
|----|---------------------|------------------------|
| HU-010 | Como coordinador, quiero crear un horario asignando ficha, instructor, ambiente y bloque de tiempo. | Formulario con validación en tiempo real; alerta si hay conflicto antes de guardar |
| HU-011 | Como coordinador, quiero que el sistema me alerte si el instructor ya está ocupado en ese bloque. | Alerta visible antes de confirmar; no se puede guardar hasta resolver el conflicto |
| HU-012 | Como coordinador, quiero modificar un horario existente y que los cambios queden en el historial. | Historial con campo, valor anterior, valor nuevo, usuario y timestamp |
| HU-013 | Como coordinador, quiero cancelar un horario con un motivo registrado. | Estado cambia a CANCELADO; motivo obligatorio; historial actualizado |
| HU-014 | Como instructor, quiero ver mi horario semanal con todos mis bloques asignados. | Vista de calendario semanal; filtrable por semana; información de ficha y ambiente |
| HU-015 | Como aprendiz, quiero consultar el horario de mi ficha para saber a qué hora y dónde tengo clases. | Vista de horario de ficha; acceso solo lectura; actualizado en tiempo real |

---

## Escala de esfuerzo

| Talla | Descripción aproximada |
|-------|------------------------|
| S | < 1 día de trabajo del equipo |
| M | 2–3 días |
| L | 1 semana |
| XL | 2+ semanas |
