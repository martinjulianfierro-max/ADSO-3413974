# Historias de Usuario

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## HU-001 — Login de usuario

**Como** usuario del sistema (coordinador, instructor o aprendiz),  
**quiero** iniciar sesión con mi correo institucional y contraseña,  
**para** acceder a las funcionalidades de acuerdo con mi rol.

**Criterios de aceptación:**
- [ ] El formulario de login acepta email y contraseña.
- [ ] Al ingresar credenciales válidas, el sistema redirige al dashboard del rol correspondiente.
- [ ] Al ingresar credenciales inválidas, muestra el mensaje: "Correo o contraseña incorrectos."
- [ ] Tras 5 intentos fallidos consecutivos, la cuenta se bloquea por 15 minutos.
- [ ] El sistema emite un JWT con expiración de 8 horas.

**Referencia RF:** RF-001

---

## HU-002 — Logout seguro

**Como** usuario autenticado,  
**quiero** poder cerrar sesión en cualquier momento,  
**para** proteger mi cuenta en dispositivos compartidos.

**Criterios de aceptación:**
- [ ] Existe un botón "Cerrar sesión" visible en el menú de usuario.
- [ ] Al hacer clic, el JWT se invalida en el servidor y se elimina del almacenamiento local.
- [ ] Tras el logout, se redirige al formulario de login.

**Referencia RF:** RF-001

---

## HU-003 — Crear ficha

**Como** coordinador,  
**quiero** registrar una nueva ficha en el sistema,  
**para** poder asignarle horarios posteriormente.

**Criterios de aceptación:**
- [ ] El formulario incluye: código SENA (7 dígitos), programa, jornada, fecha de inicio y fecha de fin.
- [ ] El sistema valida que el código de ficha sea único; si ya existe, muestra error.
- [ ] La fecha de fin debe ser posterior a la fecha de inicio; si no, muestra error de validación.
- [ ] Al guardar exitosamente, la ficha aparece en el listado con estado ACTIVA.

**Referencia RF:** RF-003

---

## HU-004 — Inactivar ficha

**Como** coordinador,  
**quiero** marcar una ficha como inactiva cuando el grupo termina su formación,  
**para** que no sea posible asignarle nuevos horarios.

**Criterios de aceptación:**
- [ ] El coordinador puede cambiar el estado de una ficha de ACTIVA a INACTIVA.
- [ ] El sistema solicita confirmación antes de inactivar.
- [ ] Una ficha inactiva no aparece en la lista de opciones al crear un nuevo horario.
- [ ] Los horarios existentes de la ficha inactiva siguen siendo consultables.

**Referencia RF:** RF-003

---

## HU-005 — Registrar instructor

**Como** coordinador,  
**quiero** registrar un nuevo instructor en el sistema,  
**para** poder asignarlo a horarios.

**Criterios de aceptación:**
- [ ] El formulario incluye: nombre, cédula, correo, tipo (planta/contratista) y especialidades.
- [ ] La cédula y el correo deben ser únicos; error descriptivo si ya existen.
- [ ] El instructor creado queda en estado ACTIVO por defecto.
- [ ] Se genera automáticamente una cuenta de usuario con rol INSTRUCTOR y contraseña temporal.

**Referencia RF:** RF-004

---

## HU-006 — Declarar disponibilidad (instructor)

**Como** instructor,  
**quiero** declarar mis rangos de disponibilidad semanal,  
**para** que el coordinador tenga información sobre cuándo puedo ser asignado.

**Criterios de aceptación:**
- [ ] El instructor puede seleccionar bloques de tiempo disponibles por día de la semana.
- [ ] La disponibilidad es informativa; el coordinador puede asignar fuera de ella con advertencia.
- [ ] Los bloques de disponibilidad se muestran visualmente en el perfil del instructor.

**Referencia RF:** RF-004

---

## HU-007 — Registrar ambiente

**Como** coordinador,  
**quiero** registrar ambientes físicos o virtuales en el sistema,  
**para** poder asignarlos a los horarios.

**Criterios de aceptación:**
- [ ] El formulario incluye: nombre, tipo (aula/laboratorio/taller/sala de sistemas/virtual), capacidad y estado.
- [ ] El nombre del ambiente debe ser único.
- [ ] El estado inicial es DISPONIBLE.

**Referencia RF:** RF-005

---

## HU-008 — Crear horario

**Como** coordinador,  
**quiero** crear un horario asignando una ficha, un instructor, un ambiente y un bloque de tiempo,  
**para** organizar la formación de la semana.

**Criterios de aceptación:**
- [ ] El formulario incluye: ficha (solo activas), instructor (solo activos), ambiente (solo disponibles), competencia, fecha/hora inicio y fin.
- [ ] Al seleccionar instructor, ambiente y rango, el sistema verifica conflictos en tiempo real (antes de guardar).
- [ ] Si hay conflicto, se muestra un mensaje descriptivo indicando qué recurso está ocupado y en qué horario.
- [ ] No se puede guardar el horario si existe conflicto activo.
- [ ] Al guardar exitosamente, se publica el evento `HorarioCreado`.

**Referencia RF:** RF-006, RF-007

---

## HU-009 — Editar horario

**Como** coordinador,  
**quiero** modificar un horario existente,  
**para** corregir errores o adaptar cambios de último momento.

**Criterios de aceptación:**
- [ ] Se puede editar cualquier campo del horario (ficha, instructor, ambiente, competencia, rango de tiempo).
- [ ] El sistema re-valida conflictos con los nuevos valores antes de guardar.
- [ ] Cada cambio genera una entrada en el historial: campo, valor anterior, valor nuevo, usuario, timestamp.
- [ ] El instructor afectado recibe notificación por correo al modificar su asignación.

**Referencia RF:** RF-008

---

## HU-010 — Cancelar horario

**Como** coordinador,  
**quiero** cancelar un horario con un motivo registrado,  
**para** dejar constancia de por qué se anuló una sesión.

**Criterios de aceptación:**
- [ ] La acción de cancelar requiere ingresar un motivo (campo obligatorio, mínimo 10 caracteres).
- [ ] El estado del horario cambia a CANCELADO; el registro se mantiene visible en el historial.
- [ ] No es posible reactivar un horario cancelado; debe crearse uno nuevo.
- [ ] El instructor asignado recibe notificación de cancelación.

**Referencia RF:** RF-008

---

## HU-011 — Ver horario semanal (instructor)

**Como** instructor,  
**quiero** ver mi horario de la semana actual en formato de calendario,  
**para** saber cuándo y dónde tengo asignadas mis sesiones.

**Criterios de aceptación:**
- [ ] La vista muestra los bloques asignados al instructor en la semana seleccionada.
- [ ] Cada bloque muestra: ficha, competencia, ambiente, hora de inicio y fin.
- [ ] El instructor puede navegar entre semanas (anterior/siguiente).
- [ ] La vista es responsiva y funciona desde el celular.

**Referencia RF:** RF-009

---

## HU-012 — Consultar horario de ficha (aprendiz)

**Como** aprendiz,  
**quiero** consultar el horario de mi ficha sin necesidad de hacer login,  
**para** saber cuándo y dónde tengo clases esta semana.

**Criterios de aceptación:**
- [ ] El aprendiz puede consultar el horario ingresando el código de su ficha.
- [ ] La vista muestra todos los bloques activos de la semana: instructor, competencia, ambiente, hora.
- [ ] Si no hay horarios publicados para la semana, muestra "No hay horarios registrados esta semana."
- [ ] La vista es solo lectura; el aprendiz no puede modificar nada.

**Referencia RF:** RF-009

---

## HU-013 — Ver historial de cambios de un horario

**Como** coordinador,  
**quiero** consultar el historial de cambios de un horario,  
**para** auditar qué se modificó, por quién y cuándo.

**Criterios de aceptación:**
- [ ] Desde la vista de detalle de un horario, hay una sección "Historial de cambios".
- [ ] Cada entrada muestra: campo modificado, valor anterior, valor nuevo, usuario y fecha/hora.
- [ ] Las entradas están ordenadas de más reciente a más antiguo.

**Referencia RF:** RF-010
