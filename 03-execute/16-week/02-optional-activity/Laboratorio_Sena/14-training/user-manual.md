# Manual de Usuario

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Introducción

Este manual explica cómo usar el Sistema de Horarios SENA según su rol. El sistema permite consultar, crear y modificar horarios académicos de forma centralizada.

**Roles de usuario:**
- **Coordinador:** Gestión completa de horarios, fichas, instructores y ambientes.
- **Instructor:** Consulta de su horario personal y declaración de disponibilidad.
- **Aprendiz:** Consulta del horario de su ficha (sin login).

---

## Acceso al sistema

**URL:** `https://horarios.sena.edu.co` *(o la URL definida en producción)*

1. Abra el navegador (Chrome, Firefox o Edge recomendado).
2. Ingrese a la URL del sistema.
3. En la pantalla de **Login**, escriba su correo institucional y su contraseña.
4. Haga clic en **Iniciar sesión**.

> ⚠️ Si olvidó su contraseña, comuníquese con el administrador del sistema.

---

## Guía para Coordinadores

### Crear un horario

1. En el menú lateral, haga clic en **Horarios**.
2. Haga clic en el botón **+ Nuevo horario**.
3. Complete el formulario:
   - **Ficha:** Seleccione la ficha del listado.
   - **Instructor:** Seleccione el instructor asignado.
   - **Ambiente:** Seleccione el espacio físico o virtual.
   - **Competencia:** Escriba el nombre de la competencia a impartir.
   - **Bloque:** Seleccione la fecha, hora de inicio y hora de fin.
4. El sistema verificará automáticamente si hay conflictos. Si aparece una alerta roja, cambie el instructor, ambiente o bloque de tiempo.
5. Cuando no haya conflictos, haga clic en **Guardar**.

### Editar un horario

1. Vaya a **Horarios** y busque el horario que desea modificar.
2. Haga clic en el horario para ver su detalle.
3. Haga clic en **Editar**.
4. Modifique los campos necesarios.
5. El sistema re-verificará conflictos. Confirme los cambios.

> 📋 Todos los cambios quedan registrados en el **Historial de cambios** del horario.

### Cancelar un horario

1. Vaya al detalle del horario.
2. Haga clic en **Cancelar horario**.
3. Ingrese el motivo de la cancelación (obligatorio).
4. Confirme la acción. El horario pasa a estado CANCELADO.

---

## Guía para Instructores

### Ver mi horario

1. Al iniciar sesión, verá su **Horario de la semana actual**.
2. Use las flechas **← Semana anterior / Semana siguiente →** para navegar.
3. Cada bloque muestra: ficha, competencia, ambiente, hora de inicio y fin.

### Declarar disponibilidad

1. En el menú lateral, haga clic en **Mi disponibilidad**.
2. Seleccione los bloques de tiempo en los que está disponible cada día.
3. Haga clic en **Guardar disponibilidad**.

> ℹ️ La disponibilidad es informativa para el coordinador; no impide que le asignen horarios fuera de ella.

---

## Guía para Aprendices

### Consultar el horario de mi ficha

No necesita crear una cuenta ni hacer login.

1. En la pantalla principal, haga clic en **Consultar horario de mi ficha**.
2. Ingrese el código de su ficha (7 dígitos, ej: `2879723`).
3. El sistema mostrará los horarios activos de la semana actual.

---

## Preguntas frecuentes

| Pregunta | Respuesta |
|----------|-----------|
| ¿Por qué no puedo guardar un horario? | Es probable que haya un conflicto de instructor o ambiente. Lea el mensaje de alerta y ajuste el bloque de tiempo o los recursos asignados. |
| No recibí la notificación de un cambio de horario | Revise su carpeta de spam. Si el problema persiste, comuníquelo al administrador. |
| ¿Puedo ver el horario de otra ficha? | Solo el coordinador y el administrador pueden ver todos los horarios. Como instructor, solo ve el suyo. Como aprendiz, puede consultar cualquier ficha pública. |
| ¿Puedo reactivar un horario cancelado? | No. Debe crear un nuevo horario. |
