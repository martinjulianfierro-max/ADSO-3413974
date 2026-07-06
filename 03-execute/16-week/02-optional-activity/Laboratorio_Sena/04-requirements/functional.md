# Requisitos Funcionales

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## RF-001 — Autenticación de usuarios

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-001 |
| **Nombre** | Login y logout de usuarios |
| **Descripción** | El sistema debe permitir a los usuarios autenticarse con su correo institucional y contraseña. Al autenticarse se emite un JWT con rol y expiración de 8 horas. El sistema debe permitir cerrar sesión, invalidando el token. |
| **Actor** | Coordinador, Instructor, Aprendiz, Administrador |
| **Prioridad** | Alta |

---

## RF-002 — Gestión de roles y permisos

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-002 |
| **Descripción** | El sistema debe controlar el acceso según el rol del usuario autenticado. Los roles son: `COORDINADOR`, `INSTRUCTOR`, `APRENDIZ`, `ADMIN`. Cada rol tiene permisos específicos sobre los recursos del sistema. |
| **Prioridad** | Alta |

**Tabla de permisos por rol:**

| Recurso | ADMIN | COORDINADOR | INSTRUCTOR | APRENDIZ |
|---------|-------|-------------|------------|----------|
| Usuarios (CRUD) | ✅ | ❌ | ❌ | ❌ |
| Fichas (CRUD) | ✅ | ✅ | ❌ | ❌ |
| Instructores (CRUD) | ✅ | ✅ | ❌ (ver propio) | ❌ |
| Ambientes (CRUD) | ✅ | ✅ | ❌ | ❌ |
| Horarios (crear/editar/cancelar) | ✅ | ✅ | ❌ | ❌ |
| Horarios (consultar) | ✅ | ✅ (todos) | ✅ (propio) | ✅ (su ficha) |

---

## RF-003 — Gestión de fichas

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-003 |
| **Descripción** | El sistema debe permitir crear, editar, consultar y desactivar fichas. Una ficha tiene: código SENA (7 dígitos, único), nombre del programa, jornada, fecha de inicio y fecha de fin. |
| **Actor** | Coordinador, Administrador |
| **Prioridad** | Alta |

---

## RF-004 — Gestión de instructores

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-004 |
| **Descripción** | El sistema debe permitir registrar, editar y desactivar instructores. Cada instructor tiene nombre, cédula (único), correo, tipo de vinculación y lista de especialidades. Un instructor puede declarar su disponibilidad semanal. |
| **Actor** | Coordinador, Administrador |
| **Prioridad** | Alta |

---

## RF-005 — Gestión de ambientes

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-005 |
| **Descripción** | El sistema debe permitir registrar, editar y cambiar el estado de ambientes físicos o virtuales. Cada ambiente tiene nombre (único), tipo, capacidad y estado. |
| **Actor** | Coordinador, Administrador |
| **Prioridad** | Alta |

---

## RF-006 — Creación de horarios

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-006 |
| **Descripción** | El sistema debe permitir al coordinador crear un horario asignando: ficha, instructor, ambiente, competencia, bloque de inicio y bloque de fin. Antes de guardar, el sistema valida que no existan conflictos de instructor ni de ambiente en el rango de tiempo seleccionado. |
| **Actor** | Coordinador |
| **Prioridad** | Alta |

---

## RF-007 — Detección de conflictos en tiempo real

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-007 |
| **Descripción** | Al seleccionar instructor, ambiente y rango de tiempo en el formulario de creación/edición de horario, el sistema debe verificar en tiempo real si existen conflictos y mostrar una alerta descriptiva. No se permite guardar un horario con conflictos activos. |
| **Actor** | Sistema (automático durante el flujo del coordinador) |
| **Prioridad** | Alta |

---

## RF-008 — Modificación y cancelación de horarios

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-008 |
| **Descripción** | El coordinador puede editar cualquier campo de un horario activo. Cada modificación genera una entrada en el historial de cambios. También puede cancelar un horario (requiere motivo). Un horario cancelado no puede ser reactivado; debe crearse uno nuevo. |
| **Actor** | Coordinador |
| **Prioridad** | Alta |

---

## RF-009 — Consulta de horarios

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-009 |
| **Descripción** | El sistema debe ofrecer vistas de horario filtradas por rol. El coordinador ve todos los horarios con filtros por ficha, instructor, ambiente y semana. El instructor ve solo sus horarios. El aprendiz ve el horario de su ficha. |
| **Actor** | Coordinador, Instructor, Aprendiz |
| **Prioridad** | Alta |

---

## RF-010 — Historial de cambios

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-010 |
| **Descripción** | Cada modificación a un horario queda registrada en un historial inmutable con: campo modificado, valor anterior, valor nuevo, usuario responsable y timestamp. El coordinador puede consultar el historial de cualquier horario. |
| **Actor** | Sistema (automático) + Coordinador (consulta) |
| **Prioridad** | Media |

---

## RF-011 — Notificaciones por correo

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-011 |
| **Descripción** | El sistema debe enviar notificaciones automáticas por correo electrónico cuando: (a) se crea un nuevo horario, (b) se modifica un horario existente, (c) se cancela un horario. Los destinatarios son el instructor asignado y, opcionalmente, representantes de la ficha. |
| **Actor** | Sistema (automático) |
| **Prioridad** | Media |

---

## RF-012 — Gestión de usuarios (admin)

| Atributo | Detalle |
|----------|---------|
| **ID** | RF-012 |
| **Descripción** | El administrador puede crear, editar, desactivar y consultar cuentas de usuario. Puede asignar roles. Las cuentas desactivadas no pueden iniciar sesión. |
| **Actor** | Administrador |
| **Prioridad** | Media |
